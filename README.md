# useInitializer

A React hook for once-only initialization with dependency tracking and cleanup

This exists for when you want to initialize an object once in a react component. We tend to reach for useState(init) or useMemo() to handle this, however these patterns turn out to be subtly flawed and will fail in react strict mode
https://github.com/facebook/react/issues/27735#issuecomment-1885624506

Usage:
```tsx
const exampleObject = useInitializer(
    ([input]) => new Example(input),
    obj => obj.dispose(),
    [input]
);
```

`exampleObject` will only be initialized when `input` changes and will remain unchanged between rerenders

The disposal function will be called when the component is unmounted or when dependencies change

If the initializer or disposal function changes, behavior is undefined