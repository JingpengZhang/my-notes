### useMemo

#### 解决了什么问题？

父组件


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