### memo

#### 解决了什么问题？

子组件未不依赖于父组件中的任何状态，但是在父组件更新状态（state）时，导致了子组件重新渲染。

使用 `memo()` 包裹住子组件，可以在该场景下，子组件不会重新渲染。

#### 使用示例

```tsx
const Father = () => {
  console.log("Father 渲染了");

  const [count, setCount] = useState(0);

  return (
    <>
      <h1>Father</h1>
      <p>count: {count}</p>
      <button onClick={() => setCount(count + 1)}>add</button>
      <Child />
    </>
  );
};
export default Father;

```

```tsx
const Child = memo(() => {
  console.log("Child 渲染了");

  return (
    <>
      <h1>Child</h1>
    </>
  );
});
export default Child;
```

### useMemo

#### 应用场景

将父组件中的函数 `fn` 作为 `props` 传入子组件，子组件调用