# React Hooks

## 入门

### 无破坏性更改

- 完全可选的
- 100% 向后兼容
- 现在可用

### 动机

- 难以复用组件间有状态的逻辑
- 复杂的组件变得难以理解
- `class` 同样困扰着人和机器

## Hooks 初体验

### 📌 State Hook

```jsx
import React, { useState } from 'react'

function Example() {
  const [count, setCount] = useState(0)
  return (
    <div>
      <p>{count}</p>
      <button onClick={() => { setCount(count + 1) }}>click me</button>
    </div>
  )
}
```

### ⚡️ Effect Hook

```jsx
import React, { useState, useEffect } from 'react'

function Example() {
  const [count, setCount] = useState(0)

  // 与 componentDidMount 和 componentDidUpdate 相似
  useEffect(() => {
    document.title = `clicked ${count} times`

    // 与 componentWillUnmount 相似
    return () => {
      // unsubscribe...
    }
  })

  return (
    <div>
      <p>{count}</p>
      <button onClick={() => { setCount(count + 1) }}>click me</button>
    </div>
  )
}
```

### ✌️ Hooks 的规则

- 只能在最顶层调用 Hooks
- 只能在函数式组件内调用 Hooks

### 💡 构建自定义的 Hooks

自定义 Hooks 更像是一种约定而非功能。一个函数如果以 **use** 开头，并且调用其它 Hooks，则我们称它为自定义 Hook。

### 🔌 其它 Hooks

- useContext
- useReducer



## 使用 State Hook

**调用 `useState()` 是做什么的？** 它声明了一个 "有状态变量"。

**向 `useState()` 传递 `argument` 是用来做什么？** 传递给 `useState()` Hook 的唯一 argument 是初始状态。

**useState() 返回什么？** 它返回一对值：*当前状态* 和 *更新状态的函数*。

```jsx
import React, { useState } from 'react'

function Example() {
  const [count, setCount] = userState(0)
  
  return (
  	<div>
    	<p>{count}</p>
      <button onClick={() => { setCount(count + 1) }}>click me</button>
    </div>
  )
}
```


## 使用 Effect Hook

`useEffect` Hook 允许在函数式组件内执行副作用。

### 未被清理的 Effects

```jsx
import React, { useState, useEffect } from 'react'

function Example() {
  const [count, setCount] = useState(0)

  useEffect(() => {
    document.title = `You clicked ${count} times`
  })

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  )
}
```

**`useEffect` 是用来做什么的？** 通过使用 `useEffect` Hook 来告知 React 组件需要在 render 之后做一些事请。

**为什么在组件中调用 `useEffect`？** 在组件内使用 `useEffect` 使我们能够在 **effect** 内访问 **state** 变量或者任何 **prop**。

**`useEffect` 在每次 render 之后都运行吗？**  是的！默认在初次 render 和之后的每次更新都运行 effect。

### 被清理的 Effects

```jsx
import React, { useState, useEffect } from 'react'

function FriendStatus(props) {
  const [isOnline, setIsOnline] = useState(null)

  useEffect(() => {
    function handleStatusChange(status) {
      setIsOnline(status.isOnline)
    }

    ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange)
    // Specify how to clean up after this effect:
    return function cleanup() {
      ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
    }
  })

  if (isOnline === null) {
    return 'Loading...'
  }

  return isOnline ? 'Online' : 'Offline'
}
```

**为什么从 effect 返回一个函数？** 这是 effects 的可选的清理机制。

**React 在何时清理 effect？** React 在组件卸载之后执行清理工作。

### Tip：使用多个 Effects 来分离关注点

将不同功能分割到多个 effects 来分离关注点。

### Tip：跳过 Effects 来优化性能

通过给 `useEffect` 传递一个 deps 数组作为可选的第二个参数，来告诉 React 当 deps 没有改变时跳过 effects。

## 自定义 Hooks

### `useStatewithCallback`

```jsx
import React, { useState, useRef, useEffect } from 'react'

export default function useStateWithCallback(initState) {
  const callbackRef = useRef(null)

  const [state, setState] = useState(initState)

  useEffect(() => {
    if (callbackRef.current) {
      callbackRef.current(state)
      callbackRef.current = null
    }
  }, [state])

  const setCallbackState = (value, callback) => {
    callbackRef.current = typeof callback === 'function' ? callback : null
    setState(value)
  }

  return [state, setCallbackState]
}
```

[ref](https://github.com/reactjs/rfcs/issues/98)

### `usePrevious`

```jsx
function usePrevious(value) {
  // The ref object is a generic container whose current property is mutable ...
  // ... and can hold any value, similar to an instance property on a class
  const ref = useRef()

  // Store current value in ref
  useEffect(() => {
    ref.current = value
  }, [value]) // Only re-run if value changes

  // Return previous value (happens before update in useEffect above)
  return ref.current
}
```

[ref](https://usehooks.com/usePrevious/)
