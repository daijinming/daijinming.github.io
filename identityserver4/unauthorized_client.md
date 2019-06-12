对接IdentityServer4，登录时，如果出现下面的问题  

>错误
抱歉，出现了一个错误 : unauthorized_client
请求 ID: 0HLNERT8AI3TT:00000004


原因有以下几种：
~~~
1、clientid\clientsecret 和管理端不一致
2、没有开启[允许离线访问]
3、允许的作用域，客户端和管理端核对不上，比如客户端需要设置了api1,但是管理端并未分派
4、重定向 Uri 不对，比如 http://localhost/signin-oidc
5、允许的授权类型：hybrid 必填
~~~
