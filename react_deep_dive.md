## 1) React Re-render

When state is changed react function/component will be re-rendered along with all the child components.
React doesn't check props.

```javascript
const Component = () => {
const [value,setValue] = useState("1");

return (
  <button onClick={()=>{setValue(2);} } />
  <Child value={value} />
)}
```
when button is clicked, state is updated then Component re-rendered. reagardless of value Child also will be re-rendered.

## 2) Preventing re-render

When the state is change or parent component re-rendered, the child component will be re-rendered too. There are some options to keep child components limited.

### a) Moving state down

```javascript
const Component= () => {
  return (
    <>
      <BtnDialog />
      <VerySlowComponent />
      <OtherSlowComponent />
    </>
  )}

  const BtnDialog = () => {
      const [isOpen,setIsOpen] = useState(false);
      return(
        <>
          {isOpen && <ModalDialog />
          <Button onClick={()=>{setIsOpen(true)}}></Button>
      })

```

### b) Components as children prop

In some stiuations we can not move state down such as scrolling, in this case creating pure functin and passing child components as children is the option

```javascript

const ComponentWithScroll = ({children}) => {
  const [scrollY,setScrollY] = useState(0);
  return(
    <div onScroll={({currentTarget})=>setScrollY(currentTarget.scrollTop)}} >
      {children}
    </div>
)}

const Component = () => {
  return(
<ComponentWithScroll>
  {children}
</ComponentWithScroll>
)}
```

### c) Components as props

Because components are props, componets will not be rendered when state is updated while state change still provides us the logic we need.

```javascript
const Layout = ({ column, content}) => {
  const [isCollapsed, setIsCollapsed] = useState(false);

  return (
    <div>
      <div>{column}</div>
      <div>
        <button onClick={()=>setIsCollapsed(!isCollapsed)}> {content} </button>
      </div>
    </div>
)}

const Component = () => {

return(
  <Layout
    column={<VerySlowComponent />}
    constent={<BunchOfSlowStuff />}
  />
)}
```

### 3) Preventing re-render with React.memo

we need to memorize child vomponent with React.memo however it is not enogh, props are need to be memorized too if they are not primitive such as number or string, because functions,arrays and objects are pass by ref.

```javascript
const ChildMemo = React.memo(Child);

const Parent = () => {
  const onChangeMemo = useCallback(()=>{ //do something },[])
  const valueMemo = useMemo(() => return {value: 'value'};)

  return <ChildMemo onChange={onChangeMemo} someValue={valueMemo}/>
}
```

While Parent component can be memorized with React.memo, since child component is an element of react object, it sould be memorized with useMemo

```javascript

const MemoParent = React.memo(Parent);
const Child = () => <div>something</div>;

const Component = () => {
  const onClick = useCallBack(()=>{
    // do something
  },[])

  const child = useMemo(()=><Child/>,[]);

  return(
    <MemoParent onClck={onClick}>
      {child}
    </MemoParent>)
}
```

### 4) Using key index

- We shouldn't use uuid because every render.it will assign new numbers
- We shouldn't use index number because if we assign new value at the top of list, all lisr index will be shifted (if the array is static,using index is fine)

  best practice for dynamic arrays :

```javascript
const data =[
{id:'kitten1', name:'Mittens'},
{id:'kitten2', name:'Grumpy'}
{id:'kitten3', name:'Mr.Cat'}];
```




     
  
