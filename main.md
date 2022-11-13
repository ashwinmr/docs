# General

## Temp

## JS

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


## React

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

### Throwing errors
- Never throw errors from backend to frontend. Instead catch them and return an error message.
    - In the frontend, check error message and throw an error.

### Loading local resources
- Electron by default allows local resources to be accessed by render processes only when their html files are loaded from local sources with the `file://` protocol for security reasons.

### Context isolation, sandboxing and preload
- When context isolation and sandboxing is enabled (by default), the render process will not won't have Node.js enviornment initialized.
- The only way for it to call Node functions (from main process) is to use IPC from the preload script.
- The preload script also won't be able to use everything in Node, only a subset of functions and not even other custom scripts written by you.
    - So the only way to execute anything from preload is to send messages to the main process using IPC from preload. And then provide these functions that use IPC as an API to the renderer.
## D3 Js

## Digital Ocean

### Setup production server
[Guide](https://www.digitalocean.com/community/tutorials/how-to-set-up-a-node-js-application-for-production-on-ubuntu-20-04)
