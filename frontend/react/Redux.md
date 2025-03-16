## Redux

参考文档：https://cn.redux.js.org/

Redux是一个用于管理javascript应用程序状态的可预测状态容器，它主要用于React应用，但是也可以和其他的视图库搭配使用如Vue。Redux的核心思想是将应用的所有状态集中存储在一个单一的store中，并且通过可预测的方式来更新这些状态。

### 1. 核心概念

1. Action(动作)
   
   Action是一个描述状态变化的普通javascript对象，它必须包含一个type属性，用于描述要执行的动作类型，还可以包含其他数据
   
   ```jsx
   // 定义一个 action
   const addTodo = {
     type: 'ADD_TODO',
     payload: 'Learn Redux'
   };
   ```

2. Reducer(纯函数)
   
   Reducer是一个纯函数，它接收当前的状态和一个action作为参数，并返回一个新的状态。Reducer负责根据action的类型来更新状态
   
   ```jsx
   // 初始状态
   const initialState = {
     todos: []
   };
   
   // reducer 函数
   const todoReducer = (state = initialState, action) => {
     switch (action.type) {
       case 'ADD_TODO':
         return {
           ...state,
           todos: [...state.todos, action.payload]
         };
       default:
         return state;
     }
   };
   ```

3. Store(状态容器)
   
   Store是一个对象，它保存了应用的所有状态，并提供了一些方法来管理状态。通过createStore函数创建一个store，该函数接收一个reducer作为参数
   
   ```jsx
   import { createStore } from 'redux';
   
   // 创建 store
   const store = createStore(todoReducer);
   ```

4. Dispatch(派发动作)
   
   Dispatch是一个方法，用于将action发送到store中，触发reducer执行
   
   ```jsx
   // 派发 action
   store.dispatch(addTodo);
   ```

5. Subscribe(订阅)
   
   Subscribe用于注册一个回调函数，当store中的状态发生变化时，该回调函数会被调用
   
   ```jsx
   // 订阅状态变化
   const unsubscribe = store.subscribe(() => {
     console.log('State updated:', store.getState());
   });
   
   // 取消订阅
   unsubscribe();
   ```

### 2. Redux的工作流程

1. **用户交互**：用户在界面上进行交互，触发一个action

2. **Dispatch Action**：通过dispatch方法将action发送到store

3. **Reducer更新状态**：store接收到action后，将当前状态和action传递给reducer，reducer根据action的类型返回一个新的状态

4. **状态更新**：store更新其内部的状态，并通知所有订阅者

5. **视图更新**：订阅者(通常是组件)接收到状态更新的通知后，更新界面

### 3. Redux的优缺点

#### 优点

1. **可预测性**：由于所有状态的变化都是通过reducer来处理，状态的变化是可预测的，便于调试和维护

2. **时间旅行调试**：可以记录和回放状态的变化，方便进行调试

3. **服务端渲染**：Redux可以很好的支持服务端渲染

#### 缺点

1. **代码冗余**：为了实现状态管理，需要编写大量的样板代码，如action、reducer等

2. **学习曲线陡峭**：对于初学者来说，理解redux的核心概念和工作流程可能需要一定的难度

### 4. Redux和React的结合

在React项目中使用Redux通常需要借助react-redux库，它提供了Provider和connect等工具，方便将Redux和React组件连接起来。

```jsx
import React from 'react';
import ReactDOM from 'react-dom/client';
import { createStore } from 'redux';
import { Provider } from 'react-redux';
import todoReducer from './reducers/todoReducer';
import App from './App';

// 创建 store
const store = createStore(todoReducer);

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <Provider store={store}>
    <App />
  </Provider>
);
```

在组价中使用connect函数来连接Redux的状态和动作

```jsx
import React from 'react';
import { connect } from 'react-redux';
import { addTodo } from './actions/todoActions';

const TodoList = ({ todos, addTodo }) => {
  return (
    <div>
      <ul>
        {todos.map((todo, index) => (
          <li key={index}>{todo}</li>
        ))}
      </ul>
      <button onClick={() => addTodo('New Todo')}>Add Todo</button>
    </div>
  );
};

const mapStateToProps = (state) => {
  return {
    todos: state.todos
  };
};

const mapDispatchToProps = (dispatch) => {
  return {
    addTodo: (todo) => dispatch(addTodo(todo))
  };
};

export default connect(mapStateToProps, mapDispatchToProps)(TodoList);
```


## Redux Toolkit

参考文档：https://toolkit.redux.js.cn/

Redux Toolkit是官方推荐的编写Redux逻辑的工具包，旨在简化Redux的使用。它与传统Redux存在多方面的不同

### 1. 代码的复杂度

### 2. 不可变数据的处理

### 3. 异步操作的处理

### 4. 配置和集成

## Redux Toolkit原理

Redux Toolkit是一个官方推荐的用于简化Redux开发的工具包，它的设计目标是让开发者能够轻松的编写Redux逻辑。主要可以从以下几个方面进行分析其原理：

### 1. createSlice原理

createSlice是Redux Toolkit中最常用的函数之一，它的主要作用是将action creators和reducers合并在一起创建。

### 2. createAsyncThunk原理

### 3. configureStore原理

### 4. Immer集成原理

关于immer的介绍，可参考[immer](./immer.md)

## Redux的使用场景(全局状态管理的使用场景)