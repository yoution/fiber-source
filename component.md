# component
component类型分为react component和普通component

## 普通component
浏览器dom构成的component，type为string，如div，span

## react component
* **Symbol(react.element)** 通过createElement或者通过es6 的extends Component生成的react类型
* **Symbol(react.portal)** 通过createPortal创建的react类型
* **Symbol(react.coroutine)** 还没开放接口
* **Symbol(react.yield)** 还没开放接口
