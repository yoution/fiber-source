# render
初始化的render过程,invokeGuardedCallback函数调用回调函数workLoop,commitAllHostEffects, commitAllLifeCycles,
```js
  workLoop
    while {
      叶子节点 = startWork(父fiber，子fiber) 
      if(叶子节点) {
        兄节点 = completeWork(叶子节点)
      }
    }
    commitAllWork
      commitAllHostEffects
        commitAllLifeCycles
```

## workLoop
```js   
  loop: do {
    叶子节点 = startWork(父fiber，子fiber) 
    if(叶子节点) {
      兄节点 = completeWork(叶子节点)
    }
  }
```
startWork: 深度遍历节点构造fiber树,根据jsx生成的节点类型创建对应的fiber节点，形成关联关系,父子关系，兄弟关系，深度遍历到叶子节点时，
父fiber根据不同的fiber.tag,执行不同的component初始化
如ClassComponent: 实例化react对象, instance.componentWillMount,render获取子component,componetDidMount和ref打effectTag

completeWork: 将含有effectTag值的fiber生成effect树,按照深度遍历生成effect树

## commitAllHostEffects
按照effect数
commitAllWork阶段进行
commitDetachRef

effectTag
Placement
PlacementAndUpdate
Update
Deletion

## commitAllLifeCycles
按照effect树
commitLifeCycles
commitAttachRef
