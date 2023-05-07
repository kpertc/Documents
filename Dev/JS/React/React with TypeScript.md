#JavaScript  #TypeScript 

https://reactjs.org/docs/hello-world.html

### Tutorials

[[YouTube] React JS Crash Course](https://www.youtube.com/watch?v=w7ejDZ8SWv8)

[[YouTube] React TypeScript Tutorial](https://www.youtube.com/watch?v=TiSGujM22OI&list=PLC3y8-rFHvwi1AXijGTKM0BKtHzVC-LSK&index=1)

Build IOS, Android, Web APP with React → [[React Native]]


<br>


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

```JavaScript
const Header = () => {
    return (
        <header>
            <h1>{title}</h1>
        </header> 
    )
}
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

```JavaScript
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

  

### **React Hooks**

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

### useEffect

```JavaScript
useEffect( () => {...}, [] )
// { ... } will execute when [] matched value changed

const 111
useEffect( () => { console.log('') }, [111] )
// if 111 changed, console.log('') will be executed
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

```JavaScript
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

### [useMemo](https://youtu.be/THL1OPn72vo) (Memo -> Memorization)

<br>

### Class

Previously, ONLY class based component could have STATE in a component. This is no longer the case since React Hooks. Functional Components to the Rescue!

```JavaScript
export default class App extends Component {
    render() {
        return {
        <div>...</div>
        }
    }
}
```


class reserved for class -> class -> className

```JavaScript
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