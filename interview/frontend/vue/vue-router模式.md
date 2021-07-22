### vue-router的各种模式

我们都知道，vue-route有hash和history两种路由模式，那么这两种方式有什么区别呢？

我们现在以vue-router4.x版本为例进行说明。

### hash模式不可以实现浏览器的前进、后退？

经验证，hash模式和history模式都是可以实现浏览器的前进和后退的，不存在说history模式可以实现浏览器的前进和后退，而hash模式不能实现浏览器的前进后退功能。

### history模式可以不配置服务器直接使用吗？

一般情况下，如果我们的页面只是一次新访问的，那么是可以不需要配置服务器做一些配合的。在不配置服务器支持的情况下，也能实现浏览器的前进和后退，只是页面不能刷新，页面一刷新就会跳转到一个404页面。

在使用了history模式的时候，还是要配置下服务器来支持的，这一步不可省。如果我们确实有一些页面只能访问一次的场景，我们可以通过其他的更加友好的解决方案。

使用了history路由模式的站点，通过nginx配置的demo：

```bash
server {
    listen       80;
    server_name  www.yourdomain.com;

    location / {
        root   D:\www.yourdomain.com\dist;
        #index  index.html index.html;
	    try_files $uri $uri/ /index.html;
    }
}
```