### 通过vite创建的React18项目配置less

1. 安装less和less-loader依赖

```bash
yarn add --dev less less-loader
# or
npm install less less-loader --save-dev
```

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