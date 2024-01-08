### 微信中打开从app分享出去的小程序,不展示homebutton

从app端分享小程序到微信,从微信打开该页面后homeButton按钮有时展示、有时不展示.还有以下几种状态:

1. 第一次打开从app分享过来的小程序,不展示homebutton按钮;

2. 刷新当前页面,也不展示homebutton;

3. 从小程序分享出去的页面,默认都是好的,可以正常展示homebutton


解决思路:

1. 显示设置navigationStyle:default看下效果,不使用默认值;

> 默认值是default

2. 看下app的分享信息:需要找app开发获取信息