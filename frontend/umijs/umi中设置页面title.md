### 设置页面title

有两种场景设置页面title

1. 获取路由信息，设置页面title

这种情况，需要在路由信息中设置title字段信息，当作当前路由组件的title，然后还需要在运行时配置文件src/app.tsx中做一个简单的配置

> umi中，约定src/app.tsx为运行时配置文件，不需要额外配置

路由配置信息，添加title字段

```ts
routes: [
    {
        path: 'orderList',
        component: '@/pages/orderList',
        title: '订单列表'
    },
]
```

在运行时配置文件src/app.tsx中配置路由变化信息处理

```tsx
export function onRouteChange({ matchedRoutes }: any) {
    if (matchedRoutes.length) {
        document.title = matchedRoutes[matchedRoutes.length - 1].route.title || '';
    }
}
```

经过2步简单的配置，就可以设置路由组件的页面title了

2. 到某个页面中，根据当前页面信息设置当前页面的title

根据当前页面差异化配置当前页面的title，可以使用Helmet组件，Helmet是umi的一个内置组件

```tsx
// 导入Helmet组件
import { Helmet } from 'umi';

const View: FC = () => {
    const [title, setTitle] = useState("xxxxx信息");
    return (
        <>
            <Helmet>
                <title>{title}</title>
            </Helmet>
            <h3>xxxxx</h3>
        </>
    );
};

export default View;
```

这样，就可以实现或者从接口获取title信息，或者从前一个页面中传递过来的title信息，也或者当前页面设置固定的title信息等多种差异化需求了。

> 如果当前页面既是路由组件，也使用了Helmet组件，那么Helmet的优先级高于路由设置的title。