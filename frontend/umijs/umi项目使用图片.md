### umi项目中使用图片

两种方式：

1. 将图片上传到CDN

2. 通过require导入项目中的静态图片。

```tsx
// 通过require导入
const medal = require("@/assets/img-medal.png");
<img src={medal} alt="" />
<img src={require("@/assets/img-medal.png")} alt="" />
// 通过CDN方式使用
<img src="https://xxxx.com/xxxx/xxxx/n_v30fc3017a261e463f94d7c3937dcce35e.png" alt="" />
```

[umi项目中图片的使用方式可参考](./umi.md)