### FingerprintJS，跨浏览器指纹识别库

FingerprintJS是一个用于设备指纹识别的开源Javascript库。它通过收集用户设备的多种属性，生成一个唯一的标识，用于识别和跟踪用户。该库主要用于防治欺诈、改善安全性以及个性化用户体验。

**工作原理**

FingerprintJS通过收集浏览器信息、设备信息、屏幕分辨率、操作系统、字体、插件等多个参数，结合这些数据生成一个哈希值。这个哈希值在不同的访问中保持相对稳定，即使用户清除了浏览器的缓存或更改了某些设置。

**特点**

1. 高准确性

- 通过多个参数组合，FingerprintJS提供较高的识别准确性，减少识别误差。

2. 隐私保护

- 尽管它生成唯一标识，但并不会收集个人身份信息，从而在一定程度上保护用户隐私。

3. 易于集成

- FingerprintJS提供较为简单的API，易于与现有系统集成。

4. 开源和社区支持

- 作为开源项目，用户可以根据需要定制，并受益于社区的支持与贡献。

5. 跨平台支持

- 兼容多种浏览器和设备，确保用户体验的一致性。

### 使用方式

1. 安装fingerprintjs

有两种安装方式，一种是通过npm等包管理工具安装，一种是通过cdn的方式以script标签的形式引入

- 通过npm等包管理工具安装

```bash
npm install @fingerprintjs/fingerprintjs
```

- 通过script标签引入

```html
<script src="https://cdn.jsdelivr.net/npm/@fingerprintjs/fingerprintjs@latest/dist/fp.min.js"></script>
```

2. 基本用法

- npm方式

```tsx
import FingerprintJSfrom from "@fingerprintjs/fingerprintjs";
// 通过IIFE的方式获取设备指纹
(async () => {
    // 设置指纹
    const fp = await FingerprintJSfrom.load();
    const result = await fp.get();
    const visitorId = result.visitorId;
    console.log('%c [ visitorId ]-11', 'font-size:13px; background:pink; color:#bf2c9f;', visitorId);
})();
```

- cdn方式

CDN的方式，也需要使用IIFE的方式获取

```html
<script src="https://cdn.jsdelivr.net/npm/@fingerprintjs/fingerprintjs@latest/dist/fp.min.js"></script>
<script>
    (async () => {
        const fp = await FingerprintJS.load();
        const result = await fp.get();
        const visitorId = await result.visitorId;
        console.log('%c [ visitorId ]-13', 'font-size:13px; background:pink; color:#bf2c9f;', visitorId);
    })();
</script>
```

> 正常情况下，应该是这种使用方式，但是由于网络原因，CDN的方式暂时没有办法测试，还没有验证其通顺性。

