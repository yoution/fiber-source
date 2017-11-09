# update
# render
invokeGuardedCallback函数调用回调函数`workLoop`，`commitAllHostEffects`, `commitAllLifeCycles`。进行update过程。

## 流程图
```js
  workLoop
    while {
      叶子节点 = startWork(父fiber，子fiber) 
      while {
        if(叶子节点) {
          兄节点 = completeWork(叶子节点)
        }
        创建effect树() 
      }
    }
    commitAllWork
      commitAllHostEffects
        commitAllLifeCycles
```

## workLoop

## commitAllHostEffects
沿着effect树进行遍历
> 按照effect数
> commitAllWork阶段进行
> commitDetachRef

effectTag
Placement
PlacementAndUpdate
Update
Deletion

## commitAllLifeCycles
按照effect树
commitLifeCycles
commitAttachRef
