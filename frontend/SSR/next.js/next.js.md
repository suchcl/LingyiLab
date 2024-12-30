### 搭建项目

项目demo地址: [https://gitee.com/ya5969/nextssr](https://gitee.com/ya5969/nextssr)

官方文档: [https://nextjs.org/](https://nextjs.org/)

> 在有语言基础的情况下，尽量看官方文档，因为官方文档是最权威的。翻译的文档，带有译者的一些个人观点，可能不会那么客观，理解起来特别费劲，如果你和译者产生不了共鸣，就有可能会误入歧途。但是Next.js的官方文档呢，确实也不够争气，点哪个哪个不动，使用起来特别不顺手。

在最新的React中(React19)，官方推荐使用社区流行的框架去搭建React应用，然后在下面给出了Next.js的相关介绍，说明React从19开始，将重点放在了对Next.js的支持上，所以如果是搭建React的项目，可以考虑直接上Next.js了。


初始化项目

```bash
npx create-next-app@latest
```

### next.js初步了解

1. 布局文件

next.js有嵌套路由的概念，每个路由、目录都可以有自己的布局文件。

项目的根目录下的laytout.tsx是整个应用的根部剧文件，每个路由的UI结构都共用这个布局文件，布局文件中通过children属性来渲染子路由。

layout.tsx: 布局文件，每个路由下都可以有这么一个布局文件，文件名固定，不可更改。 app目录下的layout.tsx是整个应用的布局文件，是必须的。

template.tsx: 模板文件，每个路由下也可以有这么一个模板文件，文件名固定，不可更改，这个文件是可选的。

layout.tsx是一个服务端组件，该组件不能访问路由名，也不能设置"use client"，否则报错。

2. 集成scss

next.js默认不能使用scss，需要安装依赖，安装依赖之后，即可直接使用。

```bash
npm install sass --save-dev
yarn add sass --dev
pnpm add sass -D
```

包管理器任意，自己习惯即可。

3. 默认的项目目录结构

```markdown
next.js
├─README.md
├─eslint.config.mjs
├─next-env.d.ts
├─next.config.ts
├─package-lock.json
├─package.json
├─pnpm-lock.yaml
├─tsconfig.json
├─src
|  ├─app
|  |  ├─favicon.ico
|  |  ├─globals.css
|  |  ├─layout.tsx
|  |  ├─page.module.css
|  |  ├─page.tsx
|  |  ├─template.tsx
|  |  ├─dashboard
|  |  |     ├─dashboard.module.scss
|  |  |     ├─layout.tsx
|  |  |     ├─page.tsx
|  |  |     ├─settings
|  |  |     |    └page.tsx
├─public
|   ├─file.svg
|   ├─globe.svg
|   ├─next.svg
|   ├─vercel.svg
|   └window.svg
```

上面目录中，dashboard目录是我新增上的，app目录下的template.tsx我新增的，其他的都是默认的。这基本就是一个完整的next.js项目的目录结构。

每个文件的意义，不必赘述。

4. 路由：应用路由和页面路由

<font color="red">到目前为止，我不太理解这2种路由的区别。</font>

不太理解什么算是应用路由，什么算是页面路由。

5. 路由跳转

路由跳转，可分为声明式跳转和编程式跳转。

- 声明式跳转

需要从next.js中导入Link组件

```tsx
<div className={styles.nav}>
    <Link href="/dashboard/settings" className={styles.link}>Settings</Link>
    <Link href="/dashboard/about" className={styles.link}>About</Link>
</div>
```

- 编程式路由跳转

通过useRouter钩子函数实现编程式路由跳转

```tsx
"use client";
import { useRouter } from "next/navigation";

export default function News() {
  const router = useRouter()
  
  const goTech = () => {
    router.push('/tech')
  }
  return (
    <div>
      <button className="btn" onClick={goTech}>科技</button>
    </div>
  )
}
```

6. 设置当前路由激活状态

next.js中提供了usePathname，可以获取当前路由，可以以次来设置当前路由的激活状态。

> next.js的官方文档，没有提供usePathname这个说明，中文的翻译文档有这个说明，可以记录下.虽然文档不同，但是在next.js@15.1.3这个版本中，usePathname这个钩子函数是生效的。

next.js的官方文档:[https://nextjs.org/docs](https://nextjs.org/docs)

next.js的中文参考文档:[https://next.nodejs.cn/docs/app/building-your-application/routing/layouts-and-templates#active-nav-links](https://next.nodejs.cn/docs/app/building-your-application/routing/layouts-and-templates#active-nav-links)

```tsx
"use client";
import Link from "next/link";
import { usePathname } from "next/navigation";
import styles from "./dashboard.module.scss";
import { useState } from "react";

export default function DashBoardlayout({ children }: Readonly<{ children: React.ReactNode}>){
    // usePathname 可以获取当前路径
    const pathname = usePathname();
    const [count,setCount] = useState<number>(0);
    const increment = () => {
        setCount(count + 1);
    }
    return (
        <div className={styles.dashboard}>
            <div className={styles.nav}>
                {/* 通过usePathname与当前路由的相等性判断，来确认是否为当前路由，设置激活标签样式 */}
                <Link href="/dashboard/settings" className={`${styles.link} ${pathname === "/dashboard/settings" ? styles.active : ""}`}>Settings</Link>
                <Link href="/dashboard/about" className={`${styles.link} ${pathname === "/dashboard/about" ? styles.active : ""}`}>About</Link>
            </div>
            <h2>我是dashboard目录的布局文件</h2>
            <div className={styles.count}>
                dashboard中layout中的数字:{count}
            </div>
            <button className={styles.btn} onClick={increment}>increment</button>
            {children}
        </div>
    )
}
```

路由的激活状态，也可以把实现部分模拟下真实环境，因为路由信息，一般都是从接口下发的：

```tsx
const linkData = [
    {
        name: "Settings",
        path: "/dashboard/settings"
    }, {
        name: "About",
        path: "/dashboard/about"
    }
];
// tsx部分
{
    linkData.map( link => (
        <Link key={link.name} href={link.path} className={`${styles.link} ${pathname === link.path ? styles.active : ""}`}>{link.name}</Link>
    ))
}
```

7. 组件：客户端组件和服务器组件

**服务端组件**

**客户端组件**


- 编程式跳转

8. 开发环境下，代码默认执行2次

因为next.js默认开启了react的严格模式，开发环境，函数组件的函数体本身会被调用2次，useEffect和useLayoutEffect的回调函数也会执行2次。

在next.js中关闭react严格模式的方式：reactStrictMode: false

```ts
import type { NextConfig } from "next";

const nextConfig: NextConfig = {
  /* config options here */
  reactStrictMode: false // 关闭react的严格模式
};

export default nextConfig;
```

> 严格模式下的部分代码执行2次，仅存在开发环境，生产环境不会执行2次。开发环境执行2次，是为了发现潜在的风险。

9. 404页面

next.js中有两种模式的404页面：

- 全局的404页面

- 具体路由下的404页面

404页面，在项目中的文件名为not-found.js,该文件为可选，如果没有该文件，next.js会自动使用框架提供的默认的404页面。

自定义的全局404页面，在app目录下

自定义的局部404页面，在具体的路由目录下

```markdown
next.js
├─README.md
├─eslint.config.mjs
├─next-env.d.ts
├─next.config.ts
├─package-lock.json
├─package.json
├─pnpm-lock.yaml
├─tree.md
├─tsconfig.json
├─src
|  ├─data
|  |  └menu.ts
|  ├─components
|  |     ├─TopBar
|  |     |   ├─index.module.scss
|  |     |   └index.tsx
|  |     ├─Header
|  |     |   ├─index.module.scss
|  |     |   └index.tsx
|  |     ├─Footer
|  |     |   ├─index.module.scss
|  |     |   └index.tsx
|  ├─app
|  |  ├─favicon.ico
|  |  ├─globals.css
|  |  ├─layout.tsx
|  |  ├─not-found.tsx
|  |  ├─page.module.css
|  |  ├─page.tsx
|  |  ├─template.tsx
|  |  ├─test
|  |  |  ├─not-found.tsx
|  |  |  └page.tsx
|  |  ├─tech
|  |  |  └page.tsx
|  |  ├─society
|  |  |    └page.tsx
|  |  ├─news
|  |  |  ├─page.tsx
|  |  |  └template.tsx
|  |  ├─finance
|  |  |    └page.tsx
├─public
|   ├─.DS_Store
|   ├─file.svg
|   ├─globe.svg
|   ├─next.svg
|   ├─vercel.svg
|   ├─window.svg
|   ├─images
|   |   └logo.webp
```

<!-- 具体路由下的not-found.tsx 404 -->
```tsx
import { notFound } from "next/navigation";
export default function Test() {
    // 需要主动触发notFount函数，才会渲染当前路由下的404页面
    notFound();
    return (
        <div>
            <h1>我是全局自定义的NotFound!</h1>
        </div>
    )
}
```

10. 路由组

next.js是基于文件系统的路由，即文件夹会被识别为路由。

next.js中有一个路由组的概念，可以添加一层路径，这一层路径还不被识别为路由，就是路由组。

next.js中，将文件夹名用小括号括起来，就是路由组。

一个路由组中，可以laytout.tsx布局文件，也可以有tempalte.tsx模板文件，也可以有not-found.tsx 404页面。

```markdown
app
├─favicon.ico
├─globals.css
├─layout.tsx
├─not-found.tsx
├─page.module.css
├─template.tsx
├─(home)
|   ├─layout.tsx
|   ├─page.tsx
|   ├─test
|   |  ├─not-found.tsx
|   |  └page.tsx
|   ├─tech
|   |  └page.tsx
|   ├─society
|   |    └page.tsx
|   ├─news
|   |  ├─page.tsx
|   |  └template.tsx
|   ├─finance
|   |    └page.tsx
```

app目录中，(home)是一个路由组，该路由组下面有test、tech、society、news、finance这几个路由，这几个路由还是/test、/tech、/society、/news、/finance这几个路由，没有因为新增了(home)路由组而受到影响。

11. 代码部署

如果是个人站点，那么可以部署到vercel.com这个网站上，免费的。

可以通过github.com的账号去登录，然后把自己的项目代码上传到github上，然后在vercel.com上，选择github.com的账号，然后把自己的项目代码上传到vercel.com上，就可以部署了。

项目有了更新以后，只需要将代码推送到github仓库即可，不需要手动重新部署vercel，这一点做的非常不错。

### 常见问题

1. hooks不能在服务器组件中使用

像useState、useEffect等hooks不能直接在服务器组件中使用，这类hooks只能在客户端组件中使用。

当希望在服务端组件中使用如useState、useEffect等hooks时，可以直接在页面顶部添加"use client";这个指令

```tsx
"use client";
import Link from "next/link";
import styles from "./dashboard.module.scss";
import { useState } from "react";

export default function DashBoardlayout({ children }: Readonly<{ children: React.ReactNode}>){

    const [count,setCount] = useState<number>(0);
    const increment = () => {
        setCount(count + 1);
    }
    return (
        <div className={styles.dashboard}>
            <div className={styles.count}>
                dashboard中layout中的数字:{count}
            </div>
            <button className={styles.btn} onClick={increment}>increment</button>
            {children}
        </div>
    )
}
```

页面顶部加上了"use client";指令，就可以在当前这个服务器组件中使用useState、useEffect等hooks了。