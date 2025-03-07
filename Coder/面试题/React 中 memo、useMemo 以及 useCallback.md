
都是为了解决 React 在改变引用数据类型数据时，引起组件不必要重新渲染的问题。
### memo

#### 应用场景

子组件未不依赖于父组件中的任何状态，但是在父组件更新状态（state）时，导致了子组件重新渲染。

使用 `memo()` 包裹住子组件，在该场景下，子组件不会重新渲染。

### useCallback

#### 应用场景

将父组件中的函数 `fn` 作为 `props` 传入子组件，在父组件更新 `state` 时，会重新渲染，导致重新创建 `fn` ，继而引发子组件重新渲染。

使用 `useCallback` 处理 `fn` 可避免子组件重新渲染。

### useMemo

#### 应用场景

父组件中的引用类型数据变量会在父组件重新渲染时重新创建，导致引发使用到该数据的子组件进行不必要的重新渲染。

使用 useMemo 返回该数据可避免子组件重新渲染。


#### 扩展：useMemo 和 useCallback 的不同点

- `useMemo` 的作用对象是变量，`useCallback` 的作用对象是函数；
- `useCallback` 会返回回调函数，而 `useMemo` 会执行回调函数；

### 参考

[memo()、useCallback()、useMemo()使用场景](https://juejin.cn/post/7039256825656524807)