# fiber
react内部的组件单位

## fiber 构成
```
fiber
|- tag 
|- key
|- type  fiber类型
|- stateNode component实例
|- return 父fiber
|- child  第一个子fiber
|- slibing 兄fiber
|- ref
|- index 当前在父fiber中的index
|- pendingProps
|- memorizedProps
|- updateQueue
|- internalContextTag
|- effectTag 二进制tag，不同的位数代表不同的值
|- nextEffect
|- firstEffect
|- lastEffect
|- pendingWorkPriority
|- alternate
|- _debug_xxxx 调试参数 
```

## fiber 类型
fiber根据component类型生成对应的fiber类型

## IndeterminateComponent


## FunctionalComponent


## ClassComponent


## HostRoot
根fiber，无对应的component

## HostComponent

## HostText

## CoroutineHandlerPhase


## CoroutineComponent


## YieldComponent


## HostPortal


## Fragment
