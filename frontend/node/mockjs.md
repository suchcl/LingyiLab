### mock.js

[参考文档: http://mockjs.com/](http://mockjs.com/)

mockjs可以模拟一些静态的数据，也可以拦截http请求，去模拟数据。

如果是在某个页面中模拟一些静态数据，就比较简单了。

```tsx
import Mock from "mockjs";

const MockData = () => {
    const username = Mock.mock("@name");

    return (
        <>
            <div>MockData</div>

            {username}
        </>
    );
};

export default MockData;
```

这种比较简单。


### 拦截网络请求

```tsx
import { memo } from "react"
import { useLocation, useSearchParams } from "react-router-dom";
import axios from "axios";
import "@/mock/news.ts";

const List = () => {
    axios.get("/api/newsList").then(res => {
        console.log("mock拦截网络请求");
    });
    
    return (
        <div>List</div>
    )
}

export default memo(List);
```

案例中，import "@/mock/news.ts";模拟数据文件直接导入到了当前页面文件中，也可以导入到整个应用的入口文件中。导入到应用的入口文件，有一个好处，就可以通过全局配置来确认是否都使用Mock来模拟数据来测试。

```tsx
import { StrictMode } from 'react'
import { createRoot } from 'react-dom/client'
import './index.css'
import App from './App.tsx'
import "@/mock/news.ts" // 全局入口中引入mock

createRoot(document.getElementById('root')!).render(
  <StrictMode>
    <App />
  </StrictMode>,
)
```

拦截网络请求，有一个前提条件，就是不能配置正常的接口请求，即便是正常的接口请求是不通的，也不行。

```ts
axios.get("/api/newsList").then(res => {
    console.log("mock拦截网络请求");
});
```

axios请求/api/newsList接口，不能给axios配置baseUrl，也不能写绝对全路径(如https://sssss.com/api/newsList),即使接口请求不通也不行。如果axios配置了baseUrl或者axios的请求url是一个全路径，mock就不能拦截这个请求了，axios就会直接请求这个真实的url了。如果这个真实的url不通，就会返回请求失败的逻辑。