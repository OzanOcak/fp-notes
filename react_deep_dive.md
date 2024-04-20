## 1) React Re-render

When state is changed react function/component will be re-rendered along with all the child components.
React doesn't check props.

```javascriptconst
Component = () => {
const [value,setValue] = useState("1");

return (
  <button onClick={()=>{setValue(2);} } />
  <Child value={value} />
)}
```
when button is clicked, state is updated then Component re-rendered. reagardeless of value Child also will be re-rendered.
