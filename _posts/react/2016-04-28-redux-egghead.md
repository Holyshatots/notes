---
layout: note
title: Redux Tutorial egghead.io
date: 2016-04-28 12:29:12 -0700
categories: react
---

### 5 Writing a Counter Reducer with Tests

A counter with ES6 javascript

```
const counter = (state = 0, action) => {
  switch(action.type) {
    case 'INCREMENT':
      return state + 1;
    case 'DECREMENT':
      return state - 1;
    default:
      return state;
  }
}

expect(
  counter(0, { type: 'INCREMENT' })
  ).toEqual(1);

expect(
  counter(1, { type: 'INCREMENT' })
).toEqual(2);

expect(
  counter(2, { type: 'DECREMENT' })
).toEqual(1);

expect(
  counter(1, { type: 'DECREMENT' })
).toEqual(0);

expect(
  counter(1, { type: 'SOMETHING_ELSE' })
).toEqual(1);

expect(
  counter( undefined, {})
).toEqual(0);

```

### 6 Store Methods

```
const counter = (state = 0, action) => {
  switch(action.type) {
    case 'INCREMENT':
      return state + 1;
    case 'DECREMENT':
      return state - 1;
    default:
      return state;
  }
}

const { createStore } = Redux;
const store = createStore(counter);

const render = () => {
  document.body.innerText = store.getState();
};

store.subscribe(render);
render();

document.addEventListener('click',  () => {
  store.dispatch({ type: 'INCREMENT' });
});


```

### 9 Avoiding Array Mutations with concat(), slice(), and ..spread

```

const addCounter = (list) => {
  return [...list, 0];
};

const removeCounter = (list, index) => {
  return [
    ...list.slice(0, index),
    ...list.slice(index + 1)
  ];
};

const incrementCounter = (list, index) => {
  return [
  ...list.slice(0, index),
  list[index] + 1,
  ...list.slice(index + 1)
  ];
};

const testAddCounter = () => {
  const listBefore = [];
  const listAfter = [0];

  deepFreeze(listBefore);

  expect(
    addCounter(listBefore)
  ).toEqual(listAfter);
};

const testRemoveCounter = () => {
  const listBefore = [0, 10, 20];
  const listAfter = [0, 20]

  deepFreeze(listBefore);

  expect(
    removeCounter(listBefore, 1)
  ).toEqual(listAfter);
};

const testIncrementCounter = () => {
  const listBefore = [0, 10, 20];
  const listAfter = [0, 11, 20];

  deepFreeze(listBefore);

  expect(
    incrementCounter(listBefore, 1)
  ).toEqual(listAfter);
};

```

### 10 Avoiding Object Mutations with Object.assign() and ..spread

```

const toggleTodo = (todo) => {
  return Object.assign({}, todo, {
      completed: !todo.completed
    });
};

const testToggleTodo = () => {
  const todoBefore = {
    id: 0,
    text: 'Learn Redux',
    completed: false
  };
  const todoAfter=  {
    id: 0,
    text: 'Learn Redux',
    completed: true
  };

  deepFreeze(todoBefore);

  expect(
    toggleTodo(todoBefore)
    ).toEqual(todoAfter);
};

testToggleTodo();
console.log('All tests passed');

```

### 11 - 19 Writing a Todo List Reducer

