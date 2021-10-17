### vue为什么采用异步渲染？

这有很好的解释：用来学习吧：https://github.com/WindrunnerMax/EveryDay/blob/master/Vue/Vue%E4%B8%BA%E4%BD%95%E9%87%87%E7%94%A8%E5%BC%82%E6%AD%A5%E6%B8%B2%E6%9F%93.md

但是本质上的原因，就是为了提升性能。因为如果不采用异步更新、渲染的策略，每次有了数据的更新后，都对DOM进行重绘，性能上差、使用体感上也会差很很多。