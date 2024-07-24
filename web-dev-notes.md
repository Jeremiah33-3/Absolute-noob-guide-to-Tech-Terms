## Exports

Named exports versus default exports, link [here](https://stackoverflow.com/questions/46913851/why-and-when-to-use-default-export-over-named-exports-in-es6-modules)
- a file can have multiple named exports but can have only 1 default export
- developers give default exports names when they import it, while we must use the names of named exports
- need to use curly braces for named exports

more info [here](https://www.freecodecamp.org/news/difference-between-default-and-named-exports-in-javascript/).

## React hooks

it is a function that may or may not return something (e.g. useState() returns an array with two values representing current state and the state setter function). except useEffect() does not return anything but takes in a callback function and the dependencies(optional) -- reactive values referenced inside the callback function

To notes:
- best practise to define static data models (data that does not change) outside of react components so they won't be recreated each time the componenet re-renders
- hooks such as useState handles dynamic data 
- useful to use the [computed property names](https://eloquentcode.com/computed-property-names-in-javascript) when updating object in useState
- good practise to **return** a cleanup function in some effects, especially those that might cause the DOM to go haywire when re-rendering; cleanup function runs both when re-rendering when dependencies change and also during [unmounting](https://stackoverflow.com/questions/31556450/what-is-mounting-in-react-js), cleanup code should have a corresponding setup code, which are usually 'symmetrical'.
- to prevent effect hook running on every re-render (ie call effect hook only on first render), pass in an empty array as the second argument, the `dependencies` array, in which the elements are variables/states, triggering the hook to run when one or many of them changes values
- cleanup function will be called when component unmounts
- only call hooks at the top-level and from React functions
- bad practise to call hooks from loops, conditions, or nested functions since data and functions managed by hooks are being handled based on their order in the function component's definition
- group the state and the corresponding effect hook together, when using separate effect hooks


### Custom hook to reuse logic
information [here](https://react.dev/learn/reusing-logic-with-custom-hooks#custom-hooks-sharing-logic-between-components).
- can create our own React hook to reuse a certain piece of logic
- since hooks are really functions, we can achieve this by defining a function that achieves the behaviour -- that'll be the hook
- note that hook name **always** start with **use**
- however, custom hook does not let you share states, but only stateful logic. the state var in one call of hook is independent of that of another. [this](https://react.dev/learn/sharing-state-between-components) is how to share states between components.

## Request, response, and object tpyes
### [Response](https://developer.mozilla.org/en-US/docs/Web/API/Response) object
- some methods, attributes to play with the object


## Miscellaneous
useful stuffs that might be overlooked:

- [template literal](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals)
