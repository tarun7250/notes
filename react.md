# jsx rules
- Return a single root element 
- If you don’t want to add an extra <div> to your markup, you can write <> and </> instead 
- This empty tag is called a `Fragment`. Fragments let you group things without leaving any trace in the browser HTML tree.

reason JSX looks like HTML, but under the hood it is transformed into plain JavaScript objects. You can’t return two objects from a function without wrapping them into an array. This explains why you also can’t return two JSX tags without wrapping them into another tag or a Fragment.

- Close all the tags (like img li ... can work without closing in html but not in jsx)
- most of the things are camel case now

# JavaScript in JSX with Curly Braces
- As text directly inside a JSX tag: \<h1>{name}'s To Do List\</h1> works, but <{tag}>Gregorio Y. Zara's To Do List</{tag}> will not.
- As attributes immediately following the = sign: src={avatar} will read the avatar variable, but src="{avatar}" will pass the string "{avatar}".
- React does not require you to use `inline styles` (CSS classes work great for most cases). But when you need an inline style, you pass an `object` to the `style attribute`

# conditional rendering
- (?:) && ?? || if(){}else{} can be used for conditional rendering
```jsx
function Item({ name, isPacked }) {
  let itemContent = name;
  if (isPacked) {
    itemContent = name + " ✅";
  }
  return (
    <li className="item">
      {itemContent}
    </li>
  );
}
```

```jsx
function Item({ name, isPacked }) {
  let itemContent = name;
  if (isPacked) {
    itemContent = (
      <del>
        {name + " ✅"}
      </del>
    );
  }
  return (
    <li className="item">
      {itemContent}
    </li>
  );
}
```

# \<Fragment> (<></>)
- does not add overhead 
- agar typescript me banate hain react wala to bas element hi return kar sakte hain nahi to typescript error show karne lgta hai but in js normal array bhi return kar sakte hain
- Warning: Invalid prop `onClick` supplied to `React.Fragment`. React.Fragment can only have `key` and `children` props.
    at App

# first component
- `export default functionName(){}` function name doesn't affect the name of the file affects
- React components are regular JavaScript functions, but their names must start with a `capital letter` or they won’t work!, for using function as `markup` define as capital letter
-  if your markup isn’t all on the same line as the return keyword, you must wrap it in a pair of parentheses

```ts
//Components can render other components, but you must never nest their definitions:

export default function Gallery() {
  // 🔴 Never define a component inside another component!
  function Profile() {
    // ...
  }
  // ...
}
//The snippet above is very slow and causes bugs. Instead, define every component at the top level:

export default function Gallery() {
  // ...
}

// ✅ Declare components at the top level
function Profile() {
  // ...
}
//When a child component needs some data from a parent, pass it by props instead of nesting definitions.
```

# import export
- A file can have no more than one default export, but it can have as many named exports as you like.

export default function Button() {}	import Button from './Button.js'; <br/>
export function Button() {}	import { Button } from './Button.js';

```jsx
import Default from './components/TodoList';// default imported in this way
import { Normal } from './components/TodoList';// normal imported in this way
```

# props
- can take arguments by `destructuring` or directly single variable
```jsx
function Avatar({ person, size }) {
  // person and size are available here
}
function Avatar(props) {
  // person and size are available here
}
```
- can pass props through spread operator
```jsx
function Profile(props) {
  return (
    <div className="card">
      <Avatar {...props} />
    </div>
  );
}
```
-  props are immutable
-  When a component needs to change its props it will have to “ask” its parent component to pass it different props (`error`)
- **when you pass a single child then it goes as object but multiple child goes as array**

# rendering lists
- Locally generated data: If your data is generated and persisted locally (e.g. notes in a note-taking app), use an incrementing counter, `crypto.randomUUID()` or a package like uuid when creating items.
- making any javascript array for printing it must have key which is not received as argument through props
- keys are automatically converted into strings
- Similarly, do not generate keys on the fly, e.g. with key={Math.random()}. This will cause keys to never match up between renders, leading to all your components and DOM being recreated every time. Not only is this slow, but it will also lose any user input inside the list items. Instead, use a stable ID based on the data.
-  React will use if you don’t specify a key at all. But the order in which you render items will change over time if an item is inserted, deleted, or if the array gets reordered. Index as a key often leads to subtle and confusing bugs.

