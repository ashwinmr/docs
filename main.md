# General

## Temp

## JS

### Formatting strings
- You can use [template strings](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals) to output data
- But you cant use this to format numbers. You have to use functions to do that.

### Destruct without declaring
- When destructing without a declration such as `let` or `var` you need to enclose the statement in parenthesis so that js does not confuse the braces for a block.
```js
({val1, val2} = func())
```

### Export and import modules
[Stack overflow answer](https://stackoverflow.com/questions/33611812/export-const-vs-export-default-in-es6)

[Complete ES6 Export Explanation](https://developer.mozilla.org/en-US/docs/web/javascript/reference/statements/export)

- `export { functionName }` is equalent to `export const function functionName() { implementation }`

### General

- `==` checks if values are equal. `===` checks if values are equal and of same type.

## Css
### Flex align
- justify-content along primary axis
- align-items along secondary axis

### Flex scroll
- If a parent without a fixed size has a child that needs to scroll
    - The parent has to have display `flex`
    - The parent has to have overflow hidden
    - The child has to have size as `100%` of parent.

## Bootstrap

### Flex
- Start with a container
- Container should have rows
- Rows should have columns
- Columns can have stuff.
- Columns should have containers if they need rows again.
    - Otherwise the rows have to be margin 0 and cols have to be padding zero.
- `flex-grow-1` will grow in the direction of the parent flex (`flex-column` or `flex-row`)
    - Rows are flex-rows by default.
- When you want to `flex-grow-1` a row, it will only work if it's parent is a `d-flex flex-column`

## React

### Optimization
Details can be found [here](https://www.developerway.com/posts/react-re-renders-guide)
- A rerender is when the render function of a component is called. A DOM update is when the real DOM is changed.
    - Once rendering is done, react compares the virtual DOM to the real DOM and only updates the parts that have changed.
    - Just because a component rerenders doesn't mean the real DOM is changed.
    - There is no need to optimize this since it is taken care of by react.
- Rerenders can be optimized.
- A rerender is caused under the following conditions
    - A component is rerendered when its state changes.
    - All the children of the component are rerendered when the component rerenders.
    - When context changes all components that use the context rerender.
    - When hooks change the component that has the hook is rerendered.
    - A component does `not` rerender because its props change. It just happens to rerender since props change when the state from which the prop is derived changes and that triggers a rerender of the parent which rerenders the children.
- A rerender of a parent rerenders all children even if the props of some children have not changed. This is because react cannot assume that the children are pure components.
    - A pure component is one which does not have side effects and the same props always result in the same output.
- Therefore keep the state as close as possible to the component that uses it to prevent unnecessary render of its siblings.
- A rerender can also be prevented if the child component is a prop (through props or children) and not a regular child.
- A rerender can also be prevented by memoizing the component. Then react only rerenders if the memoized components props change.
    - In this case the component will rerender if its function props dont use `useCallback`, since a new function is created each time.
    - The memoization will also fail if the memoized component has a child component since that will be a new object each time. To prevent this, the child component has to be memoized but by using `usememo` (not `memo`).
    - Memoization can also fail if a callback has a dependancy that changed. So it is good to create callbacks with as few dependancies as possible. One way to do this is to use the `setState` function of a dependancy to get the current values of a state instead of directly listing the state as a dependancy.

### Dependencies
- When creating a `useCallback` function, make sure to also pass in any functions it uses as dependancy (unless the funtion is a `setState`).
    - If this is not done the callback will be calling functions that might have been replaced in the next render. It will still be using the old function that may be using old state.
### Update state
- Do not mutate state for updating. Instead clone and set state.
    - If you mutate that state and use the mutated object to set state, react might think that the object has not changed since the reference remains the same. Rerenders might not happen and cause strange bugs.
- Set state is asynchronous. Do not depends on it being run before code that follows it.

### Execution order
- Use effect runs after the first render and every time the state is updated.
### When to use what
- Data
    - If you need to save state while programming is running, `useState()`
    - If the data needs to be reloaded on restarting the program, use local storage.
    - If the data needs to be accessible in multiple components, use context.
- Functions
    - If it does not use any hooks, make it a regular function
    - If it uses hooks like `useState`, make it a hook

### Use state function input
- If there is an expensive computation to get the initial value of a state, you can input the function so that it is only called once to get the initial state.
    - If you were to make it part of the function, it will be called on every render for no reason.

### Change svg color
- Save svg copy as Optimized svg in inkscape.
- Edit the svg to have fill=`current` and stroke=`current` at the top level group.
- Import the svg as a component and set stroke and fill
```js
import { ReactComponent as Logo } from 'path/to/logo.svg'

<Logo width='35px' height='35px' stroke='color' fill='color' />
```


## Express

### Throwing errors
- Never throw errors from backend to frontend. Instead catch them and return an error response.
    - You can use `try catch` to handle the error response and then throw regular errors in the frontend if needed.

### Response codes
- 400: Bad request
- 401: Unauthorized
- 404: Not found


### Backend request guide
- `get` for read operations
  - Parameters for required inputs
  - Query for optional inputs
- `post` for update operations and hiding inputs

## Electron
### Napi Exception handling
Details can be found [here](https://github.com/nodejs/node-addon-api/blob/main/doc/error_handling.md)

- Enable cpp exceptions using in `bindings.gyp`
```js
`defines': ['NAPI_CPP_EXCEPTIONS']
```
- Disable cpp exceptions using
```js
'defines': ['NAPI_DISABLE_CPP_EXCEPTIONS'],
```

### Load svg in react
Details can be found [here](https://www.pluralsight.com/guides/how-to-load-svg-with-react-and-webpack)

### Saving svg for react
- Svg from inkscape won't work with react.
- You need to save a copy with the format `Optimized SVG`
  - Here you need to select the option `Remove Metadata`
- If you want to be able to modify the svg from react
    - Remove the `width` and `height` from svg tag.
    - Set all fills and strokes to `current`
    - Use `stroke = black` and `fill = none` as props in the react svg component.

### Throwing errors
- If you throw errors in the main process they get serialized by the time they are in the preload script
- You have to catch them in the preload script, get the message and throw a normal exception from preload which can be caught in render.
- Also note that invoke functions from render are async. Therefore, you have to await them if you want to catch an exception from them. 
    - It is enough to await them. You don't have to return anything to catch.

### Loading local resources
- Electron by default allows local resources to be accessed by render processes only when their html files are loaded from local sources with the `file://` protocol for security reasons.

### Context isolation, sandboxing and preload
- When context isolation and sandboxing is enabled (by default), the render process will not won't have Node.js enviornment initialized.
- The only way for it to call Node functions (from main process) is to use IPC from the preload script.
- The preload script also won't be able to use everything in Node, only a subset of functions and not even other custom scripts written by you.
    - So the only way to execute anything from preload is to send messages to the main process using IPC from preload. And then provide these functions that use IPC as an API to the renderer.
## D3 Js

### Capturing pointer events
- If you want two sibling elements to do some action for the same event, put them in a group and add the handler to the group.
    - The events from the siblings will bubble up to the group and be handled in one place.

## Visx

- Linepaths by default have a transparent fill which captures pointer events. Set the fill to `none` to prevent this.

## Digital Ocean

### Setup production server
[Guide](https://www.digitalocean.com/community/tutorials/how-to-set-up-a-node-js-application-for-production-on-ubuntu-20-04)
