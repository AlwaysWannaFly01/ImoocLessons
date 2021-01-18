#一.移动web开发与适配(mobile-web-rem)
## 1.rem布局基础

#二.vue3学习课程(Vue3Lesson)
## 1.vue3-test1(初始化vue3项目)

#三.b站李南江视频
 ## 1.vue3.0是如何变快的?
```
- diff算法优化:https://vue-next-template-explorer.netlify.app/
 
 + vue2中的虚拟dom是进行全量的对比
 
 + vue3新增了静态标记(PatchFlag),
 
    在与上次虚拟节点进行比对的时候,只比对带有patchflag的节点
    并且可以通过flag的信息得知当前节点要比对的具体内容
    
 - hoistStatic 静态提升
 
 + vue2中无论元素是否参与更新,每次都会重新创建,然后渲染
 
 + vue3中对于不参与更新的元素,会做静态提升,只会被创建一次,在渲染时直接复用即可
 
 - cacheHandlers时间侦听器缓存
 + 默认情况下onClick会被视为动态绑定,所以每次都会追踪它的变化
   但是因为是同一个函数,所以没有追踪变化,直接缓存起来复用即可



```
 
 
