# async
默认执行同步流程，通过以下方式开启异步流程
```js
  Component.prototype.unstable_isAsyncReactComponent = true
```

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
              if(父fiber.兄fiber){ 
                父fiber = 父fiber.兄fiber
                break; 
              }
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
异步调用的核心为[`requestIdleCallback`](https://developers.google.com/web/updates/2015/08/using-requestidlecallback)调用`workLoop`

## async的影响
`unstable_isAsyncReactComponent`标记在不同的component上，对`render`和`update`过程会产生不同的效果   
| |rootcomponent|子component|
|-------|-------------|-------------|
|render|异步|同步|
|update|异步|异步|
