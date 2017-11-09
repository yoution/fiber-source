# render
invokeGuardedCallback函数调用回调函数`workLoop`，`commitAllHostEffects`, `commitAllLifeCycles`。render过程和update过程都会分别经过这3个过程，内部会区分是render过程还是update过程。

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
![fiber-trees](./image/trees.png)   
图中有3个react对象，componetA，componentB，componentC，componentB包含componentC。   
### 创建fiber树
startWork创建fiber树，深度遍历jsx生成的component树，实例化component后生成对应的fiber树，直至叶子节点，不同的component类型创建对应的fiber节点，fiber节点形成关联关系，如父子关系，兄弟关系;
component的实例化过程，父fiber根据不同的fiber.tag，执行不同的component实例化:  
* ClassComponent: 实例化react对象, 执行instance.componentWillMount，执行render获取子component，为componetDidMount和ref打effectTag;    
* HostComponent: 为ref打effectTag;   
* ...

### 创建dom树
`completeWork`沿着`startWork`遍历的逆序遍历，从子fiber向父fiber遍历，直至某个fiber含有兄弟fiber，如果含有兄弟fiber，则结束当前过程，从兄弟fiber进行`startWork`过程。
子fiber根据不同的fiber.tag进行`completeWork`  
* ClassComponent: 无 
* HostComponent: 生成dom，将子fiber类型为HostComponent或者HostText类型的fiber的dom插入当前dom，创建dom树，设置props
* ...

### 创建effect树
effectTag，是二进制位构成的标记位，在`startWork`过程中生成，如instant含有componentDidMount函数，含有ref，会分别打上不同的标记位，供commit过程使用。
沿着`startWork`遍历的逆序遍历，每一个fiber在`completeWork`后，如果当前fiber含有effectTag，则将当前fiber加入fiber树中。
![effect](./image/effect.png)   
effect树的最终结果，就相当于沿着component树做的中序遍历值。

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
