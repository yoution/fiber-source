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

|Name|Status|Description|
|:--:|:----:|:----------|
|<a href="https://github.com/webpack/html-loader"><img width="48" height="48" src="https://worldvectorlogo.com/logos/html5.svg"></a>|![html-npm]|Exports HTML as string, require references to static resources|
|<a href="https://github.com/pugjs/pug-loader"><img width="48" height="48" src="https://cdn.rawgit.com/pugjs/pug-logo/master/SVG/pug-final-logo-_-colour-128.svg"></a>|![pug-npm]|Loads Pug templates and returns a function|
|<a href="https://github.com/webpack/jade-loader"><img width="48" height="48" src="https://worldvectorlogo.com/logos/jade-3.svg"></a>|![jade-npm]|Loads Jade templates and returns a function|
|<a href="https://github.com/peerigon/markdown-loader"><img width="48" height="48" src="https://worldvectorlogo.com/logos/markdown.svg"></a>|![md-npm]|Compiles Markdown to HTML|
|<a href="https://github.com/posthtml/posthtml-loader"><img width="48" height="48" src="http://posthtml.github.io/posthtml/logo.svg"></a>|![posthtml-npm]|Loads and transforms a HTML file using [PostHTML](https://github.com/posthtml/posthtml)|
|<a href="https://github.com/altano/handlebars-loader"><img width="48" height="48" src="https://worldvectorlogo.com/logos/handlebars-1.svg"></a>|![hbs-npm]| Compiles Handlebars to HTML|


| |rootcomponent|子component|
|-------|-------------|-------------|
|render|异步|同步|
|update|异步|异步|
