# redux-learning
Learning Redux witth simple To-Do application

## What is Redux ?
Redux is a JavaScript library that manages and centralizes application state. It's a predictable state container that helps developers write JavaScript apps that behave consistently across environments and are easy to test.

Redux itself is a `standalone library` that can be used with any UI layer or framework, including React, Angular, Vue, Ember, and vanilla JS. Although Redux and React are commonly used together, they are independent of each other. If you are using Redux with any kind of UI framework, you will normally use a `UI binding` library to tie Redux together with your UI framework, rather than directly interacting with the store from your UI code.

It's also stated in their official website that its a `Predictable state container for JS apps` not `React Apps`. Visit official site [here](https://redux.js.org/)

![image](https://github.com/akshayxemo/redux-learning/assets/83893825/01dd5b0b-c99c-40e8-ba6c-651b30eee01c)

## What is Redux-Toolkit (RTK) ?
Redux Toolkit (RTK) is a library that provides tools and conventions for writing Redux logic. It's a recommended approach for writing Redux logic and is often used with React, but can also be used with other JavaScript frameworks. RTK includes utilities that help simplify many common use cases, including store setup, creating reducers and writing immutable update logic, and even creating entire "slices" of state at once.

The `@reduxjs/toolkit` package wraps around the `core redux` package, and contains API methods and common dependencies that we think are essential for building a Redux app. Redux Toolkit builds in our suggested best practices, simplifies most Redux tasks, prevents common mistakes, and makes it easier to write Redux applications.

## What is React-Redux ?
React Redux is the official React UI bindings layer for Redux. It lets your React components read data from a Redux store, and dispatch actions to the store to update state. It's helps your react app to establish connection with redux-toolkit.

# Lets See how to get started ?
Check out the original [documentation](https://redux.js.org/introduction/getting-started) for more details. I am using React and NPM package manager. If you use any other pakage manager then check out the documentation.

# Installation
## Redux-toolkit
```
npm install @reduxjs/toolkit
```
## React-Redux
```
npm install react-redux
```

## My Folder Structure
```
.
├── ...
├── src
│   ├── app
│       └── store.js            # Main Storage
│   ├── features
│       └── todo
│           └── todoSlice.js    # Reducers definitions
│   ├── components
│       ├── AddTodo.jsx         # components where we will use the methods declared in slice reducers
│       └── Todo.jsx
│   ├── App.jsx
│   ├── App.css
│   ├── index.css
│   ├── Main.jsx
│   └── ...
└── ...
```

**A application only contains one store that is the best practice.** 

> Only four things to remember : `Store` `Reducers` `useSelector` `useDispatch`

Methods Require :
> 1. `configureStore` from `@reduxjs/toolkit` to initially configure the store
> 2. `createSlice` from `@reduxjs/toolkit` to create Slices
> 3. `nanoid` from `@reduxjs/toolkit` to generate random unique ID

## Code snippets
Configuring the initial store which stores the states related to todo application.
### store.js
```
import {configureStore} from '@reduxjs/toolkit'
import todoReducer from '../features/todo/todoSlice'

export const store = configureStore({
    reducer: todoReducer
})
```

Configuring the initial state and the todo slice. there can be more than one slice as well. In this slice we can see that there are two things we are using `state` and `action` in the callback function in reducers in the todo slice. 

`state` : this stores the initial state ( it is an object and can contain multiple values ). Each time state passes to the callback means it passes all the values that are currently stored in the state.

`action` : an action parameter refers to a plain JavaScript object that represents an intention to change the state. Think of Redux actions as messengers that deliver information about events happening in your app to the Redux store. It contains payload which contains the message or data that has been dispatched.

### todoSlice.js
```
import {createSlice, nanoid} from '@reduxjs/toolkit';

/* configuring initial state */
const initialState = {
  todos: [{id:1, text:'hello world'}]
};

export const todoSlice = createSlice({
  name: 'todo',
  initialState,
  reducers: {
    addTodo:(state, action)=>{
      const todo = {
        id: nanoid(),
        text: action.payload
      };
      state.todos.push(todo);
    },
    removeTodo: (state, action)=>{
      state.todos = state.todos.filter((todo)=>{
        todo.id !== action.payload
      })
    }
  }
});

export const {addTodo, removeTodo} = todoSlice.action;
export default todoSlice.reducer;
```
**we have to export all individual reducers and also a main reducer source which is a default export that is been used in the store.js to store the state.**

## how to use this Reducers
For adding the todo then use `addTodo` reducer and `useDispatch` method from 'react-redux'

### AddTodo.jsx
```
import {useDispatch} from 'react-redux'
import {addTodo} from '../feature/todo/todoSlice'

export default const AddTodo = ()=>{
    const[input, setInput] = useState('');
    const dispatch = useDispatch();
    const addTodoHandler = (e)=>{
        e.preventDefault();
        dispatch(addTodo(input));
        setInput('');
    }

    return <>
        <form onsubmit={addTodoHandler}>
            <input name="text" value={input} onchange={(e)=>{setInput(e.target.value)}}/>
            <button type="submit">Add todo</button>
        </form>
    </>
}

```
### Todo.jsx
```
import {useSelector, useDispatch} from 'react-redux'
import {removeTodo} from '../feature/todo/todoSlice'

export default const Todo = ()=>{
    const todos = useSelector(state => state.todos);
    const dispatch = useDispatch();

    return <>
        <div>Todos</div>
        {todos.map((todo)=>{
            return <li key={todo.id}>
                {todo.text}
            <button
            onclick={()=>{dispatch(removeTodo(todo.id))}}>
            X</button>
            </li>
        }
    </>
}

```
### App.jsx
```
import AddTodo from '../components/AddTodo';
import Todo from '../components/Todo';
import './App.css';

export default const App = ()=>{
    return <>
        <div>TODO LITS</div>
        <div>
        <AddTodo/>
        <Todo/>
        </div>
    </>
}
```

> Now Wrap everything in `Provider` from 'react-redux' and pass the store props
### Main.jsx
```
import React from 'react';
import ReactDom from 'react-dom/client';
import './App.jsx'
import './index.css'
import {Provider} from 'react-redux';
import {store} from './app/store';

ReactDom.createRoot(document.getElementById('root')).render(
    <React.StrictMode>
        <Provider store={store}>
            <App/>
        </Provider>
    </React.StrictMode>

```
This tutorial is given in this [youtube video](https://youtu.be/1i04-A7kfFI?si=pNHpxLO5ussLTz73) by [Hitesh Choudhary](https://github.com/hiteshchoudhary/) `channel Name: 
Chai aur Code`
