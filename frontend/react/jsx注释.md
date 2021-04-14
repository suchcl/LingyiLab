jsx的注释，和其他类型文件的注释大同小异，基本相同，如在js中的单行注释和多行注释方法，但由于jsx的特殊性，所以在注释上也有些特别的地方.

在一个react类型的javascript文件中，DOM之外部分的注释方式，和js的注释方法相同，有单行注释和块注释两种方式：

```javascript
/*这是js文件中的注释，在jsx中也是正常的*/
export default function house_detail() {
    return (
        /**
         * name：hosueDetail.js
         * author：xxx
         * date: 2021-12-12
         * description: 这是在jsx部分DOM元素之外的部分，注释方式和js文件的注释方式完全相同，同样支持块注释和行注释，参考下面一行
         */
        // 这也是合法的注释
        <div className="house-detail">
            
        </div>
    );
}
```

jsx中DOM元素中的注释，和普通的js注释有些区别，需要将注释包裹在一堆大括号({})中。

```javascript
/*这是js注释*/
export default function house_detail() {
    return (
        <div className="house-detail">
            <ul className="nav">
                {/*这里是正确的jsx注释*/}
                <li><Link href="/"><a>Link去首页</a></Link></li>
                <li>
                    <Link href="/list/houseList"><a>Link去楼盘列表页</a></Link>
                </li>
                <li>
                    <Link href="https://www.baidu.com" className="link">
                        <a target="_blank" className="link-a">测试新标签打开</a>
                    </Link>
                </li>
            </ul>
        </div>
    );
}
```

jsx中的注释，就是这么简单。