```
const todo = (state, action) => {
  switch (action.type) {
    case 'ADD_TODO':
      return {
        id: action.id,
        text: action.text,
        completed: false
      };
    case 'TOGGLE_TODO':
      if(state.id !== action.id) {
        return state;
      }

      return {
        ..state,
        completed: !state.completed
      };
    default:
      return state;
  }
}


const todos = (state = [], action) => {
  switch (action.type) {
    case 'ADD_TODO':
      return [
        ...state,
        todo(undefined, action)
      ];
    case 'TOGGLE_TODO':
      return state.map(todo => {
        return state.map(t => todo(t, action));
      });
    default:
      return state;
  }
};

const visiblityFilter = (
  state = 'SHOW_ALL',
  action
) => {
  switch (action.type) {
      case 'SET_VISIBILTY_FILTER':
        return action.filter;
      default:
        return state;
  }
};


const { combineReducers } = Redux;
const todoApp = combineReducers({
  todos,
  visibilityFilter
});

/*
const todoApp = (state = {}, action) => {
  return {
    todos: todos(
      state.todos,
      action
    ),
    visibilityFilter: visibilityFilter(
      state.visibilityFilter,
      action
    )
  };
};
*/

const testAddTodo = () => {
  const stateBefore = [];
  const action = {
    type: 'ADD_TODO',
    id: 0,
    text: 'Learn Redux'
  };
  const stateAfter = [
    {
      id: 0,
      text: 'Learn Redux',
      completed: false
    }
  ];

  deepFreeze(stateBefore);
  deepFreeze(action);

  expect(
    todos(stateBefore, action)
    ).toEqual(stateAfter);
};

const testToggleTodo = () => {
  const stateBefore = [
    {
      id: 0,
      text: 'Learn Redux',
      completed: fase
    },
    {
      id: 1,
      text: 'Go shopping',
      completed: false
  }
  ];
  const action = {
    type: 'TOGGLE_TODO',
    id: 1
  };
  const stateAfter = [
    {
      id: 0,
      text: 'Learn Redux',
      completed: false
    },
    {
      id: 1,
      text: 'Go shopping',
      completed: true
    }
  ];

  deepFreeze(stateBefore);
  deepFreeze(action);

  expect(
    todos(stateBefore, action)
  ).toEqual(stateAfter);
};


const { createStore } = Redux;
const store = createStore(todoApp);

const { Component } = React;

const FilterLink = ({
  filter,
  currentFilter
  children
}) => {
  if (filter === currentFilter) {
    return <span>{children}</span>;
  }
  return (
    <a href='#'
       onClick={e => {
          e.preventDefault();
          store.dispatch({
            type: 'SET_VISIBILITY_FILTER',
            filter
            });
         }}
      >
        {children}
      </a>
    );
};

const getVisibileTodos = (
  todos,
  filter
) => {
  switch (filter) {
    case 'SHOW_ALL':
      return todos;
    case 'SHOW_COMPLETED':
      return todos.filter(
          t => t.completed
      );
    case 'SHOW_ACTIVE':
      return todos.filter(
        t => !t.completed
      );
  }
}

let nextTodoId = 0;
class TodoApp extends Component {
  render() {
    const {
      todos,
      visibilityFilter
    } = this.props;
    const visibleTodos = getVisibleTodos(
        todos,
        visibilityFilter
    );
    return (
      <div>
        <input ref={ node => {
          this.input = node;
        }} />
        <button onClick={() => {
          store.dispatch({
            type: 'ADD_TODO',
            text: this.input.value,
            id: nextTodoId++
            });
            this.input.value = '';
          }}>
            Add Todo
          </button>
          <ul>
            {visibleTodos.map(todo =>
                <li key={todo.id}
                    onClick={() => {
                      store.dispatch({
                        type: 'TOGGLE_TODO',
                        id: todo.id
                        });
                    }}
                    style={{
                      textDecoration:
                        todo.completed ?
                          'line-through' :
                          'none'
                    }}>
                  {todo.text}
                </li>
            )}
          </ul>
          <p>
            Show:
            {' '}
            <FilterLink
              filter='SHOW_ALL'
              currentFilter={visibilityFilter}
            >
              All
            </FilterLink>
            {' '}
            <FilterLink
              filter='SHOW_ACTIVE'
              currentFilter={visibilityFilter}
            >
              Active
            </FilterLink>
            {' '}
            <FilterLink
              filter='SHOW_COMPLETED'
              currentFilter={visibilityFilter}
            >
              Completed
            </FilterLink>
          </p>
      </div>
    );
  }
}

const render = () => {
  ReactDOM.render(
    <TodoApp
      {...store.getState()}
    />,
    document.getElementById('root')
  );
};

store.subscribe(render);
render();

testAddTodo();
testToggleTodo();
console.log('All tests passed!');
```
