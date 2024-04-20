## React Performance

### 1-Moving Down the state

When the state is changed, the component is rerendered along with all the child components.

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
#### Abstracting with custom hooks doesn't change performance problem

Using custom hook doesn't change child components being rerendered, it is just abstract functions and states so reading code become easier

```javascript
const useModalDialog = () => {
  const [isOpen, setIsOpen] = useState(false);
  const [width, setWidth] = useState(0);

  useEffect(() => {
    const listener = () => {
      setWidth(window.outerWidth);
    };

    window.addEventListener('resize', listener);

    return () => window.removeEventListener('resize', listener);
  }, []);

  return {
    isOpen,
    open: () => setIsOpen(true),
    close: () => setIsOpen(false),
  };
};


export default function App() {
  // state is in hook now
  const { isOpen, open, close } = useModalDialog();

  useEffect(() => {
    console.info('Component that uses useModalDialog re-renders');
  });

  return(
   <>
     <Button onClick-{open}>Open</Button>
     {isOpen ? <ModelDialog onClose={close}/> : null}
     <VerySlowComponent/>
     <BunchOfStuff/>
     <OtherStuffAlsoComponent/>
   </>
   )
}
```
The solution is moving the state to child component so only child component will be re-rendered when the state is changed.

```
const ButtonWithModalDialog = () => {
  const [isOpen, setIsOpen] = useState(false);

  // render only Button and ModalDialog here
  return (
    <>
      <Button onClick={() => setIsOpen(true)}>Open dialog</Button>
      {isOpen ? <ModalDialog onClose={() => setIsOpen(false)} /> : null}
    </>
  );
};
```
### 2-Pure Functions

For some components, it is not possible to move state down

```javascript
const MovingBlock = ({ position }: { position: number }) => (
  <div className="movable-block" style={{ top: position }}>
    {position}
  </div>
);

const getPosition = (val: number) => 150 - val / 2;

export default function App() {
  const [position, setPosition] = useState(150);

  const onScroll = (e: any) => {
    const calculated = getPosition(e.target.scrollTop);
    setPosition(calculated);
  };

  return (
    <div className="scrollable-block" onScroll={onScroll}>
      <MovingBlock position={position} />
      <VerySlowComponent />
      <BunchOfStuff />
      <OtherStuffAlsoComplicated />
    </div>
  );
```
when we scroll down, state of position will change and all components including child components will be rerendered. the solution of this is passing components as an argument 

```javascript
  return (
    <div className="scrollable-block" onScroll={onScroll}>
      <MovingBlock position={position} />
      {/* put our children prop here, where the slow bunch of stuff used to be */}
      {children}
    </div>
  );
```
