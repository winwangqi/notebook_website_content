# React Hooks

## `useStatewithCallback`

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

## `usePrevious`

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