# pure components
- same input should always give same output
- Pure functions don’t mutate variables outside of the function’s scope or objects that were created before the call—that makes them impure!
- However, it’s completely fine to change variables and objects that you’ve just created while rendering.
- updating the screen, starting an animation, changing the data—are called `side effects`. They’re things that happen “on the side”, not during rendering.
- If some data changes in the middle of rendering a deep component tree, React can restart rendering without wasting time to finish the outdated render. Purity makes it safe to stop calculating at any time.

# react trees
- react render tree has only react components not ui primitives
-  bundle all the necessary JavaScript to ship to the client. The tool responsible for this is called a bundler, and bundlers will use the dependency tree to determine what modules should be included.

# react Events
- Are usually defined inside your components.
- Have names that start with `handle`, followed by the name of the event.
- you log the event object (e), the event is still active inside the handler. However, when you expand the logged object in the browser console later, it might show currentTarget as null because the event has already been recycled.??
- Note that the value of currentTarget is only available in a handler for the event. Outside an event handler it will be null. This means that, for example, if you take a reference to the Event object inside an event handler and then access its currentTarget property outside the event handler, its value will be null.
- multiple????
- It travels down, calling all onClickCapture handlers.
- It travels up, calling all onClick handlers.
- a \<form> submit event, which happens when a button inside of it is clicked, will reload the whole page by default it should be prevented using `e.preventDefault();`inside handler
- Unlike rendering functions, event handlers don’t need to be pure,

# state management
- Local variables don’t persist between renders.
- Changes to local variables won’t trigger renders. 
- State is isolated and private  each component has its own state
- 

# renders
### trigger -> render-> commit
- in “Strict Mode”, React calls each component’s function twice to check errors
- Triggering a render (delivering the guest’s order to the kitchen)
- Rendering the component (preparing the order in the kitchen)
- Committing to the DOM (placing the order on the table)
- There are two reasons for a component to render:
  - It’s the component’s initial render.
  - The component’s (or one of its ancestors’) state has been updated.
- On initial render, React will call the root component.
- For subsequent renders, React will call the function component whose state update triggered the render.
- For the initial render, React will use the appendChild() DOM API to put all the DOM nodes it has created on screen.
- For re-renders, React will apply the minimal necessary operations (calculated while rendering!) to make the DOM match the latest rendering output.
- React only changes the DOM nodes if there’s a difference between renders

# ?? avoid state contradiction test
```jsx
import { useState } from 'react';

export default function FeedbackForm() {
  const [text, setText] = useState('');
  const [isSending, setIsSending] = useState(false);
  const [isSent, setIsSent] = useState(false);

  async function handleSubmit(e) {
    e.preventDefault();
    setIsSending(true);
    await sendMessage(text);
    setIsSending(false);
    setIsSent(true);
  }

  if (isSent) {
    return <h1>Thanks for feedback!</h1>
  }

// Pretend to send a message.
function sendMessage(text) {
  return new Promise(resolve => {
    setTimeout(resolve, 2000);
  });
}

```
# states
- Group related state consider merging them
- avoid deeply nested state, flatten them make them at top level this will make them to change easily
### updating a nested object
```jsx
const [person, setPerson] = useState({
  name: 'Niki de Saint Phalle',
  artwork: {
    title: 'Blue Nana',
    city: 'Hamburg',
    image: 'https://i.imgur.com/Sd1AgUOm.jpg',
  }
});
/// can be done in this way
setPerson({
  ...person, // Copy other fields
  artwork: { // but replace the artwork
    ...person.artwork, // with the same one
    city: 'New Delhi' // but in New Delhi!
  }
});
```
- for changing objects using states new instance has to be created  like above can flatten deeply nested object to work bit easily but in case use immer 

