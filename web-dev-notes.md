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


## Miscellaneous
useful stuffs that might be overlooked:

- [template literal](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals)
