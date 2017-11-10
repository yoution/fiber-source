# fiber
react内部的组件单位

## fiber结构
```
fiber
|- tag type对应的标记
|- key 
|- type  fiber类型
|- stateNode component实例对象
|- return 父fiber，fiber tree中的位置
|- child  第一个子fiber，fiber tree中的位置
|- slibing 兄fiber，fiber tree中的位置
|- ref instance的ref
|- index 当前在父fiber中的index
|- pendingProps instance的newProps
|- memorizedProps instance的oldProps
|- memorizedState instance的state
|- updateQueue setState后的待更新状态
|  |- 
|- internalContextTag
|- effectTag 二进制tag，不同的位数代表不同的值
|- nextEffect effect tree中的位置
|- firstEffect effect tree中的位置
|- lastEffect effect tree中的位置
|- pendingWorkPriority 是否需要update标记
|- alternate 当前fiber的备份
|- _debug_xxxx 调试参数 
```

## fiber 类型
fiber根据component类型生成对应的fiber类型

### IndeterminateComponent


### FunctionalComponent


### ClassComponent
type为function,react对象

### HostRoot
根fiber，无对应的component

### HostComponent
type为string,如div，span
### HostText

### CoroutineHandlerPhase


### CoroutineComponent


### YieldComponent


### HostPortal


### Fragment
