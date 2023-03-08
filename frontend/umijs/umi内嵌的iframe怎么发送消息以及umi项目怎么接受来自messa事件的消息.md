### umi项目中内嵌的iframe怎么在页面加载时postMessage消息

在现在的一些前端项目中，虽然有了微前端，但还是有可能会用到iframe。下面我们就简单说下umi项目中内嵌的iframe页面怎么postMessage消息。

很多时候，主项目都需要向嵌入的iframe页面传递一些消息，被嵌入的页面根据主页面传递过来的信息做一些业务上的处理，这种场景下，主应用一般都是通过postMessage这个API去发送消息的，这也是原生支持的，不存在什么兼容性的问题，一般主流浏览器都能支持。

看案例：

```tsx
import { FC, memo, useEffect, useRef, useState } from 'react';

interface PageProps {}
const Index: FC<PageProps> = (props) => {
  const [token, setToken] = useState<string>("");
  const frameRef = useRef(null);
  const [frameUrl, setFrameUrl] = useState<string>('');
  useEffect(() => {
    const iframe = frameRef.current;
    iframe!.onload = () => {
      frameRef.current!.contentWindow.postMessage(
        {
          name: 'Nicholas Zakas',
          age: 12,
          token,
        },
        frameUrl,
      );
    };
  }, []);
  return (
    <>
      {token && (
        <iframe src={frameUrl} ref={frameRef} width="100%" height="100%" style={{ border: 0 }} ></iframe>
      )}
    </>
  );
};

export default memo(Index);
```

一个简单的嵌入iframe并发送消息的页面，基本可以实现了。

### umi项目怎么接收其他项目通过postMessage()方法传递过来的消息呢

可以在umi项目加载的时候监听message事件，这个事件可以在项目的全局文件中去监听。

src/globa.ts是umi项目的全局文件。

```ts
window.addEventListener("message", receiveMessage, false);

function receiveMessage(e: any) {
    const { origin,data } = e;
    if (origin === "http://localhost:8000") {
        console.log("event333:", e);
        console.log('data:', data);
    }
}
```

参数e中包含了很多有价值的信息，其中最为关键的我使用到了origin和data这2个参数，origin记录了事件的来源，data为来源页面传递过来的数据。参数e的具体参数信息，可参考如下:

[message事件的参数信息](./images/i15.png)