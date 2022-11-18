## Dsk 说明

## rabmitMq版本

## http版本

>POST http://server.com/wps-gec-dsk?use_gec=true&topk_gec=64&max_snt_len=2048&with_score=true&score_snts=32&internal_sim_default=0.2&ibeg_byte=true&diffmerge=false&mkfbatch=0&dskhost=172.17.0.1%3A7095&timeout=9
{
    "essay": "English is a internationaly language which becomes importantly for modern world. 中文In China, English is took to be a foreigh language which many student choosed to learn.\n\n They use at least one hour to learn English knowledges a day."
}




| 参数名称 | 参数说明 |
|---|---|
| use_gec| bool 为True 时启动gpu的gec翻译 |
| topk_gec|int = 64 , 只翻译文中 前64 个句子 |
|max_snt_len| int=2048, 超过这个长度的句子不分析| 
|with_score |bool=True, 为False时 不打分 |
| score_snts| int=32, 取文中前32个句子进行打分|
| internal_sim_default| float=0.2 , 缺省内相关度，这个维度计算很重，wps不需要，直接取缺省值|
|ibeg_byte|bool=True： 返回偏移， wps前端定位需求|
|diffmerge|bool=False：GEC的合并策略|
|mkfbatch| int=0： 在调用mkf时的并发数|
|dskhost| str="172.17.0.1:7095" 提供dsk-java分析的api|
|timeout|int=9 ： 调用gec时的blpop等待时间| 

返回结果
```json
{
  "snt": [ //按句子结构返回
    {
      "feedback": { //反馈
        "_for modern world@e_prep.wrong": { //kp key
          "cate": "e_prep.wrong",//错误类别
          "iend": 12, //本句子内 词汇结束位置
          "kp": "_for modern world",//kp
          "by": "pigai_spss.kp_feedback_cn",
          "word_list": "for modern world",
          "ibeg": 9, //本句子内 词汇开始位置
          "id": 1249650,
          "short_msg": "介词误用，建议将<b>for modern world</b>改为<b>in modern world</b>。", //返回信息
          "kp_type": "HYB",
          "ibeg_byte": 63, //本句子内 字母开始位置
          "iend_byte": 79 //本句子内 字母结束位置
        },
        "internationaly@e_spell": {
          "cate": "e_spell",
          "iend": 5,
          "correct": "",
          "kp": "internationaly",
          "ibeg": 4,
          "iwc": 1,
          "by": "pigai_spss.kp_feedback_cn",
          "word_list": "internationaly",
          "id": 1258443,
          "short_msg": "拼写不规范，<b>internationaly</b>是不是：<b>internationally</b>、<b>international</b>、<b>internationale</b>。",
          "kp_type": "HYB",
          "ibeg_byte": 13,
          "iend_byte": 27
        }
      },
      "meta": {
        "pid": 0,
        "para_id": 0, //段落
        "sid": 0, //段落内的句子标号
        "tc": 12,
        "sub_cnt": 1,
        "pos_rewrite": "[^/^, English/NNP, is/VBZ, a/DT, internationaly/NNP, language/NN, which/WDT, becomes/VBZ, importantly/RB, for/IN, modern/JJ, world/NN, ./.]",
        "pred_lemma": "be",
        "postag": "^_^_^ English_nnp_language_ilanguage_n_sb_english is_vbz_v_presten_be a_dt_n3_a internationaly_nnp_gpe_n_internationaly language_nn_n_language which_wdt_n_which becomes_vbz_v_presten_become importantly_rb_importantly for_in_for modern_jj_n2_modern world_nn_n_world ._._.",
        "snt": "English is a internationaly language which becomes importantly for modern world.", //去空格后的句子
        "lex_list": "English is a internationaly language which becomes importantly for modern world .",
        "vpat": [
          "be _n"
        ],
        "tense": "",
        "snt_ori": "English is a internationaly language which becomes importantly for modern world." //原来的句子
      }
    },
    {
      //同上
    },
    {
        //同上
    }
  ],
  "info": {
    "essay": "原来的文章",
    "formula_score": 45.96, //分析的文章
    "cate_score": {  //4大分类分数
      "1": 14.36,
      "2": 54.16,
      "3": 38.2,
      "4": 63.79
    },
    "pingyu": "请增加词汇的积累；文章词汇表达做的很好，请注意词汇表达的多样性；请作者增加词汇表达的丰富度，请注意词汇表达的多样性",// 评语
    "timing": 0.6566987037658691 //时间
  },
  "doc": {
    "word_gt7": 0.2727272727272727,
    "b3": 0,
    "b3_b1": 0.003115264797507788,
    "ttr": 72.71074755737332,
    "ttr1": 3.4112114616897666,
    "ttr2": 23.267439218359463,
    "doc_tc": 43,
    "cl_sum": 3,
    "cl_dens": 1,
    "cl_ratio": 1,
    "awl": 4.4772727272727275,
    "awl_sd": 2.9270574454998655,
    "ast": 14.666666666666666,
    "asl": 77.66666666666667,
    "ast_sd": 2.3273733406281565,
    "mwe_pv": 1.3333333333333333,
    "mwe_disconj": 1,
    "pv_dens": 1.3333333333333333,
    "disconj_dens": 1,
    "v_ratio": 0.20454545454545456,
    "n_ratio": 0.29545454545454547,
    "jj_ratio": 0.045454545454545456,
    "rb_ratio": 0.06818181818181818,
    "cc_ratio": 0,
    "comma_ratio": 0.022727272727272728,
    "art_ratio": 0.06818181818181818,
    "simple_sent_ratio": 0,
    "simple_sent_ri": 1,
    "word_diff_avg": 4.6658437500000005,
    "pred_diff_max3": 3.923333333333334,
    "prmods_tc": 2.75,
    "prmods_ratio": 0.16349206349206347,
    "tc": 44,
    "snt_num": 3, //句子数
    "word_num": 44,//词汇数
    "word_type": 32,
    "internal_sim": 0.2
  }
}
```

