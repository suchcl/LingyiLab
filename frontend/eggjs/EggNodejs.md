### 异步编程模型

我们都知道Nodejs是一个异步的世界，Nodejs中的API都是以函数回调的形式的编程模型，这种编程模型在一些场景中简化了思考逻辑，但是也给我们带来了很多的问题，如：

回调地域：部分场景需要回调的多层次嵌套

异步函数中的同步调用：部分的异步函数中有时会有同步调用，但是由于js中的事件机制，包裹函数异步回调和被包裹的同步函数不能确定是谁被先执行，带来数据的不一致性；

虽然nodejs有各种由于异步编程带来的问题，但是好在现在有了优秀的解决方案-promise，而且promise还被列入到web标准，成为统一、标准的解决方案。在promise的基础上，结合Generator提供的切换上下文能力，出现了如co等第三方类库让我们用同步的方式编写异步代码，同时，async function这个标准统一方案已在ES2017中实现，并在Nodejs8中实现了；
