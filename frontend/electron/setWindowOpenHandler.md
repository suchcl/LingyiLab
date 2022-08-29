### 新窗口打开事件监听

在electron应用中，以前在监听新窗口打开事件，是通过new-window事件来监听的，现在new-window事件已经被废弃了，不再推荐使用了，而是推荐使用setWindowOpenHandler这个实例方法，这个是WebContents类的实例，而WebContents类是BrowserWindow和BrowserView类的实例属性，所以BrowserWindow和BrowserView的实例都可以调用setWindowOpenHandler这个实例方法。

根据文档，setWindowOpenHandler方法的参数是一个函数，函数参数是一个对象，参数类型需要特别注意，我第一次在使用的时候，没有注意参数类型，就导致用错参数的情况。

一个使用案例：

```js
win.webContents.setWindowOpenHandler(({url}) => {
    const view = new BrowserView();
    win.setBrowserView(view);
    const [winWidth,winHeight] = win.getContentSize();
    view.setBounds({
        x: 0,
        y: 34,
        width: winWidth,
        height: winHeight
    });
    view.webContents.loadFile(url);
    return {
        action: "deny"
    }
});
```

最终需要注意的是setWindowOpenHandler方法的返回值，返回值是一个包含有action属性的对象，该属性值常用2个值：allow和deny。deny:表示拒绝创建新的窗口，allow表示允许创建新的窗口。

在返回值为deny的时候，常用于使用使用BrowserView创建多标签页的时候使用。因为创建多标签页，就不再允许创建新的窗口，就会返回deny，拒绝创建新的窗口，而是仅仅创建一个新的view即可。

setWindowOpenHandler还有其他的几个属性，不再向西介绍，个人认为有了url，是否创建新窗口需要特别注意一下，稍作提示而已。