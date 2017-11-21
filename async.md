# async
开启异步
```js
  Component.prototype.unstable_isAsyncReactComponent = true
```
requestIdleCallback调用`workLoop`

## 流程图
```js
  workLoop
    while {
      if(timeRemaining() > 0){
        叶子节点 = beginWork(父fiber，子fiber) 
        if(!叶子节点){
          while(父fiber) {
            if(子fiber) {
              父fiber = completeWork(子fiber)
              创建effect树() 
              if(父fiber.兄fiber){ break; }
            }
          }
        }
      }
    }
    if(timeRemaining() > 0){
      commitAllWork
        commitAllHostEffects
          commitAllLifeCycles
    }
```

