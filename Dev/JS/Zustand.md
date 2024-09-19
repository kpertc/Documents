#web-dev 

Global State Management

Redux

- https://github.com/pmndrs/zustand
- https://zustand.docs.pmnd.rs/getting-started/introduction

```sh
npm i zustand
```

Tutorial: [[YouTube] Zustand - Complete Tutorial by Cosden Solutions](https://youtu.be/_ngCLZ5Iz-0?si=uh_-KhTyJq74RU3U)

### Create Store
`store.js`
```TypeScript
import { create } from "zustand"

type _storeType = {
    count: number
}

export const useStore = create<_storeType>(() => ({
    count: 0
}))
```

```jsx
export const useStore = create<_storeType>((set) => ({
    count: 0
    // function to update value
    increment: () => {
	    // set hard-coded value
	    set({ count: 1 })
	    // set value from pre value
	    set((state) => ({ count: state.count + 1}))
    }
	incrementAsync: async () => {
		...
	}
}))
```
### In react component
Get value
```TypeScript
import { useStore } from './store'

// start with `use` is a react hook, react will listen to the change
const count = useStore((state) => state.count);
```

use increment function
``` jsx
const increment = useStore((state) => state.increment)
...
<button onClick={increment}>incrementButton</button>
```

Best Practice
```js
// do -> the component only listen count
const count = useStore((state) => state.count)

// do not -> Less performance -> the component will listen to all `state`
const { count } = useStore((state) => state)
```

### Outside react component
```TypeScript
const _getCount = () => {
    const count = useStore.getState().count;
    console.log(count)
}

const _setCount = () => {
    useStore.setState({ count: 1 })
}
```
