<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [umijs项目中的文件命名使用小驼峰的命名方式](#umijs%E9%A1%B9%E7%9B%AE%E4%B8%AD%E7%9A%84%E6%96%87%E4%BB%B6%E5%91%BD%E5%90%8D%E4%BD%BF%E7%94%A8%E5%B0%8F%E9%A9%BC%E5%B3%B0%E7%9A%84%E5%91%BD%E5%90%8D%E6%96%B9%E5%BC%8F)
- [umijs项目中组件的导入和文件名有关系吗？](#umijs%E9%A1%B9%E7%9B%AE%E4%B8%AD%E7%BB%84%E4%BB%B6%E7%9A%84%E5%AF%BC%E5%85%A5%E5%92%8C%E6%96%87%E4%BB%B6%E5%90%8D%E6%9C%89%E5%85%B3%E7%B3%BB%E5%90%97)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

### umijs项目中的文件命名使用小驼峰的命名方式

<font color="#f20">umijs项目中的文件命名，采用小驼峰的命名方式</font>，否则热更新可能会失效。

今天在一个umi项目中新增了一个文件，配置好了路由，结果在更新了文件内容的时候，发现只有第一次更新文件会热更新，再次编辑文件的时候，热更新就不再生效了，但是能够监听到文件的变化。

我的环境：

```markdown
系统：MacBook Pro，M1
umijs版本：^3.5.21
nodejs版本：v14.19.2
```

### umijs项目中组件的导入和文件名有关系吗？

关系是一定有的。但是组件名，不一定是文件名，文件名和组件名没有必然的关系。

一个文件中，可以有多个组件，也可以只有一个组件。导入、导出，是从一个文件中导入、导出。

```tsx
import UserInfo from '../components/user';
```

如demo，表示从user.tsx文件中导入了UserInfo组件，当然了，user.tsx文件中，还可能有其他的组件，只是这里只导入了一个UserInfo组件。

```tsx
import { UserProfile } from '../components/user';
```

如这里，user.tsx文件中又新增了一个组件UserProfile。当然了，一个文件中有了多个组件以后，只能有一个组件通过export default的方式导出，所以这里组件的导出方式要遵循import/export规则，在组件导入的时候，是通过{}的方式导入的。

> 所以，在umijs中，文件名使用小驼峰的命名方式；文件和组件以及文件名和组件名之间，没有必然的关系。

> 这里说的文件名使用小驼峰的命名方式，应该也是可以通过配置的方式不必去遵循这个规则，但是无论配置多少都是需要配置，倒不如直接记住一个规则，简单省事。