# redux-learning
Learning Redux witth simple To-Do application

## What is Redux ?
Redux is a JavaScript library that manages and centralizes application state. It's a predictable state container that helps developers write JavaScript apps that behave consistently across environments and are easy to test.

Redux itself is a `standalone library` that can be used with any UI layer or framework, including React, Angular, Vue, Ember, and vanilla JS. Although Redux and React are commonly used together, they are independent of each other. If you are using Redux with any kind of UI framework, you will normally use a `UI binding` library to tie Redux together with your UI framework, rather than directly interacting with the store from your UI code.

It's also stated in their official website that its a "Predictable state container for JS apps" not "React Apps". Visit official site [here](https://redux.js.org/)

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

## Folder Structure
```
.
├── ...
├── src
│   ├── app
│       └── store.js
│   ├── features
│       └── toDoSlice.js
│   ├── components
│       ├── AddTodo.jsx
│       └── Todo.jsx
│   └── ...
└── ...
```
