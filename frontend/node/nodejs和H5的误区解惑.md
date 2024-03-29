## Node.js和H5的误区解析

### Node.js的误区

1. Node.js作为一门新兴的开发语言,具有跨平台、模块化、生态丰富等的众多优势,在前端领域得到了广泛的应用;

2. Node.js是一个功能强大的前端开发框架,能够满足各种类型应用的开发.

这是很多业内人士的认知,在日常的工作交流中以及在留存的文档中也是这样记录并传播,那么这两种认知是否准确呢?我们去查询node.js文档,从根源上、从基础认知上去剖析node.js,从而让我们更加清晰的去认识node.js,去使用node.js.

### Node.js是什么?

我们打开官网首页,首页正文的第一句话,就对node.js做了一个阐述:Node.js is an open-source,cross-platform Javascript runtime environment,就是说Node.js是一个开源的、跨平台的jascript的运行时环境.

简单分析一下,Node.js是一个开源的、跨平台的、构建在Chrome V8 Javascript引擎之上的Javascript运行时环境,提供了一组用于处理文件系统、网络请求、操作系统APId内置库,采用事件驱动、非阻塞式的I/O模型,它实现了开发者可以使用javascript开发语言来开发服务器端应用和命令行工具.与传统的运行在浏览器的javascript不同,Nodejs可以在服务器端运行javascript代码,基于此,Nodejs被广泛的应用于构建高性能、可扩展的网络应用和后端服务,使得它在处理高并发请求时有出色的表现.

### Node.js有什么特点及优势

1. 跨平台:可以在不同的平台系统上运行,可以运行在window上,也可以运行在Mac和linux上,具备跨平台的开发和部署能力;

2. 开源:使用成本低,切功能灵活,开发者可以根据实际需要去扩展、改善功能,使用起来更加灵活;

3. 模块化:Node.js提供了三种类型的模块化能力,包括Node.js内置的模块、第三方模块以及开发者自定义的模块,功能强大的模块化系统,构建了庞大的生态系统,使得开发人员能够快速集成和使用各种功能和工具;

4. 单线程非阻塞式I/O模型:Node.js使用的非阻塞式、事件驱动的I/O模型,使得它能够处理大量的并发请求,高效的执行I/O操作,且不会因此造成阻塞而引起资源的浪费;

5. 强大的包管理器,丰富的包:Node.js通过NPM构建了一个庞大的开源的生态系统,拥有丰富的第三方模块和库,使得开发者在满足某些功能开发的同时,还可以快速的扩展到其他应用;

6. 支持命令行工具开发:Node.js可以用来开发命令行工具和脚本,提供了对文件系统、进程管理等底层操作的支持,使得开发者能够轻松的构建自定义的命令行工具,对前端开发者尤其友好;

7. 采用javascript作为开发语言:开发者在前端和服务端使用统一的开发语言和开发工具,可以大大的提高代码的复用率,同时也可以推动node.js生态的发展;


Node.js的这些特点、优势,都是其他开发环境不具备的,使它可以构建高性能、高可扩展的网络应用程序,尤其是它采用的事件驱动和非阻塞式I/O模型,能够处理大量并发请求、高效处理I/O操作;

### Node.js的弊端

单线程应该就是Node.js最大的弊端了.正是因为其单线程,导致其可靠性低、资源利用率低,所以它在处理计算密集型的任务方面的时候性能表现相对较弱.在这种情况下,传统的多线程开发语言如Java、C++等可能更加合适.虽然有这个不足,但是Nodejs也可以通过将计算任务委托给子进程或者利用Nodejs的集群模块来解决这个问题;

另外,精通于Node.js专业的人才偏少,也应该算是一个弊端吧,也在一定程度上阻塞了Node.js的发展和推广应用.

### Node.js适合做哪些类型的应用?

基于Node.js的一些特点,那么它适合做哪些类型的应用呢?

1. API服务:Node.js的轻量级和高并发处理的特性,可以用来构建web应用服务的API;

2. 命令行工具:基于Node.js提供的命令行工具开发能力,可以使用Node.js构建自定义的命令行工具和脚本,可用于自动化任务、文件操作和版本控制等等,现在前端工程中的各种cli工具,基本都可以实现;

3. 实时应用:基于Node.js的事件驱动和非阻塞式I/O模型的优势,可以用来构建实时应用,如实时的聊天工具、实时协作工具、实时通知服务等;

4. 信息展示类的web应用:由于这类应用具有访问量大但计算少的特性,正是Node.js的优势所在.


### Node.js是一个能够满足构建多种应用场景的优秀前端开发框架或者前端库吗?

开发框架和库是软件开发中常见的概念,它们在设计和功能上有所区别:

#### 开发框架

