### useMemo

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

```