#JavaScript  #TypeScript 

React 19
https://react.dev/learn

### React 19
- `use()` unwrap a promise or context during render
- Actions + `useActionState`, `useOptimistic`, `useFormStatus`
- ref as a prop → `forwardRef` deprecated
- `<Context>` works as the provider → `<Context.Provider>` deprecated
- `defaultProps` / `propTypes` removed on function components

### Tutorials
[[YouTube] React Tutorial for Beginners by Programming with Mosh](https://www.youtube.com/watch?v=SqcY0GlETPk)
[[YouTube] React JS Crash Course](https://www.youtube.com/watch?v=w7ejDZ8SWv8)
[[YouTube] React TypeScript Tutorial](https://www.youtube.com/watch?v=TiSGujM22OI&list=PLC3y8-rFHvwi1AXijGTKM0BKtHzVC-LSK&index=1)


Document Object Model (DOM)

- React (Library)
  ↳ Runtime virtual DOM, in memory, Lightweight
- Svelt 
  ↳ declarative code → compiler JavaScript
- Angular (Framework)
- Vue (Framework)

> [!NOTE] Library vs Framework
> Library - A tool that provides specific functionality
> Framework - A set of tools and guidelines for building apps- Routing, HTTP, app state, internationalization, form validation, animation ...

React is not platform specific
- Web → `react-dom` library, `ReactDom` virtual dom
- Apps → Build IOS, Android, Web APP with React → [[React Native]]

### Installation

Folder name can not have capital letters and space.

Init React-TS with Vite
`npm create vite@latest projectname -- --template react-ts`

react.dev now points to: Next.js, React Router, Expo (frameworks) / Vite, Parcel, Rsbuild (from scratch)

---
Deprecated — `create-react-app` was sunset Feb 2025 and removed from the docs
`npx create-react-app` need to specify a folder
`npx create-react-app .` Create React app in the folder, the folder should be empty.

Create react TypeScript template
`npx create-react-app react-typescript-demo --template typescript`

---
Recommend Tool:
Chrome Extension `React Developer Tools`

### Basics
-   Structure the "view" layer of your application
-   Reusable components with their own state
-   Interactive UIs with Virtual DOM
-   JSX - Dynamic markup
-   Performance & test
-   Popularity

JSX (JavaScript Syntax Extension)

UI as component

Components can have "state" which is an object that determines how a component renders and behaves.

### Basic Component

```jsx
const Header = ({ title = 'name' }) => { // capitalize → PascalCasing
    return (
        <header>
            <h1>{title}</h1>
        </header> 
    )
}
```

```tsx
<Header></Header>
// or
<Header /> // self close syntax
```

```JavaScript
// ≤ React 18 only — React 19 removed both on function components, they are now silently ignored
Header.defaultProps = {
    title: 'name'
}

// types in JavaScript
Header.propTypes = {
    title: PropTypes.string.isRequired
}

// React 19: default → ES6 default parameter `({ title = 'name' })`, types → TypeScript

export default Header
```

```jsx
const Button = ({ color, text }) => {
    const onClick = () => {
        console.log('click')
    }
    
    return (
        <button
            onClick={onClick}
            style = {{ background: color }}
            className = 'btn'
        >
         {text}
        </button>
    )
}
```
##### `React.Fragment`
``` jsx
	<React.Fragment>
		...
	</React.Fragment>

	// or shorthand
	<>
		...
	</>
```

##### Conditional Render
```jsx
{items.length === 0 ? <p>...</p> : null }
{items.length === 0 && <p>...</p> } // if true then render
```

##### key
when use JS to render a list of item by `array.map()`, child item needs `key={}` ==a string or a number== that uniquely identifies

> - Keys must be unique among siblings.
> - Keys must not change
> - React will use `index` by default if you don't specify a `key`
> - https://react.dev/learn/rendering-lists#rules-of-keys

``` jsx
// render a list
{items.map(item => (
	<li key={item}>{item}</li>
))}
```

### React Hooks
are functions that let us **hook** into the **React** state and lifecycle features from function components
-   **useState** - Return a stateful value and a function to update it
-   **useEffect** Perform side effects in function components
-   useContext, useReducer, useRef
- 
### useState
setState will re-render the component
```JavaScript
function App() {
    const [count, setCount] = useState(4)
    // first is value, second is function
    
    return (    
    )
}
```
##### Updater Function
```js
// update value
<button onClick={() => setCount(count + 1)}>
<button onClick={() => setCount(prevCount => prevCount + 1)}> // prevCount is pending state not current state

// update object with pending state, naming convention → first letter
<button onClick={(event) => setObject(o => ({ ...o, property: event.target.value }))}> // ({ }) wrapper is required, otherwise the braces read as a function body

// update array, always immutable, never a.push() then setArray(a)
<button onClick={()=> setArray(a => [...a, item])}>                                      // append
<button onClick={()=> setArray(a => a.filter(x => x.id !== id))}>                        // remove
<button onClick={()=> setArray(a => a.map(x => x.id === id ? {...x, done: true} : x))}>  // update
```
### useEffect
```JavaScript

// run every time when the component update
useEffect( () => {...} )

// blank [], will run once when component start
// dev + StrictMode runs it twice (mount → unmount → remount) by design, write the cleanup so the double-run is harmless
useEffect( () => {...}, [] )

// update, when variable changes
const variable
useEffect( () => { ... }, [variable] )
```

Return -> clean up function

``` typescript
useEffect( () => {
	console.log('resource changed');

	return () => {
		console.log('return from resource change')
	}

}, [resourceType])
```

### [useRef](https://youtu.be/t2ypzz6gJm0)
useState will re-render
useRef will not re-render

Reference a value
```ts
const renderCount = useRef(1) // ref -> 1

useEffect(() => {
    renderCount.current = renderCount.current + 1
})
```

Reference object
```jsx
const inputRef = useRef(); // inputRef.current = <input> element

return (
	<input ref={inputRef} /> 
)
```

### useContext
```TypeScript
export var ThemeContext = createContext(_sceneManager); // init value

return (
    <ThemeContext.Provider value={_sceneManager}>
    ...
    </ThemeContext.Provider>
)
```

In Function Component
```JavaScript
import { useContext } from "react";
import { ThemeContext } from "path";

const _sceneManager: SceneManager = useContext(ThemeContext)!;
```
### [useMemo](https://youtu.be/THL1OPn72vo) 
Memo -> Memorization, will not re-process until dependencies change
```ts
const doubleNumber = useMemo(()=>{
		return slowFunction(number)
	},
	[number] // dependency
)
```

use in react-three-fiber to store position heavy calculation
```jsx
const positions = useMemo(() => {
    const positions = new Float32Array(verticesCount * 3)
    
    for(let i = 0; i < verticesCount * 3; i++)
        positions[i] = (Math.random() - 0.5) * 3
    
    return positions
}, [])
```

### useCallback
`useCallback(fn, deps)` returns a stable **function identity** across renders, so `React.memo` children don't re-render and effect dependency arrays don't re-fire
``` js
const handleClick = useCallback(() => {
	doSomething(id)
}, [id])
```

### `<Suspense />`

Lazy loading
https://react.dev/reference/react/Suspense

```JavaScript
// fallback elements
<Suspense
    fallback={ 
        <> 
        ...
        </> 
    }
>
    .... Long time e.g. Loading model
</Suspense>
```

### Class

Previously, ONLY class based component could have STATE in a component. This is no longer the case since React Hooks. Functional Components to the Rescue!

```jsx
import { Component } from 'react'

export default class App extends Component {
    render() {
        return (
        <div>...</div>
        )
    }
}
```

class reserved for class -> class -> className

```jsx
export default class AppClass extends Component {

	constructor(props) {
		super(props);
		this.state = {
			name: "",
			age: 100,
			isMale: true,
		};
	}

	// this.setState({ age: 101 })  // only inside methods, never in the class body

	render() {

		// const { name, age, isMale } = this.state;
		
		return (
			<div>
				<h1>My name is {this.state.name}</h1>
				<h2>I am {this.state.age} years old</h2>
				<h3>I am a {this.state.isMale ? "Male" :"Female"}</h3>
			
			</div>
		)
	}
}
```


**React-route package**

`react-router-dom` — v7 (Nov 2024): most APIs now import from `react-router`

`<Switch />` use prior to React Router v6, Now it is replaced by `<Routes />`

v6.4+ / v7: data router `createBrowserRouter` with `loader` / `action`, the pattern to reach for now instead of bare `<Routes>`