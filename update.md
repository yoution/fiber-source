# update
# render
**invokeGuardedCallback**函数调用回调函数`workLoop`，`commitAllHostEffects`, `commitAllLifeCycles`，进行update过程。   
当某个component执行setState后，会从当前fiber向父fiber遍历，直至根fiber, 设置每个fiber的pendingWorkPriority，标示当前路径需要进行更新。

## 流程图
```js
  workLoop
    while {
      叶子节点 = beginWork(父fiber，子fiber) 
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

### 更新fiber树
`beginWork`
更新fiber树，深度遍历fiber树，进行更新操作, 直至子fiber不含有pendingWorkPriority。   
父fiber根据不同的tag，执行不同的fiber更新:  
* **ClassComponent**, componentWillReceiveProps，shouldComponentUpdate，componentWillUpdate，为componentDidUpdate打effectTag，为ref打effectTag，render生成新的子component，进行子fiber的diff，
  * 父fiber的子fiber和备份的父fiber的子fiber相同
    * 子component和新component进行diff
      * 如果key相同
        * 如果type相同, 复制子fiber，同时备份子fiber
        * 如果type不同,为子fiber和子fiber的兄弟fiber打上删除effectTag，将它们加入effect树
      * 如果key不同,为子fiber和子fiber的兄弟fiber打上删除effectTag，将它们加入effect树
 为新的component生成fiber，新fiber后续走[`render`](./render.md)流程创建render树，创建dom树，创建effect树。
* **HostComponent**, diff当前fiber的props
  * 如果相同，复制fiber，同时备份子fiber
  * 如果不同
* ...

### 更新dom树
`completeWork`沿着`beginWork`遍历的逆序遍历，从子fiber向父fiber遍历，直至某个fiber含有兄弟fiber，如果含有兄弟fiber，则结束当前过程，从兄弟fiber进行`beginWork`过程。   
如果该子fiber为新增加的，则按照[`render`](./render.md)过程操作，   
如果该子fiber只是更新，则根据不同的.tag进行`completeWork`  
* **ClassComponent**，无 
* **HostComponent**, 更新fiber的props，为props改变打effectTag
* ...


### 更新effect树

## commitAllHostEffects
沿着effect树进行遍历，detatchRef，根据effectTag进行
* **Placement**: 新增加的fiber执行同[`render`](./render.md)
* **Deletion**: 从删除fiber开始进行深度遍历子遍历，按照fiber的tag进行删除操作:
  * **ClassComponent**:删除ref，执行componentWillUnmount
  * **HostComponent**: 删除ref，从父dom删除子dom
* **PlacementAndUpdate**
* **Update**
  * **HostComponent**: 更新props到dom,设置content

## commitAllLifeCycles
重新沿着effect树进行遍历，根据fiber的effectTag的值进行对应的操作。   
如果是新fiber，则执行[`render`](./render.md)过程的操作，如果是老的fiber，每一个fiber依次进行
1. **commitAttachRef**，处理component上的ref值   
2. **commitLifeCycles**, 
  * **ClassComponent**: 执行componentDidUpdate，执行setState回调
  * **HostComponent**: 如有focus，执行focus操作, 处理ref
