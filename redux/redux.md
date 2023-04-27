# Redux

## What is Redux?

It helps to understand what this "Redux" thing is in the first place. What does it do? What problems does it help me solve? Why would I want to use it?

Redux is a pattern and library for managing and updating application state, using events called "actions". It serves as a centralized store for state that needs to be used across your entire application, with rules ensuring that the state can only be updated in a predictable fashion.

## Why Should I Use Redux?

Redux helps you manage "global" state - state that is needed across many parts of your application.

The patterns and tools provided by Redux make it easier to understand when, where, why, and how the state in your application is being updated, and how your application logic will behave when those changes occur. Redux guides you towards writing code that is predictable and testable, which helps give you confidence that your application will work as expected.

## Common Misconceptions

- Redux is not directly related to React in any way, it is just commonly used with React but the Redux library can be used in any JS UI library or even with just vanilla JS




## Splitting What Redux Gives You into 2 Categories
1. State Abtraction - Redux Offers the ability to abstract the state of your application into an isolated space in what is called a "store", to read a value of state it must be retrieved from the store.
2. Redux Pattern - A programming pattern for creating a "predictable" container for how state in your application changes.



## Understanding the Redux Pattern

The idea behind the Redux Pattern is that you have 3 main core features controlling how specific state changes.

When you want to change the value of state, you "dispatch" whats called an "action", an action is just a regular JS object that usually contains 2 properties, type an payload

The action is then sent to a function called a "reducer", the job of the reducer is to evaluate what "type" of action was dispatched, and perform the appropriate modifications to the state based on that type of action


The redux library introduces a lot of new terminology

- Actions - JS Objects which contain a type property and (optionally) a payload property
- Dispatch -  a function which sends an action to a state reducer
- Reducers - a function that looks at the action passed in as an argument and performs state mutations based on the value of the action "type" property
- Stores - The object which house the value of state/states, to read from state, it must be fetched from the store

## Overview

1. Learn the Redux Pattern using the base **Redux Library** with vanilla JavaScript
2. Learn **Redux Toolkit**, the new and recommended way to use Redux
3. Integration with React with the **React-Redux** Library
4. **RTK Query** extension, a query library for redux



## Using Base Redux

### Step 1: Create a node project and install the Redux library

```powershell

npm i redux

```

### Step 2: Create index.js and create your first action types as constant variables

The reason we put them in constants to avoid spelling mistakes later when we dispatch the action objects

```js


const redux = require('redux')

// Action Types, not action objects
const INCREMENT = 'INCREMENT'
const DECREMENT = 'DECREMENT'

// This is an action object,

{
    type: INCREMENT,
}

// We are going to dispatch this to the reducer


```

### Step 3: Create the intialState object an the reducer function


```js

const initialState = {
        value: 0
    }

// The reucer uses a switch statement to determine what the new state will be, based on what "type" of action was passed in
const reducer = (state = initialState, action) => {
  switch (action.type) {
    case INCREMENT: {
      return { value: state.value + 1 }
    }
    case DECREMENT: {
      return { value: state.value - 1 }
    }
    default: return state
  }
}


```


### Step 4: Import the redux library and create the store

```js
const redux = require('redux')


const store = redux.createStore(reducer) // Using the createStore method and passing our reducer as an arg

console.log(store.getState()) // Logging the initial state


const unsubscribe = store.subscribe(_ => console.log(store.getState())) // Creatinh a subscription to log the state anytime it changes

```


### Step 5: Dispatch an Action Object

```js


store.dispatch({type: INCREMENT})

// See state changes logged in console

```

```js

store.dispatch({type: INCREMENT})
store.dispatch({type: INCREMENT})
store.dispatch({type: INCREMENT})
store.dispatch({type: INCREMENT})
store.dispatch({type: DECREMENT})
store.dispatch({type: DECREMENT})

// See state changes logged in console, value should be 2

```
### Step 6: Action Creators

Action Creators are simply just functions that return an action object. It is recommended to use action created rather than passing an action into a dispatch directly beacuse if you make changes to a spceific action it must change anywhere that action is being dispatched, with action creators we can keep it in one function


```js
const increment = () => {
     return {
        type: INCREMENT
    }
}
const decrement = () => {
     return {
        type: DECREMENT
    }
}
store.dispatch(increment())
store.dispatch(increment())
store.dispatch(increment())
store.dispatch(decrement())
store.dispatch(decrement())
```



### Step 7: Sending Data in an Action with the Payload Property

Actions can optionally take another property, typically called "payload", which will carry data to the reducer

For example, if we wanted to turn our reducer into an Add/Subtract calculator which added or subtracted the value from what we send in the payload, we need to makea few changes to our reducer and action creators










