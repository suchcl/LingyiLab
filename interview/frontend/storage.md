### cookie、sessionStorage、localStorage的区别

cookie是在HTML4标准中提出来让客户端保存数据的，可以自动和服务端通过http请求进行数据通信，和session配合使用实现跟踪浏览器用户身份，如前几年常用的登录状态保持，就是通过cookie、session配合使用实现的，而webstorage（包括了sessionStorage和localStorage）是在HTML5标准中提出来的，就是为了保存数据，不会和服务端进行数据的通信。WebStorage的2个主要目标：

1. 提供一种在cookie之外的客户端存储机制；

2. 提供一种可以存储大数据量的客户端存储机制；

<b>相同点：</b>

cookie、localStorage、sessionStorage都是客户端的存储机制，也都存储相同的数据类型：字符串。

<b>不同点</b>

1. 生命周期
   
   cookie可以设置声明时效，那么它的生命周期就是它设置的时效到期前，时效到期了，cookie也就自动消失了；如果没有设置时效，那么cookie就是临时存储在内存中，临时存储，那么它是会话级别的，会话结束后，cookie也是就自动消失了；

   localStorage是没有生命周期的概念的，它是存储在本地磁盘中的，除非清理磁盘、或者根据需要主动删除，否则localStorage是永久有效的。localStorage和浏览器没有关系，无论是关闭浏览器或者是卸载浏览器、还是会话结束，localStorage都不会消失；

   sessionStorage仅在当前会话下有效。sessionStorage引入了一个“浏览器窗口”的概念，sessionStorage是在同源窗口中始终存在数据，只要这个窗口没有关闭，哪怕刷新页面了或者进入了同源的另一个新的页面，sessionStorage也是依旧存在；<font color="#f20">但是如果页面跳转到了其他的窗口，无论是否在同一个域下，之前的sessionStorage都会消失</font>。

   > 总结一下，就是sessionStorage就是在当前窗口（浏览器中的一个页签）下的同一个域下有效，窗口关闭，sessionStorage消失；同一个浏览器，新窗口（新的浏览器页签）打开的页面，也获取不到前一个页面中的sessionStorage。

   localStorage和sessionStorage的区别：二者都是HTMl5标准提出来的新的客户端存储方案，但是localStorage是一种客户端持久化的存储机制，而sessionStorage是一种非持久化的客户端存储机制。

2. 网络请求（网络流量消耗）

   cookie每次都会随着http请求自动和服务器进行数据通信，webStorage(一般情况下说的webStorage都是指的localStorage和sessionStorage)不会主动和服务端进行数据通信，其目标就是为了客户端的本地存储。所以从这个角度来说，使用cookie会消耗一定的网络流量，而webStorage不会消耗网络流量，我们可以根据实际的业务场景选择使用合适的客户端存储技术。比如在校验客户端身份的合法校验的时候，就比较适合使用cookie，因为校验身份一般会通过token，针对每个接口去校验。

3. 大小限制

    cookie的大小限制，大概在4K左右，非常小，所以cookie不适合存储质量较大的数据。webStorage可以存储的数据就相对大一些，一般为5M，但这个值不是绝对的。5M指的是在同一个域下的容量大小，我们也可以通过一些技术手段来扩充容量。

4. 安全性

    cookie会自动随着http请求和服务端进行数据通信，webStorage不会随着http请求自动和服务端进行数据通信，所以在安全性上来说，webStorage不用担心我本地存储的数据会在网络进行过程中被恶意劫持，安全性相对高一些。

5. 使用便利性上
   
   webStorage提供了一些常用、原生的方法，使用非常方便，且localStorage和sessionStorage是原生对象，可以直接使用；cookie没有提供可直接操作cookie的方法，使用便利性上差了一点；

   webStorage的常用方法：

   ```javascript
    setItem(key,value);  // 保存数据
    getItem(key); // 获取数据
    removeItem(key); // 删除数据
    clear(); // 清理所有数据
    key(index); // 获取某个索引的key
   ```

### cookie的弊端

通过上面部分的学习，我们了解了cookie提供了在客户端持久化存储的功能，部分场景下减轻了服务器的存储压力，但是也存在一些不足的地方：

1. 每个特定的域名下最多只能生成20个cookie；

2. IE6或更低版本的浏览器最多能生成20个cookie：但是现在基本不用考虑了，IE6、IE7这些浏览器基本上不会再继续使用了；

3. IE7开始之后的几个IE版本的浏览器可以存储50个cookie，在数量做了很大的提升：现在也基本不需要考虑IE7了，IE浏览器的市占率已经很低了；

4. Firefox可以最多生成50个cookie：到这里已经可以发现，不管是早期的IE6及更早的版本，以及从IE7开始和Firefox，最多只能生成50个cookie，对数量有严格的限制，要求我们在做技术方案的时候，就不能滥用cookie；

5. chrome和safari没有做cookie数量上的限制：chrome和safari是W3C标准实现的比较接近的浏览器，对于cookie的处理，也是人性化了许多，减少了一些限制；

6. IE和Opera具备自动清理cookie的功能，IE会清理近期使用频率低的cookie，Opera会随机清理：虽然浏览器提供的自动清理功能能够让我们使用更多的cookie，但是总会被清理掉不希望被清理的数据，体验不够友好；

7. 容量小：cookie最多可以存储4K的数据，4096个字节，在实际操作的时候，一般最大设置为不超过4095个字节；

8. 安全性上的问题：cookie会自动跟随HTTP氢气和服务端做数据通信，如果在这个过程中被恶意拦截了，就可以通过非法手段获取到服务器上的session信息，具有一定的安全风险；