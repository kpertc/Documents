#JavaScript  #TypeScript 

https://reactjs.org/docs/hello-world.html

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
`npx create-react-app` need to specify a folder
`npx create-react-app .` Create React app in the folder, the folder should be empty.

Create react TypeScript template
`npx create-react-app react-typescript-demo --template typescript`

---
Init React-TS with Vite
`npm init vite@latest` `projectName` `-- --template react-ts`

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
const Header = () => { // capitalize → PascalCasing
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
Header.defaultProps = {
    title: 'name'
}

// types in JavaScript
Header.propTypes = {
    title: PropTypes.string.isRequired
}

export default Header
```

```jsx
const Button = ({ color, text }) => {
    const onClick = () => {
        console.log('click')
    }
    
    return (
        <button
            onClick = {onclick}
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
<button onClick={()=> setObject(o => ...o, property: event.target.value)>

// update array
<button onClick={()=> setArray()}>
```
 
### useEffect
```JavaScript

// run every time when the component update
useEffect( () => {...} )

// blank [], will run once when component start
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
const inputRef = useRef(); // inputRef = <input> element

return (
	<input ref={inputRef}> 
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
store a function?
``` js

```

### `<Suspense />`

Lazy loading
https://react.dev/reference/react/Suspense

```JavaScript
<Suspense
    {/* fallback elements */}
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
export default class App extends Component {
    render() {
        return {
        <div>...</div>
        }
    }
}
```

class reserved for class -> class -> className

```jsx
export default class AppClass extends Component {

	constructor(props) {
		super(props);
	}

	this.state = {
		name: "",
		age: 100,
		isMale: true,
	};

	this.setState ...

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

`react-router-dom`

`<Switch />` use prior to React Router v6, Now it is replaced by `<Routes />`