### 通过vite创建的React18项目配置less

### 一种可能的方式

这种方式可能是在vite早期的时候需要配置，但是现在vite的版本是6.0.1的时候，已经不再需要在vite.config.js中配置了。

之前的已经无从考证，个人认为考证也没有什么意义，我们的目标是能把我们预期的预处理器正常运行即可。

1. 安装less和less-loader依赖

```bash
yarn add --dev less less-loader
# or
npm install less less-loader --save-dev
```

> 经过实践，less和less-loader不是必须安装的依赖，也就是说，less和less-loader可以不用安装了

2. 配置vite.cofnig.ts

```ts
export default defineConfig({
  plugins: [react()],
  // 配置支持less
  css: {
    preprocessorOptions: {
      less: {
        javascriptEnabled: true
      }
    }
  }
})
```

3. 组件中引入less文件

```tsx
import { FC, useEffect, useState } from "react";
import axios from "axios";
import "./index.less"
```

4. 组件中声明class

```tsx
<div className="userList"></div>
```

到此，已经可以在通过vite创建的react18项目中使用less预处理器了。

### 现在已经验证可行的方式

vite6发布了，然后就顺便学习了下，然后在配置预处理器的时候，发现vite已经内置了less、sass的loader,less和sass也已经内置了，不需要做任何配置，直接使用即可。

```tsx
import { memo } from "react";
import "./index.less";

const Header = () => {
    return (
        <>
            <div className="header">Header</div>
            <ul className="menu">
                <li>首页</li>
                <li>列表</li>
            </ul>
        </>
    )
}

export default memo(Header);
```

> 在调试过程中，如果效果没有出来，可以 尝试安装下less、sass依赖

```bash
pnpm install less -D
ppm install sass -D
```