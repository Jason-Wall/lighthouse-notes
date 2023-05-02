# React Context API

https://github.com/gary-jipp/demo-react-context

- Prop drilling - Passing props waaaay down the tree so other components can use it. Considered bad form but it works.

  - Move state and functions to the closest ancestor and pass down to whoever needs it.

- react useContext - All child components are wrapped in the context of the parent. Anything you want to share with the children is available.
- Take your logic (manage state, actions to change state) and break it out into a custom hook.
- Convert into a context provider:

  - make a new folder src - `providers`
  - Save your hook to providers, rename file/ code instances to <Name>Provider - this will be very similar to a component.
  - Create context

  ```jsx
  import {createContext, useState} from 'react'

  export counterContext = createContext();
  // ... code, state, etc.

  const value = {foo, bar, more}//... all the state, fucntions, etc you want to share }
  return(
    <nameContext.Provider value = {value}>
      {props.children}
    </nameContext.Provider>
  )
  ```

- Now wrap any components you want to use this with `<NameProvider> tags`

  ```jsx
  <NameProvider>
    <App />
  </NameProvider>
  ```

- To use it:

```jsx
import {useContext} from 'react'
import {nameContext} from 'providers/NameProvider';

export defaul function Component(){
  const{foo, bar, more} = userContext(nameContext)
}

```

- Don't forget to wrap your components

- Consider conditional rendering instead of reactRouter?
