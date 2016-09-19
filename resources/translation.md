# 翻译资源

## 句子翻译
> API: http://api.pigai.org/translation/trans_sentence

######请求参数(POST/GET)

| 参数名称 | 参数说明 |
|---|---|
| rid | String，批改网作文号 |
| snt | String，答案 |
| referer | JSON串，参考答案, 格式如: '["referer1", 'referer2']'|
| info_word | JSON串，限定词, 格式如: '["word1", "word2"]' |
| access_token | 必须，这个token如何获取是通过[授权流程](../handbooks/workflows.html)得到这个token |
| scope | 资源访问控制，固定值:all_json |

###资源scope
根据`appkey`的作用范围，开发者每次通过认证获取的access_token都有一个作用域`scope`,决定了该token能否从批改网的api获取正确的返回值。

###返回结果
######成功
```json
{
    "error": "success",
    "error_code": 0,
    "error_description": "success",
    "data": {}
}
```
######失败
```json
{
    "error": "原因",
    "error_code": 21329,
    "error_description": "原因描述"
}
```

######scope为all_json的返回详细格式

```json
{
    "error": "success",
    "error_code": 0,
    "error_description": "success",
    "data": {
        "id": "0",
        "dsk": {
            "kw": {
                "hand": 0.55479014,
                "look": 0.42604497,
                "hold": 0.49634662,
                "key": 0.5141338
            },
            "doccmd_list": "Sntbr,Sntsum,Kwsim,DimExpr,Scorer,Pingyu",
            "doc": {
                "gramv_ratio": 0.4761905,
                "cl_ratio": 0.9090909,
                "d_ttr1": 0.70710677,
                "d_ttr2": 1,
                "token_devia_ratio": 0,
                "complex_max": 2,
                "score": 48.326786,
                "awl_sd": 2.1514616,
                "para_last_tratio": 1,
                "grammar_err": 0,
                "whcl_num": 0,
                "prmods_ratio_new": 0.64285713,
                "d_num": 1,
                "ptprtcl_num": 1,
                "r_ttr": 1,
                "n_ttr2": 2,
                "ttr1": 2.4494898,
                "n_ttr1": 1,
                "spell_correct_ratio": 1,
                "sub_tc": 9,
                "d_len": 10,
                "fitted_num": 0,
                "kp_correct_ri": 1,
                "prprn_num": 0,
                "score_kpu": 0,
                "incomplete_num": 0,
                "x_len": 0,
                "ast_new": 14,
                "mwe_disconj": 0,
                "atl_sd": 2.2738357,
                "word_gt7": 0.083333336,
                "content_word_ratio": 0,
                "para_first_sratio": 1,
                "lex_num": 14,
                "word_gt6": 0.16666667,
                "word_gt9": 0.083333336,
                "word_gt8": 0.083333336,
                "n_ttr": 1,
                "grammar_correct_ri": 1,
                "simple_sent_ri": 1,
                "r_len": 3,
                "asl": 62,
                "mwe_pv": 0,
                "snt_num": 1,
                "lemma_type": 14,
                "v_len": 4,
                "psmods_ratio": 0.2857143,
                "r_type": 3,
                "kw_overlap": 0,
                "gramv_vxp": 1,
                "lemma_num": 14,
                "gramv_vov": 0,
                "r_ratio": 0.21428572,
                "a_num": 1,
                "r_num": 3,
                "para_last_sratio": 1,
                "a_ttr2": 1,
                "a_ttr1": 0.70710677,
                "subcl_num": 0,
                "a_ttr": 1,
                "comma_ratio": 0.07092199,
                "compcl_num": 0,
                "para_token_avg": 14,
                "token_num": 14,
                "para_num": 1,
                "v_ratio": 0.14285715,
                "ttr": 100,
                "psmods_tc": 4,
                "d_type": 1,
                "a_ratio": 0.071428575,
                "word_diff_avg": 3.673077,
                "b3_b1": 0.010791368,
                "incomplete_ratio": 0,
                "mwe_pronaux": 0,
                "ast_sd": 0,
                "x_num": 0,
                "token_type": 14,
                "gramv": 1,
                "pred_diff_max3": 1.6766667,
                "pred_diff_max2": 2.515,
                "prmods_ratio": 0.64285713,
                "pred_diff_max1": 5.03,
                "fitted_ratio": 0,
                "complex_factor": 2,
                "a_len": 3,
                "snt_correct_ratio": 0.9090909,
                "r_ttr1": 1.2247449,
                "r_ttr2": 3,
                "dot_ratio": 0.07092199,
                "n_len": 3.5,
                "n_ratio": 0.14285715,
                "spell_err": 0,
                "snt_tc_10_19": 0.9090909,
                "doc_strlen": 62,
                "prmods_tc": 9,
                "snt_tc_40_": 0,
                "snt_tc_30_39": 0,
                "external_sim": 0,
                "mwe_pv_ratio": 0,
                "gramv_vxxp": 0,
                "v_ttr1": 1,
                "v_ttr2": 2,
                "word_diff_num": 12,
                "n_num": 2,
                "para_snt_avg": 1,
                "h_ttr2": 2,
                "h_ttr1": 1,
                "c_ratio": 0,
                "c_type": 0,
                "n_type": 2,
                "pred_diff_avg": 5.03,
                "awl": 4.0833335,
                "h_len": 1,
                "para_first_tratio": 1,
                "word_type": 12,
                "h_ratio": 0.14285715,
                "the_ratio": 0.07092199,
                "snt_tc_20_29": 0,
                "p_ttr1": 1.2247449,
                "mwe_pvd": 0,
                "p_ttr2": 3,
                "cate": 0,
                "h_type": 2,
                "snt_max": 14,
                "prmods_tc_new": 9,
                "p_ttr": 1,
                "b3": 0,
                "b2": 0.083333336,
                "ast": 14,
                "v_type": 2,
                "b4": 0,
                "b1_bu": 0.08333343,
                "p_num": 3,
                "doc_tc": 14,
                "atl": 3.642857,
                "cl_sum": 1,
                "gramv_idf": 19.520456,
                "snt_tc_0_9": 0,
                "b0": 0,
                "b1": 0.91666657,
                "x_type": 0,
                "c_num": 0,
                "h_ttr": 1,
                "v_ttr": 1,
                "internal_sim": 0.050087586,
                "lex_type": 14,
                "snt_min": 14,
                "c_len": 0,
                "ttr2": 12,
                "p_len": 3,
                "x_ratio": 0,
                "b0_num": 0,
                "a_type": 1,
                "kp_err": 0,
                "simple_sent_num": 0,
                "infcl_num": 0,
                "punct_err": 0,
                "prprn_type": 0,
                "cl_type": 1,
                "h_num": 2,
                "prprtcl_num": 0,
                "d_ttr": 1,
                "d_ratio": 0.071428575,
                "v_num": 2,
                "relcl_num": 0,
                "sc_num": 0,
                "word_num": 12,
                "p_type": 3,
                "p_ratio": 0.21428572
            },
            "snt": [
                {
                    "feedback": {
                        "hold": {
                            "cate": "confusion",
                            "ibeg": 4,
                            "word_list": "held",
                            "iend": 5,
                            "long_msg": "<a href='http://www.jukuu.com/search.php?q=contain'/>contain</a>: 普通用词，所涉及的物体常常是其组成部分或内容。强调包容关系。既可指具体有形的东西，也可指抽象无形的东西。<br><a href='http://www.jukuu.com/search.php?q=include'/>include</a>: 普通用词，指一整体包含着各独立的部分，也指某东西包含另一东西的某一部分。<br><a href='http://www.jukuu.com/search.php?q=embrace'/>embrace</a>: 正式用词，指把某事物纳入整个之中。<br><a href='http://www.jukuu.com/search.php?q=involve'/>involve</a>: 把包含因整体的性质决定的成分或结果。所包括的往往是无形的，不可触知的东西，多用作引申。<br><a href='http://www.jukuu.com/search.php?q=comprehend'/>comprehend</a>: 正工用词，指包含在整体范围以内。<br><a href='http://www.jukuu.com/search.php?q=hold'/>hold</a>: 常和contain换用。指能够容纳或有足够的容纳量。强调包容能力。<br><a href='http://www.jukuu.com/search.php?q=comprise'/>comprise</a>: 书面用词，暗指一个整体包括不同部分所组成，可与include交换使用。",
                            "kp": "hold",
                            "by": "pigai_spss.kp_feedback_cn",
                            "short_msg": "易混词汇: contain, include, embrace, involve, comprehend, <b>hold</b>, comprise 均含有“包括，包含”之意。"
                        }
                    },
                    "meta": {
                        "pred_lemma": "look",
                        "sid": 0,
                        "complex_factor": 2,
                        "vpat": [
                            "look for _n"
                        ],
                        "tense": [
                            "loc_sr",
                            "past"
                        ],
                        "para_id": 1,
                        "postag": "^_^_^ With_in_par8_p7_s14_with the_dt_sb2_n2_the keys_nns_sb_n_key held_vbn_ptprtcl4_vp4_hold in_in_p3_in his_prp$_sb2_ones_n2_a_his hand_nn_sb_n_hand ,_,_h_, he_prp_sb_n_he looked_vbd_vp4_pastten_v_look for_in_p2_for them_prp_sb_n_them everywhere_rb_d_everywhere ._._h_.",
                        "pid": 1,
                        "pos_rewrite": "[^/^, With/IN, the/DT, keys/NNS, held/VBN, in/IN, his/PRP$, hand/NN, ,/,, he/PRP, looked/VBD, for/IN, them/PRP, everywhere/RB, ./.]",
                        "snt": "With the keys held in his hand, he looked for them everywhere.",
                        "sub_cnt": 9,
                        "tc": 14,
                        "lex_list": "With the keys held in his hand , he looked for them everywhere ."
                    }
                }
            ],
            "info": {
                "time": 2,
                "my_port": 7097,
                "rid": "716896",
                "my_ip": "192.168.1.215",
                "did": "0",
                "formula_id": "1",
                "cate_score": {
                    "0": 0,
                    "1": 46.469402,
                    "2": 75.7108,
                    "3": 21.21213,
                    "4": 37.565693
                },
                "final_score": 48.326786,
                "formular_score": 28.534348,
                "pingyu_key": "ttr1:1_b3:1_spell:9 ast:7_cld:4_sntc:8 discd:1_pvd:1 ",
                "pingyu": "单词拼写做得很好，请注意积累词汇量；从句数量偏少，且文中有几处句子错误；语言不流畅。"
            }
        },
        "status": "ok",
        "score": 41.72261428833
    }
}
```