```jsx
updatePerson(draft => {
  draft.artwork.city = 'Lagos';
});
```
- `npm install use-immer`
- `import { useImmer } from 'use-immer'`
```jsx
const [person, updatePerson] = useImmer({
  name: 'Niki de Saint Phalle',
  artwork: {
    title: 'Blue Nana',
    city: 'Hamburg',
    image: 'https://i.imgur.com/Sd1AgUOm.jpg',
  }
});

function handleNameChange(e) {
  updatePerson(draft => {
    draft.name = e.target.value;
  });
}
```
- state mutation is not recommended 

id | avoid (mutates the array)| prefer (returns a new array)
--- | --- | --- 
adding | push, unshift | concat, [...arr] spread syntax
removing | pop, shift, splice | filter, slice 
replacing | splice, arr[i] = ... assignment | map 
sorting | reverse, sort | copy the array first

useImmer can be used for both 
### array states
- Adding to an array
```jsx
setArtists( // Replace the state
  [ // with a new array
    ...artists, // that contains all the old items
    { id: nextId++, name: name } // and one new item at the end
  ]
);
```
- Removing from an array
```jsx
setArtists(
  artists.filter(a => a.id !== artist.id)
);
```
- Transforming an array 
```jsx
function handleClick() {
    const nextShapes = shapes.map(shape => {
      if (shape.type === 'square') {
        return shape;
      } else {
        return {
          ...shape,
          y: shape.y + 50,
        };
      }
    });
    setShapes(nextShapes);
  }
```
```jsx
{counters.map((counter, i) => (
  <li key={i}>
    {counter}
    <button onClick={() => {
      handleIncrementClick(i);
    }}>+1</button>
  </li>
))}

const nextCounters = counters.map((c, i) => {
      if (i === index) {
        // Increment the clicked counter
        return c + 1;
      } else {
        // The rest haven't changed
        return c;
      }
    });
    setCounters(nextCounters);
```
- updating objects inside array
```jsx
function handleToggleMyList(artworkId, nextSeen) {
  const myNextList = [...myList];
  const artwork = myNextList.find(
    a => a.id === artworkId
  );
  artwork.seen = nextSeen;
  setMyList(myNextList);
}
```
- rest can be done directly using array functions of javscript
- and for concise code can use immer

#### imperative and declarative
- imperative ui design involves telling everything if this happens make this happen.....
- in declarative just define states initial and final and tell the changes framework will handle it
- “living styleguides” or “storybooks”.
- declarative principle
  - Identify your component’s different visual states
  - Determine the human and computer triggers for state changes.
  - Model the state with useState.
  - Remove non-essential state to avoid bugs and paradoxes.
  - Connect the event handlers to set state.

## state preserving
### Same component at the same position preserves state 
### it’s the position in the UI tree—not in the JSX markup—that matters to React! 
```jsx
<div>
  {isFancy ? (
    <Counter isFancy={true} /> 
  ) : (
    <Counter isFancy={false} /> 
  )}
  <label>
    <input
      type="checkbox"
      checked={isFancy}
      onChange={e => {
        setIsFancy(e.target.checked)
      }}
    />
    Use fancy styling
  </label>
</div>

/////
export default function App() {
  const [isFancy, setIsFancy] = useState(false);
  if (isFancy) {
    return (
      <div>
        <Counter isFancy={true} />
        <label>
          <input
            type="checkbox"
            checked={isFancy}
            onChange={e => {
              setIsFancy(e.target.checked)
            }}
          />
          Use fancy styling
        </label>
      </div>
    );
  }
  return (
    <div>
      <Counter isFancy={false} />
      <label>
        <input
          type="checkbox"
          checked={isFancy}
          onChange={e => {
            setIsFancy(e.target.checked)
          }}
        />
        Use fancy styling
      </label>
    </div>
  );
}
```
- rendering components at different positions to refresh state
```jsx
{isPlayerA &&
  <Counter person="Taylor" />
}
{!isPlayerA &&
  <Counter person="Sarah" />
}
```
- specifying keys tells react to keep keys itself as part of the position instead of there order in the parent