7.1: Create new Action Type constants ADD and SUBTRACT

7.2: Create new action creators that now return an object with a property type AND payload. the AC takes in a argument which becomes the payload.

7.3: Change reducer to account for new types, instead of adding to the state by 1, have it add to the value within action.payload
```js
const ADD = 'ADD'
const SUBTRACT = 'SUBTRACT'

const add = (value) => {
     return {
        type: ADD,
        payload: value
    }
}
const subtract = (value) => {
     return {
        type: SUBTRACT,
        payload: value
    }
}

const reducer = (state = initialState, action) => {
  switch (action.type) {
    case INCREMENT: {
            return { value: state.value + 1 }
    }
    case DECREMENT: {
            return { value: state.value - 1 }
    }
    case ADD: {
      return { value: state.value + action.payload }
    }
    case SUBTRACT: {
      return { value: state.value - action.payload }
    }
    default: return state
  }
}



```


### Step 8: Dispatching Actions With Payloads


```js

store.dispatch(add(5))
store.dispatch(add(5))
store.dispatch(add(5))
store.dispatch(add(5))
store.dispatch(add(5))
store.dispatch(subtract(5))
store.dispatch(subtract(5))
store.dispatch(subtract(5))


```


### Step 9: Multiple Reducers & TODO Project Prep

We gonna create a whole seperate reducer for managing a state of todos, with the combineReducers method we can combine multiple reducers into a single 
"root reducer" which we can then pass as an argument into our store. First lets create our todoReucer and change the name of our calculator from reducer to calcReducer


```js


const todoReducer = (state = [], action) => {
        switch(action.type){
                default: return state
            }
    }

const calcReducer = (state = initialState, action) => {
  switch (action.type) {
    case INCREMENT: {
            return { value: state.value + 1 }
    }
    case DECREMENT: {
            return { value: state.value - 1 }
    }
    case ADD: {
      return { value: state.value + action.payload }
    }
    case SUBTRACT: {
      return { value: state.value - action.payload }
    }
    default: return state
  }
}
const rootReducer = combineReducers({
    todos: todoReducer,
    calc: calcReducer
    })

const store = redux.createStore(rootReducer)
```


Now create Action Type constants: ADDTODO, MARKCOMPLETE, DELETETODO, EDITTODO and their action creators

```JS

const ADDTODO = 'ADDTODO'
const MARKCOMPLETE = 'MARKCOMPLETE'
const DELETETODO = 'DELETETODO'
const EDITTODO = 'EDITTODO'


const addTodo = (todo) => {
  return {
    type: ADDTODO,
    payload: todo
  }
}
const markComplete = (id) => {
  return {
    type: MARKCOMPLETE,
    payload: id
  }
}

const deleteTodo = (id) => {
  return {
    type: DELETETODO,
    payload: id
  }
}

const editTodo = (payload) => {
  return {
    type: EDITTODO,
    payload
  }
}

```


### Step 10: Todo Project


Prompt: Your job is to create redux reducer to manage the state of an array of todo objects, the schema of the state should be as follows

```ts

type TodoState = {
    todos: {
        id: number,
        body: string
        completed: boolean
    }[]
}
```
Your reducer should add new todos, mark a single todo as complete, delete a single todo, and edit the body of a single todo



SOLUTION:

```js
const ADDTODO = 'ADDTODO'
const MARKCOMPLETE = 'MARKCOMPLETE'
const DELETETODO = 'DELETETODO'
const EDITTODO = 'EDITTODO'


const addTodo = (todo) => {
  return {
    type: ADDTODO,
    payload: todo
  }
}
const markComplete = (id) => {
  return {
    type: MARKCOMPLETE,
    payload: id
  }
}

const deleteTodo = (id) => {
  return {
    type: DELETETODO,
    payload: id
  }
}

const editTodo = (payload) => {
  return {
    type: EDITTODO,
    payload
  }
}

const todoReducer = (state = { todos: [] }, action) => {
  switch (action.type) {
    case ADDTODO: {
      return {
        ...state,
        todos: [...state.todos, action.payload]
      }
    }
    case MARKCOMPLETE: {
      return {
        ...state,
        todos: state.todos.map(todo => todo.id === action.payload ? { ...todo, completed: true } : todo)
      }
    }
    case DELETETODO: {
      return {
        ...state,
        todos: state.todos.filter(todo => todo.id !== action.payload)
      }
    }
    case EDITTODO: {
      const { id, body } = action.payload
      return {
        ...state,
        todos: state.todos.map(todo => {
          if (todo.id === id) {
            return {
              ...todo,
              body: body
            }
          }

          return todo
        })
      }
    }
    default: return state
  }

}


store.dispatch(addTodo({ id: store.getState().todo.todos.length + 1, body: 'get groceries', completed: false }))
store.dispatch(addTodo({ id: store.getState().todo.todos.length + 1, body: 'get groceries', completed: false }))
store.dispatch(addTodo({ id: store.getState().todo.todos.length + 1, body: 'get groceries', completed: false }))
store.dispatch(addTodo({ id: store.getState().todo.todos.length + 1, body: 'get groceries', completed: false }))
store.dispatch(addTodo({ id: store.getState().todo.todos.length + 1, body: 'get groceries', completed: false }))
store.dispatch(addTodo({ id: store.getState().todo.todos.length + 1, body: 'get groceries', completed: false }))
store.dispatch(addTodo({ id: store.getState().todo.todos.length + 1, body: 'get groceries', completed: false }))
store.dispatch(addTodo({ id: store.getState().todo.todos.length + 1, body: 'get groceries', completed: false }))
store.dispatch(markComplete(8))
store.dispatch(markComplete(5))
store.dispatch(markComplete(3))
store.dispatch(deleteTodo(3))
store.dispatch(deleteTodo(5))
store.dispatch(editTodo({ id: 8, body: 'eat potato' }))
store.dispatch(editTodo({ id: 4, body: 'eat potato' }))
store.dispatch(editTodo({ id: 1, body: 'eat potato' }))



```


