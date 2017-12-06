# LittleReact
LittleReact说明：

2017-12-6更新：

其实当时写这个博客的本意是为了找工作方便，显摆显摆自己；不过这么长时间竟然有好多人看过，还有几个小伙伴给我的github几个start，心中甚是惶恐，担心误人子弟，便再更新自己的一些看法。

 

写此文时是年初 当时为了换个好工作 未免有些急功近利 只求快 未曾细细品味~如今看来当时的我无非就是一个看了几本书就觉得自己挺牛逼的二货而已；

而今马上就是18年了，真是一入江湖岁月催啊~

 

言归正传：其实当时我的水准应当还算可以~毕竟看了很多很多书~  不过对React的理解还是有些勉强了，当时写这个LittleReact算是照猫画虎吧，跟着断点一点一点写下来了的，所以只是描摹了一些，很多地方都没有思考过；

虽然努力不会白费，但这样写一遍下来对React的理解我估计撑死也就三成；

 

所以此处分两种情况吧：如果你跟当初的我一样急着提升自己，急着换个好工作，那说说我的经历：当时我要面高级前端，2月份去了几家公司都被人家鄙视了~说我基础不扎实~没办法~每被鄙视一次就把JavaScript高级程序设计再看一遍，经典确实

是经典每次看都能有新的收获，看了三四遍之后（我可是看的很认真的骚年~你也别偷懒~），再去面试就是我鄙视他们了~ 接着再问React~那时还是理解的不够透彻，老办法一遍一遍的看 深入React技术栈这本书（和React源码），也是受益匪浅~再之后面试就过了，这个过程得花费了我四五个月吧，甚是惭愧；如果你跟我当时境况相似，骚年，迷茫，自我怀疑，痛苦都会有的不过持续的努力这些都会过去的，过去之后再回头看，当时大破天的绝望也不过尔尔~希望你能坚持骚年；

 

另外一种情况：你工作比较稳定，没那么着急~那就这么来：真正的自己实现一个React，先学会karma  rollup这两个工具karma是用来做单元测试的，rollup是用来打包代码的；把preact(迷你版react),react,anu(司徒正美先生写的一个类react框架很棒的),下载到自己本地，react的单元测试是用的facebook自己的jest先不用管~，先看preact这个库比较简单，然后自己一点点写，写一部分然后就跑跑单元测试（单元测试这个三个框架都有，自己一点一点写相似的单元测试）；过程中一定要自己写，把React对应的api当成黑盒子自己

实现自己的逻辑，实在不知道怎么写再看看别人怎么写的，这个过程会比较漫长，不过你肯定会收获满满~我现在就在这么做~在这给你安利下我的  MayReact    https://github.com/sven36/MayReact

最后的效果就是你会写一个能在生产环境使用的React~因为你最终会把所有的单元测试都跑一遍~ 再之后就是同样的思路写写react-redux,react-router,那时再使用React  如烹小鲜尔~（我目前还在写React之中，这些都完成之后我打算写写webpack和babel了~）

路漫漫其修远兮~愿你我都能孜孜以求~

 

 

---------------------------------2333的分割线-----以下为原文就不修改了算是对自己的中二一种纪念吧~------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------



前言：最近一直在看React源码，看了几天总有雾里观花之感；便想着自己从头写一遍，这几天基本上写了个大概了；

React的VirtualDOM,DOM diff,生命周期管理，单向数据流动等等都具备了；

当然也省略了非常多的细节和检查，事件系统和CallBackQuenue,PoolClass等都没有~（暂时DOM diff不太全，我再想想怎么写更好）；

不过这样足够理解React了，而且React剩下的部分看看就基本知道作用了；




那么言归正传：说一说我个人感觉其中比较难得地方和一些思路；（我使用的是React15.3版本）

首先：React现在已经非常庞大了，我当初本想多写几篇一点一点介绍的，不过我发现即使写了光看的话肯定看不明白的，最好的方法只能是自己写一遍；

第二点：必须要首先弄懂Transition事务模块；

Transition模块：现在React绝大部分模块都需要Transition触发的，这个是一个包裹函数，构造函数需原型继承Transaction，或原型方法逐个赋值。且getTransactionWrappers方法用于添加前置钩子与后置钩子；reinitializeTransaction方法在初始化时调用，用于清空前、后置钩子；perform方法实际执行method函数、及前后钩子。（看不懂可以去跑一跑我的Git上的示例）

第三点：ReactElement以及ReactComponent；传入的参数先转化为ReactElement，然后根据不同的node类型转换为不同的ReactComponent;

第四点:ReactComponent的递归渲染和ReactClass的原型混入传入的参数，在递归渲染时原型调用（这个我有些说不明白），我是调试React的运行过程，看了十来遍看明白的~~

第五点：纸上得来终觉浅，绝知此事要躬行~~


绝大部分代码都加上注释了，想自己写一写的可以参照一下；

最后附上我的参照资料，也深深感谢这两位作者：

http://purplebamboo.github.io/2015/09/15/reactjs_source_analyze_part_two/

http://schifred.iteye.com/category/368891
