# **Investigation into Issue 2: Parent/Child Rendering Issue**

While I was unable to find a definite second rendering issue impacting both Parent and Child copmonents, I did find possible issues or things I am questioning.

## **Possible Issue: Button onClick Callback function**
Could use 'useCallback' to memoize the counter button's onClick callback:

#### Original
```JSX
<button 
  onClick={() => {
    setValue((value) => value + 1);
  }}
> 
```

#### With 'useCallback'
```JSX
const handleClick = useCallback(() => {
  setValue((value) => value + 1)
})

<button onClick={handleClick}>
  Update State on Parent ++
</button>
```

### Reasoning For:
- This would prevent the function from being recreated each time the component is re-rendered.
- If in the future this application needed a second counter in the same component we would already have useCallback implemented for the first counter's callback.

### Reasoning Against:
- As is, the counter is not a heavy computation and this may be counter productive.
- Not sure if this would be considered a 'rendering' issue.


## **Questioning/Curiousity**
- The string 'Child Component' does not change nor is it a heavy computation, so I would not intially memoize it.
- Why is it being memoized?