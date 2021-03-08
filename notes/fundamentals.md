# 一些基础知识点总结
https://www.youtube.com/channel/UC80PWRj_ZU8Zu0HSMNVwKWw - 看的这位宝藏博主的教学视频

# Create a new app
1. 记住React是一个js的library, 不是一个framework!
2. `npx create-react-app hello-world`

# Folder structure
1. public folder 里面有一个 `index.html`，这是整个app唯一(?)的一个Html。因为我们要全权让React来render html的body。   
在 `index.html` 里面有一个id为root的div:   
```
<div id="root"></div>
```
React在`index.js`来操作它：   
```
ReactDOM.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
  document.getElementById('root')
);
```
# Functional Components
1. 就是javascript functions. Input: `Props`. Outpu: html (JSX)
2. Default export   
这里终于了解了import/export 名称不match的情况！
假如说我们有另一个file里面定义了一个 `Greet` component，但是有default export (id: `export default Greet`). 这时候我们在另一个file来Import它的时候，可以不用 `Greet`这个名字，也可以不用大括号，比如 `import Component2 from ./components/Greet`      
但是如果我们在`Greet.js`里面最后写了 `export const Greet`. 那我们import的时候必须也要用 `import { Greet } from "./components/Greet"`. 也要注意有括号和没括号的区别！   
# Class Components
1. 要 extents React的Component class
2. 相比于Functional Components 有 state, 还有 `this` keyword，可以用hooks
3. 必须有 render(return()) function
4. 也要 export
# Props vs State
Props:
- props get passed to the componenet
- props are immutable
- props -> Functional Components; this.props -> Class Components

State:
- state is managed within the component
- Variables declared in the function body
- State can be changed
- `useState` Hook - Functional Components
- `this.state` - Class Components
# setState
为什么必须要用`setState` 而不能直接修改state（比如 `this.state.count = 10`)呢？因为第二种虽然可以改变state，但是无法Render UI.
`setState` 可以加callback function! `setState(..new state.., callback())`
比如：   
```
this.setState(
  // 下面是新的state
  {
    count: this.state.count + 1
  },
  // 下面的是callback function, change完state会call
  () => {
    console.log('Callback value', this.state.count)
  }
)
```