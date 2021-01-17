# fed-e-task-04-01

#### 1. 请简述 React 16 版本中初始渲染的流程
##### React初始渲染分为 render 和 commit 阶段，render阶段是协调层负责阶段，该阶段需为每个 react 元素构建 Fiber 对象，在创建 Fiber 对象之后还要为些创建相对应的 DOM 对象，要为 Fiber 对象添加 effectTag 属性，用来记录当前 Fiber 要执行的 DOM 操作，这个新构建的 Fiber 对象可以称作是 workInProgress 树，可理解为待提交的 Fiber 树，然后在render 结束后， fiber 会被保存到 fiberroot 中。在 commit 阶段可先获取 render 的成果，就是在 fiberroot 中新构建的 workInProgress Fiber 树，最后根据 fiber 中的 effectTag 属性进行相应的 DOM 操作

#### 2. 为什么 React 16 版本中 render 阶段放弃了使用递归
##### 递归耗内存，它使用 JavaScript 自身的执行栈，更新一旦开始，中途就无法中断。当VirtualDOM 树的层级很深时，virtualDOM 的比对就会长期占用 JavaScript 主线程，由于 JavaScript 又是单线程的无法同时执行其他任务，所以在比对的过程中无法响应用户操作，无法即时执行元素动画，造成了页面卡顿的现象。

#### 3. 请简述 React 16 版本中 commit 阶段的三个子阶段分别做了什么事情
##### 1、检查 finishedWork 是否也有 effect ，如有插入 effect 链表中
##### 2、第一次遍历effect链，更新class组件实例上的state,props，执行getSnapshotBeforeUpdate生命周期
##### 3、第二次遍历effect链，不同的effectTag，执行不同的操作，比如重置文本节点，执行 插入、更新、删除等的 effect 操作，真正的对 dom 进行修改。
##### 4、第三次遍历effect链，这次遍历就是做一些收尾工作。执行componentDidMount、componentDidUpdate，更新的回调函数等。


#### 4. 请简述 workInProgress Fiber 树存在的意义是什么
##### 实现双缓存技术, 在内存中构建 DOM 结构以及 DOM 更新, 在 commit 阶段实现 DOM 的快速更新.


