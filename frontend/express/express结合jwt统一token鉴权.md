### token鉴权登录的优势

token鉴权登录的优势:无状态、可以跨域、可以防止csrf、性能好(每次请求不用去服务器请求相应的session),客户端只需要将token存入本地,每次访问服务端(请求接口)的时候,headers上加上token即可.

### express