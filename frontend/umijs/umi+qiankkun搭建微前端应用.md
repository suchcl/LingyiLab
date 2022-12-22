### umi+qiankun搭建微前端应用

微前端应用，我了解过的有MicroApp(https://micro-zoe.github.io/micro-app/)和qiankun(https://qiankun.umijs.org/zh/guide),不过以前都是简单的了解过，由于实际项目并没有这个诉求，也就没有深入调研实践过，仅仅简单的了解了下。

MicroApp和qiankun的一个最外在的区别，就是基座应用。

由于是很早之前看的，现在先简单的说下，以后补充个确认的结论。印象中，MicroApp，需要搭建一个基座应用，这个基座应用，就是纯粹的基座应用，不做别的用途；其他应用，即需要嵌入到这个基座应用的那些应用都作为这个应用的子应用，这些子应用地位平等，不存在主从的关系。而在qiankun中，不需要搭建这么一个纯粹的基座应用。qiankun的思想，是选择一个主应用(逻辑上的主应用吧，理论上哪个应用都可以)作为前端应用的基座应用，其他应用作为子应用接入。

<font color="#f20">这是我大概的一个印象，接下来我补充确切的文档说明。</font>

关于MicroApp，可以参考：[MicroApp](../%E6%9E%B6%E6%9E%84%E4%B8%8E%E8%AE%BE%E8%AE%A1/%E5%BE%AE%E5%89%8D%E7%AB%AF.md)

关于qiankun，可以参考[qiankun](../%E6%9E%B6%E6%9E%84%E4%B8%8E%E8%AE%BE%E8%AE%A1/qiankun.md)
