# fiber
react内部的组件单位

## fiber结构
```
fiber
|- tag type对应的标记
|- key  component的key
|- type  fiber类型
|- stateNode component实例对象
|- return 父fiber，fiber tree中的位置
|- child  第一个子fiber，fiber tree中的位置
|- slibing 兄fiber，fiber tree中的位置
|- ref component的ref
|- index 当前在父fiber中的index
|- pendingProps component的newProps
|- memorizedProps component的oldProps
|- memorizedState component的state
|- updateQueue setState后的待更新状态
|- internalContextTag
|- effectTag 二进制tag，不同的位数代表不同的值
|- nextEffect effect tree中的位置
|- firstEffect effect tree中的位置
|- lastEffect effect tree中的位置
|- pendingWorkPriority update的待更新等级
|- alternate 当前fiber的备份
|- _debug_xxxx 调试参数 
```

## fiber 类型
fiber根据[component类型](./component.md)生成对应的fiber类型

* **HostRoot** 生成根fiber，相当于container元素生成的component
* **IndeterminateComponent** type为function，非react对象，相当于render函数，没有react生命周期
* **FunctionalComponent** 
* **ClassComponent** react.element
* **HostComponent** type为string普通component，如div，span
* **HostText**  type为string的普通component，且是anoymouns element
* **CoroutineHandlerPhase** 
* **CoroutineComponent**  react.coroutine
* **YieldComponent**  react.yield
* **HostPortal**  react.portal
* **Fragment** 
