# Debouncing

Debouncing is a programming pattern or a technique to restrict the calling of
a time-consuming function frequently, by delaying the execution of the function
until a specified time to avoid unnecessary CPU cycles, API calls, and
improve performance.

A debounce function is a higher-order function that returns another function,
to create closure around the function parameters (fn, timeout) and a timer
variable.

The term debounce comes from electronics. When you're pressing a button, let's
say on your TV remote, the signal travels to the microchip of the remote so
quickly that before you manage to release the button, it bounces, and the
microchip registers your "click" multiple times. To mitigate this, once a
signal from the button is received, the microchip stops processing signals
from the button for a few microseconds while it's physically impossible for you
to press it again.

The common use cases are search box suggestions, text-field auto-saves, and
eliminating double-button clicks.

Here is a simple example implementation.

```js
function debounce(fn, timeout = 300) {
  let timer

  return (...args) => {
    clearTimeout(timer)
    timer = setTimeout(() => {
      fn.apply(this, args)
    }, timeout)
  }
}

function saveInput() {
  console.log('Saving data')
}

const processChange = debounce(() => saveInput())
```

Here is an usage with `react-select` to load suggestions when user types in.

```jsx
import Select from "react-select/async";

export default function MyComponent() {
  const debounce = (fn, timeout = 600) => {
    let timer
    return (...args) => {
      clearTimeout(timer)
      timer = setTimeout(() => {
        fn(...args)
      }, timeout)
    }
  }

  const fetchOptions = async (query) => {
    let options = []
    try {
      ({ options } = (await axios.get('https://api.example.com/some/path')).data)
    } catch (error) {
      console.log(error)
    }
    return options
  }

  const loadOptions = (query, cb) => {
    fetchOptions(query).then((options) => cb(options))
  }

  return (
    <Select
      placeholder="Type your query..."
      loadOptions={debounce(loadOptions, 600)}
    />
  )
}
```

It seems that it is not easy to use deboucing for functions that return
promises, since a promise cannot be cancelled. It is more convenient to
use debouncing on function that pass their results to a callback, like
in the example with `react-select`. Read the following threads on SO:

- [Debounce function implemented with promises](https://stackoverflow.com/questions/35228052)
- [Promise it possible to force cancel a promise](https://stackoverflow.com/questions/30233302)

## References

- [What is Debounce in JavaScript?](https://blog.bitsrc.io/what-is-debounce-in-javascript-a2b8e6157a5a)
- [Debounce – How to Delay a Function in JavaScript (JS ES6 Example)](https://www.freecodecamp.org/news/javascript-debounce-example/)