**开发框架**是一种提供了一整套结构和结构和规范的软件工具集合,用于帮助开发人员构建应用程序.开发框架通常提供了一个基础架构,定义了应用程序的结构、组织和工作流程,开发人员按其约束和规则进行开发即可.框架一般都会包含一些工具库和开发规范的约定,并提供一定的基础功能让项目快速运行起来.

**开发框架的一些特点和优势**

- 提供基本的应用程序结构和组织方式

- 定义通用的编码规范和最佳实践

- 提供基本的功能库和工具,用于快速处理常见的任务和功能

- 提供抽象层和接口,使得复杂功能简单化

- 通常会包含一套测试和调试工具

**常见的前端开发框架**

在前端开发领域中,常见、常用且比较流行的开发框架有exprss、Koa、nest、umi、Vue、Angular等.

> React暂且不算是开发框架,后文介绍

#### 库

库,是一组可充用的代码集合,常用于解决特定的问题或提供特定的功能.库通常是独立的,开发人员可以根据需要有选择性的使用它们,也可以有选择性的不使用它们.库大多数情况下是通过提供函数、类或模块的方式供调用方在自己的项目中特定的地方去调用这些能力去完成一些特定的功能.

库的主要特点有:

- 提供特定的功能函数、类或者模块

- 可以被导入到应用程序中被使用

- 通常具有很高的可定制性和扩展性,允许开发人员根据实际需要进行能力的扩展和配置

- 具备良好甚至是优秀的文档

前端开发领域比较常用的一些库有axios、lodash、dayjs、momentjs、redux、mobx、React、React Router、jQuery等等.

> Reac是一个库,而没有被归为框架.

#### 框架和库的区别

- 依赖关系:开发框架通常会包含、依赖于很多的库和工具,整合到一起完成并提供完整的开发环境、制定约束.库则是可以独立使用的,一般情况下是不依赖于其他的组件或者库的.

- 控制权:一般情况下,开发框架都会对应用程序的结构和工作流程有着绝对的控制权,开发者需要遵循框架规定的约束和规范去实现功能.但是库一般不会,也不能去控制程序的结构或者工作流程,它仅仅是实现某个功能的一个方法而已.

总的来说,框架是在控制着开发者可以做什么,不可以做什么;库,是开发者控制着它什么时候被调用,让它去帮助我们快速实现某个功能.

**React为什么是一个库而不是一个框架呢?**

React官网已经明确了,React是一个用于构建用户界面的javascript库,专注于视图层的开发.React提供了一种声明式的编程模型,通过使用组件化的方式构建用户界面,提供了一些核心的功能,如虚拟DOM、组件化开发、单向数据流等,但是没有提供完整的应用程序的架构和规范.为了构建完整的React应用,需要结合其他的库和工具,如React Router、Redux等,React通过和这些工具一起配合使用,去构建大型、复杂的web应用.

Vue和React相比,提供了更多的核心功能,如数据绑定、虚拟DOM、组件化开发、路由管理、状态管理,同时Vue也提供了一套完整的规范和生态系统,包括官方的插件和工具,以及许多的第三方扩展库.Vue提供了整套的结构和约定,所以Vue是一个框架,而不仅仅是一个库.

### H5的不同观点

H5就是手机上的网页,手机上看的网页就是H5;

严谨的说,H5是指HTML5(HyperText Markup Language 5),是HTML的第5个主要版本.HTML5中引入了许多新的特性和功能,旨在提供更强大、更丰富的网页和应用程序开发能力.

坊间也有一种观点,指用HTML5语言制作的一切数字产品,那么这个范围的H5就不仅仅指移动端的网页了,也包括了PC端上使用了HTML5技术的网页(那就几乎可以说是现在所有的web应用都是H5了).

也有一种观点是效果酷炫的移动页面,也有把凡是在移动设备上的页面都被称为了H5.

那么H5究竟是什么,什么是H5,没有一个统一的、权威的概念和定义.但可以确定的是,无论是哪个版本的H5,都是其背后的强大的技术支撑,简单的H5背后的强大的能力支撑是最重要的.

### 小结

通过我们对一些基础概念的分析,应该可以得出这样的结论:

1. nodejs不是一门新兴的开发语言,因为它就不是一门语言,它是一个可以为javascript这门语言运行的环境,仅此而已;

2. nodejs也不是一个开发框架,因为它不给我们提供一个开发框架具备的任何一个能力;

3. H5,可以说除了HTML5这个标准外,其他的是没有统一的认知,所以在说到H5相关的事情时,一定要谨慎对待;

科学技术的不断发展和应用推动了社会的进步和发展,改善了人们的生活质量,提高了工作效率,促进了经济的发展.作为一名开发技术人员,也要时刻保持对技术的敬畏和渴望的精神,严谨的对待技术的发展,保持对知识的渴望,也做好布道、授业、解惑的这一社会责任.