## Redux Toolkit Intro

Redux Toolkit is the new recommended way to use the redux library. It was created to solve the following issues with the base redux 

"Configuring a Redux store requires too much boilerplate code"
- Action Types
- Action Creators
- Control Flow (switch/if) inside of Reducer
        
"I have to add a lot of packages to get Redux to do anything useful"

- Immer
- Redux-Thunk
- Redux-Devtools
    


Redux Toolkit was created to help solve these common complaints and improve the DX


### Step 1: Installing Redux Toolkit


```bash

npm i @reduxjs/toolkit

```





### Step 2: Creating a Slice

A Slice in redux is basically the combination of a reducer and all of its actions inside a single object

What we are going to do is create our calcReducer and todoReducer with Redux Toolkit


RTK uses the Immer library to allow the usage of impure operations, but under the hood, its still pure. With RTK, you can modify state directly within the reducer.




```js

const { configureStore, createSlice } = require('@reduxjs/toolkit')

const calcSlice = createSlice({
        name: 'calc',
        initialState: {
                value: 0
            },
            reducers: {
                    increment: (state, action) => {
                            state.value++
                        },
                    decrement: (state, action) => {
                            state.value--
                        },
                    subtract: (state, action) => {
                            state.value += action.payload
                        },
                    add: (state, action) => {
                            state.value += action.payload
                        }
                }
    })


export const {increment, decrement, add, subtract} = calcSlice.actions

export const calcReducer = calcSlice.reducer

```


### Step 3: Configuring the Store with RTK

```js


const store = configureStore({
  reducer: {
    calc: calcReducer
  }
})

store.subscribe(_ => console.log(store.getState()))



store.dispatch(increment())
store.dispatch(increment())
store.dispatch(increment())
store.dispatch(increment())


```

### Step 4: RTK Todo Implementation


```js



const todoSlice = createSlice({
  name: 'todo',
  initialState: {
    todos: [],
    count: 0
  },
  reducers: {
    addTodo: (state, action) => {
      state.todos.push(action.payload)
      state.count++
    },
    deleteTodo: (state, action) => {
      state.todos = state.todos.filter(todo => todo.id !== action.payload)
      state.count--

    },
    markComplete: (state, action) => {
      const todo = state.todos.find(todo => todo.id === action.payload)
      todo.complete = true

    },
    editTodo: (state, action) => {
      const todo = state.todos.find(todo => todo.id === action.payload.id)

      todo.body = action.payload.body
    }

  }
})

const { addTodo, deleteTodo, markComplete, editTodo } = todoSlice.actions
const todoReducer = todoSlice.reducer
const store = configureStore({
  reducer: {
    calc: calcReducer,
    todo: todoReducer
  }
})

store.subscribe(_ => console.log(store.getState().todo))



store.dispatch(increment())
store.dispatch(increment())
store.dispatch(increment())
store.dispatch(increment())
store.dispatch(addTodo({ id: store.getState().todo.todos.length + 1, body: 'yuh', complete: false }))
store.dispatch(addTodo({ id: store.getState().todo.todos.length + 1, body: 'yuh', complete: false }))
store.dispatch(addTodo({ id: store.getState().todo.todos.length + 1, body: 'yuh', complete: false }))
store.dispatch(addTodo({ id: store.getState().todo.todos.length + 1, body: 'yuh', complete: false }))
store.dispatch(addTodo({ id: store.getState().todo.todos.length + 1, body: 'yuh', complete: false }))
store.dispatch(deleteTodo(5))
store.dispatch(markComplete(4))
store.dispatch(editTodo({ id: 4, body: 'fuckkkkkk' }))

```


