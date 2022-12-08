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

## Bootstrap

### Flex
- Start with a container
- Container should have rows
- Rows should have columns
- Columns can have stuff or more rows.
- When you want to `flex-grow-1` a row, it will only work if it's parent is a `d-flex flex-column`

## React

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
