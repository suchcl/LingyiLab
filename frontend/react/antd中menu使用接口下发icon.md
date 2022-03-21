### antd怎么使用服务端下发的icon图标？

如果是菜单比较少，且是静态的，那么就比较好实现了，没有讨论的价值。这里主要讨论的是菜单是服务端下发的，服务端下发的菜单中有一个icon的字段，如：

```ts
[
  {
    "id": 1,
    "path": "/orderList",
    "text": "订单列表",
    "icon": "BarChartOutlined"
  },
  {
    "id": 2,
    "path": "/report",
    "text": "商品管理",
    "icon": "CameraOutlined"
  }
]
```

菜单的名称和图标，都是服务端下发，如果直接给菜单的icon属性赋值如：

```tsx
<Menu.Item key={item.path} icon={item.icon}>
    <Link to={item.path}>{item.text}</Link>
</Menu.Item>
```

是不可以的，因为根据Menu.Item的API，icon的属性值是ReactNode类型，而上面我们的赋值是字符串型的。那怎么办呢？

### 动态创建ReactNode

因为菜单中的icon属性值是ReactNode类型，可我们从接口获取到的是一个字符串类型值，那么没有办法，就根据这个字符串类型来创建一个ReactNode吧。

> 注意：从接口获取到的这个icon字段，就是预定义好的icon标签。

> 假设我们我们都是使用的ant的预设的图标

实现动态创建菜单icon的步骤：

1. 导入icon图标库

```tsx
import * as Icon from "@ant-design/icons"; // 这里我选择了全部导入了，如果我们已经确定了使用的icon，也可以导入指定的icon
```

2. 编写创建ReactNode的的方法

```tsx
// 创建icon图标元素
const iconToElement = (name: string) =>
    React.createElement(Icon && (Icon as any)[name], {
        style: { fontSize: '16px' }
    })
```

3. 在菜单中使用

```tsx
<Menu.Item key={item.path} icon={item.icon ? iconToElement(item.icon) : ""}>
    <Link to={item.path}>{item.text}</Link>
</Menu.Item>
```

贴一下全部的代码：

```tsx
import React, { FC, useEffect, useState } from 'react';
import { Layout, Menu } from "antd";
import * as Icon from "@ant-design/icons";
const { Header, Content, Footer, Sider } = Layout;
const { SubMenu } = Menu;
import request from 'umi-request';
import logo from "../../assets/images/logo.png";
import style from "./less/layout2.less";
import { Link } from 'umi';


const MainLayout: FC = (props) => {
    const [menu, setMenu] = useState([]);
    const [defaultOpenKey, setDefaultOpenKey] = useState([]);
    const getMenu = () => {
        request.get("http://localhost:3000/menu").then(function (res) {
            setDefaultOpenKey(res.defaultOpenKey);
            setMenu(res.data);
        }).catch(err => {
            console.log(err);
        })
    }
    useEffect(() => {
        getMenu();
    }, []);

    // 创建icon图标元素
    const iconToElement = (name: string) =>
        React.createElement(Icon && (Icon as any)[name], {
            style: { fontSize: '16px' }
        })

    return <div>
        <Layout>
            <Header className={style.header}>
                <div className={style.logo}>
                    <img src={logo} alt="logo" />
                </div>
            </Header>
            <Layout>
                <Sider width={200} className="site-layout-background" theme="light">
                    <Menu mode='inline' defaultSelectedKeys={defaultOpenKey} defaultOpenKeys={defaultOpenKey} theme="light">
                        {
                            menu.map((item: any) => {
                                if (item.children && item.children.length > 0) {
                                    return <SubMenu key={item.path} title={item.text} icon={item.icon ? iconToElement(item.icon) : ""}>
                                        {
                                            item.children.map((citem: any) => {
                                                return <Menu.Item key={citem.path} icon={citem.icon ? iconToElement(citem.icon) : ""}>
                                                    <Link to={citem.path}>{citem.text}</Link>
                                                </Menu.Item>
                                            })
                                        }
                                    </SubMenu>
                                } else {
                                    return (<Menu.Item key={item.path} icon={item.icon ? iconToElement(item.icon) : ""}>
                                        <Link to={item.path}>{item.text}</Link>
                                    </Menu.Item>
                                    )
                                }
                            })
                        }
                    </Menu>
                </Sider>
                <Layout className={style.maincontentWraper}>
                    <Content className={style.maincontent} style={{ minHeight: '90vh' }}>
                        {props.children}
                    </Content>
                </Layout>
            </Layout>
        </Layout>
    </div>
}
export default MainLayout;
```