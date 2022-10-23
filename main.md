# General

## Temp


# How To

# Language Guides

## JS

### Export and import modules
[Stack overflow answer](https://stackoverflow.com/questions/33611812/export-const-vs-export-default-in-es6)

### General

- `==` checks if values are equal. `===` checks if values are equal and of same type.

## Solidity

# Library Guides

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

## Electron

### Throwing errors
- Never throw errors from backend to frontend. Instead catch them and return an error message.
    - In the frontend, check error message and throw an error.

### Backend request guide
- `get` for read operations
  - Parameters for required inputs
  - Query for optional inputs
- `post` for update operations and hiding inputs

## D3 Js