### preserving states of removed components
- hide with CSS
- lift up states
- use localStorage

-  React waits until all code in the event handlers has run before processing your state updates.
- for updating same state multiple times use updater function
- `setNumber(n => n + 1): n => n + 1 is a function. React adds it to a queue.` return value is used for the next 
- 

# useRef
- “remember” some information, but you don’t want that information to trigger new renders, you can use a ref.
- updates synchronously
- \<div ref={myRef}>, React will put the corresponding DOM element into myRef.current. Once the element is removed from the DOM, React will update myRef.current to be null **works only on builtin browser components** not custom ones
- for keeping list in ref store a map / array in ref.current and then push refs inside it 
```jsx
<li
  key={cat}
  ref={(node) => {
    const map = getMap();
    if (node) {
      map.set(cat, node);
    } else {
      map.delete(cat);
    }
  }}
>
```
- for keeping refs to custom components
- React sets ref.current during the commit
- Before updating the DOM, React sets the affected ref.current values to null. - After updating the DOM, React immediately sets them to the corresponding DOM nodes.
-  scrolling to a node, focusing a node, triggering an animation, selecting text, or calling browser APIs that React does not expose
- try to modify the DOM manually, you can risk conflicting with the changes React
### forwarding ref
- if want to attach ref to child node then it must be wrapped in forwardRef
```jsx
const MyInput = forwardRef((props, ref) => {
  return <input {...props} ref={ref} />;
});
//calling
<MyInput ref={inputRef}>
```

### useImperativeHandle
- forward only particular functions or  of child component to parent
```jsx
const realInputRef = useRef(null);
useImperativeHandle(ref, () => ({
  // Only expose focus and nothing else here it exposes this particular object
  focus() {
    realInputRef.current.focus();
  },
}));
return <input {...props} ref={realInputRef} />;

```
### flushSync
- escapes react way of batching state updates and does the updates synchronously
- pass function in flushSync
```jsx
function handleAdd() {
  const newTodo = { id: nextId++, text: text };
  flushSync(() => {
    setText('');
    setTodos([ ...todos, newTodo]);      
  });
  listRef.current.lastChild.scrollIntoView({
    behavior: 'smooth',
    block: 'nearest'
  });
}
```
# effects
- Effects run at the end of a commit after the screen updates
- in strict mode runs twice during mounting
- preloading data or hoisting data requirements to routes??
```jsx
//avoiding race conditions -  ignore stale responses
useEffect(() => {
  let ignore = false;
  setBio(null);
  fetchBio(person).then(result => {
    if (!ignore) {
      setBio(result);
    }
  });
  return () => {
    ignore = true;
  }
}, [person]);
```

- Always check whether you can reset all state with a key or calculate everything during rendering instead 
-  Props, state, and other values declared inside the component are reactive because they’re calculated during rendering and participate in the React data flow.

```jsx
 const onMessage = useEffectEvent(receivedMessage => {
    setMessages(msgs => [...msgs, receivedMessage]);
    if (!isMuted) {
      playSound();
    }
  });

  useEffect(() => {
    const connection = createConnection();
    connection.connect();
    connection.on('message', (receivedMessage) => {
      onMessage(receivedMessage);
    });
    return () => connection.disconnect();
  }, [roomId]);
```

# hooks
- Retain the data between renders
- Trigger React to render the component with new data (re-rendering)
- Rendering must always be a pure calculation
- This is because Hooks must only be called at the top-level of your component.

## useContext
- corresponding \<Context.Provider> needs to be above the component doing the useContext() call.
- React automatically re-renders all the children that use a particular context starting from the provider that receives a different value
- Skipping re-renders with memo does not prevent the children receiving fresh context values.
- useContext() always looks for the closest provider above the component that calls it. It searches upwards and does not consider providers in the component from which you’re calling useContext()
- You can override the context for a part of the tree by wrapping that part in a provider with a different value.

