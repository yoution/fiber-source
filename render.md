# render
初始化的render过程,invokeGuardedCallback函数调用回调函数workLoop, commitAllLifeCycles,

## workLoop
```js   
  loop: do {
    performWork() {
      叶子节点 = startWork(父fiber，子fiber) 
      if(叶子节点) {
        兄节点 = completeWork(叶子节点)
      }
    }
    commitAllWork()
  }
```
深度遍历节点构造fiber树,根据jsx生成的节点类型创建对应的fiber节点，形成关联关系,父子关系，兄弟关系，深度遍历到叶子节点时，
completeWork: 生成effect树,按照深度遍历生成effect树


## commitAllLifeCycles
commitAllWork阶段进行
commitDetachRef

effectTag
Placement
PlacementAndUpdate
Update
Deletion
