# 了解OAuth2.0
###客户端应用授权
1.
引导需要授权的用户到如下地址：
```
http://api.pigai.org/oauth2/authorize?response_type=token&client_id=Your_Client_Id&redirect_uri=Your_Registered_Redirect_Uri&state=Your_State"
```
2.
如果授权成功,页面跳转至 `Your_Registered_Redirect_Uri/#access_token=TOKEN`
