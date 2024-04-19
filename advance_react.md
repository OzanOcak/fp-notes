## React Performance

### Moving Down the state

```javascript
export default function App(){

const [isOpen,setIsOpen] = useState(false);

return(
<>
  <Button onClick-{()=> setIsPoen(true)}>Open</Button>
  {isOpen ? <ModelDialog onClose={()=> setIsOpen(false)}/> : null}
  <VerySlowComponent/>
  <BunchOfStuff/>
  <OtherStuffAlsoComponent/>
</>
)

}
```