```jsx
<ThemeContext.Provider value="dark">
  ...
  <ThemeContext.Provider value="light">
    <Footer />
  </ThemeContext.Provider>
  ...
</ThemeContext.Provider>
```
- If you forget to specify value, it’s like passing value={undefined}.

## useMemo
- usually if calculation takes more than 1ms then do memoization
- if in dependency list there is some constant object or variable then on each rerender the useMemo dependency will change then no point of memoization
```js
function Dropdown({ allItems, text }) {
  const searchOptions = { matchMode: 'whole-word', text };

  const visibleItems = useMemo(() => {
    return searchItems(allItems, searchOptions);
  }, [allItems, searchOptions]); // 🚩 Caution: Dependency on an object created in the component body
  // ...
```
- here search options can it self be memoized or may be used in use ref
```js
function Dropdown({ allItems, text }) {
  const searchOptions = useMemo(() => {
    return { matchMode: 'whole-word', text };
  }, [text]); // ✅ Only changes when text changes
  ...
}
```
- since hooks doesn't works in loop so if want to use useMemo then create a new element inside the actual element 
```js
function ReportList({ items }) {
  return (
    <article>
      {items.map(item =>
        <Report key={item.id} item={item} />
      )}
    </article>
  );
}

function Report({ item }) {
  // ✅ Call useMemo at the top level:
  const data = useMemo(() => calculateReport(item), [item]);
  return (
    <figure>
      <Chart data={data} />
    </figure>
  );
}
```
## useCallback
- it memoizes the whole function rather than its output

## useDeferredValue
- when there are frequent state updates deferred value remains the initial but when the state update stops only then 
- similar functioning to debouncing but not exactly because it is non blocking
- **if React is in the middle of re-rendering a large list, but the user makes another keystroke, React will abandon that re-render, handle the keystroke, and then start rendering in the background again.**
```jsx
const [text, setText] = useState('');
  const deferredText = useDeferredValue(text);
  return (
    <>
      <input value={text} onChange={e => setText(e.target.value)} />
      <SlowList text={deferredText} />
    </>
  );
```

## useTransition
- If there are multiple ongoing Transitions, React currently batches them together. This is a limitation that will likely be removed in a future release.
- With a Transition, your UI stays responsive in the middle of a re-render
- isPending boolean value returned by useTransition to indicate to the user that a Transition is in progress.- under start transition everything must be synchronous , no settimeout, await ..
- The function you pass to startTransition does not get delayed. Unlike with the browser setTimeout, it does not run the callback later. React executes your function immediately, but any state updates scheduled while it is running are marked as Transitions.


```jsx
const [isPending, startTransition] = useTransition();
function selectTab(nextTab) {
    startTransition(() => {
      setTab(nextTab);
    });
  }
```

# react fiber
- react fiber is the actual node created in tree
```js
```



selected useId active useId
wrap in form
typeof ki jagah !!
i18nization
use svg in different files
css change 
critical rendering part a lot of css
use updater function more
event key press 
clean code

just hook for computation 
connection


//
kitna available hai, qr scan se


users - contact name address password - true false

last empty adding order
orderId,	userName,	userContact,	items,	status,	creationTime,	devlieryDate

https://script.google.com/macros/s/AKfycbywxqoMLTpIYIt0hGQeDzohrlhlVs9WbWWLKjx7_BJOrBvlkJttEF8IY2qrtbtisnjc7g/exec

https://script.google.com/macros/s/AKfycbywxqoMLTpIYIt0hGQeDzohrlhlVs9WbWWLKjx7_BJOrBvlkJttEF8IY2qrtbtisnjc7g/exec

search product name

i<10



        userEvent.hover(messageInChat);
        const messageDropdown = await screen.findByRole('message-dropdown');
        expect(messageDropdown).toBeInTheDocument();


        await userEvent.click(messageDropdown)