### Step 5: Extra Reducers

The extraReducers property is needed is you need the reducer to react to actions that arent generated directly from the slice. For example, lets say we have two slices, one for number of cakes in stock and the other for ice cream. Let's say we wanted whenever we sold a cake for us to also give away an ice cream, we can accomplish this with extraReducers



```js

const { configureStore, createSlice } = require('@reduxjs/toolkit')

const cakeSlice = createSlice({
  name: 'cake',
  initialState: {
    cakes: 5
  },
  reducers: {
    sellCake: (state) => {
      state.cakes--
    }
  }
})

const iceCreamSlice = createSlice({
  name: 'cake',
  initialState: {
    iceCreams: 5
  },
  reducers: {
    sellIceCream: (state) => {
      state.cakes--
    }
  },
  extraReducers: (builder) => {
    builder.addCase(cakeSlice.actions.sellCake, (state, action) => {
      state.iceCreams--
    })
  }
})
const store = configureStore({
  reducer: {
    cake: cakeSlice.reducer,
    iceCream: iceCreamSlice.reducer
  }
})

store.subscribe(_ => console.log(store.getState()))


store.dispatch(cakeSlice.actions.sellCake())
store.dispatch(cakeSlice.actions.sellCake())
store.dispatch(cakeSlice.actions.sellCake())


```


### Step 6: Async Thunks & createAsyncThunk

#### What is a "thunk"?

The word "thunk" is a programming term that means "a piece of code that does some delayed work". Rather than execute some logic now, we can write a function body or code that can be used to perform the work later.

For Redux specifically, "thunks" are a pattern of writing functions with logic inside that can interact with a Redux store's dispatch and getState methods.

#### What is createAsyncThunk

createAsyncThunk is a function that accepts a Redux action type string and a callback function that should return a promise. It generates promise lifecycle action types based on the action type prefix that you pass in, and returns a thunk action creator that will run the promise callback and dispatch the lifecycle actions based on the returned promise.

This abstracts the standard recommended approach for handling async request lifecycles.

It does not generate any reducer functions, since it does not know what data you're fetching, how you want to track loading state, or how the data you return needs to be processed. You should write your own reducer logic that handles these actions, with whatever loading state and processing logic is appropriate for your own app.



```js

const fetchPosts = createAsyncThunk('posts/fetchposts', async () => {
  const res = await axios.get('https://jsonplaceholder.typicode.com/posts')

  const posts = res.data

  return posts.slice(0, 5).map(post => ({ title: post.title }))

})

const fetchPostById = createAsyncThunk('posts/fetchPostById', async (id) => {
  const res = await axios.get('https://jsonplaceholder.typicode.com/posts/' + id)

  const post = res.data

  return post

})
const postsSlice = createSlice({
  name: 'posts',
  initialState: {
    isLoading: false,
    isSuccess: false,
    isError: false,
    data: [],
    message: ''
  },
  reducers: {
    reset: (state) => {
      state.isLoading = false,
        state.isSuccess = false,
        state.data = [],
        state.message = '',
        state.isError = false
    }
  },
  extraReducers: (builder) => {
    builder.addCase(fetchPosts.pending, fetchPostById.pending, (state) => {
      state.isLoading = true
      state.isSuccess = false
      state.isError = false


    })
    builder.addCase(fetchPosts.fulfilled, (state, action) => {
      state.isLoading = false
      state.isSuccess = true
      state.isError = false
      state.data = action.payload

    })
    builder.addCase(fetchPosts.rejected, (state, action) => {
      console.log(action)
      state.isLoading = false
      state.isSuccess = false
      state.isError = true
      state.message = action.error.message
    })
    builder.addCase(fetchPostById.pending, (state, action) => {
      state.isLoading = true
      state.isError = false
      state.isSuccess = false
    })
    builder.addCase(fetchPostById.rejected, (state, action) => {
      state.isLoading = false
      state.isError = true
      state.isSuccess = false
      state.message = action.error.message
    })
    builder.addCase(fetchPostById.fulfilled, (state, action) => {
      state.isLoading = false
      state.isError = false
      state.isSuccess = true
      state.message = 'Single Post Retrieved',
        state.data = action.payload
    })
  }
})
const store = configureStore({
  reducer: {
    posts: postsSlice.reducer
  }
})

store.subscribe(_ => console.log(store.getState().posts))


store.dispatch(fetchPostById(3))




```
