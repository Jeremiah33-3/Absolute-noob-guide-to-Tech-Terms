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

## Container components and presentational components
> Separating container components from presentational components is a popular React programming pattern.

Functional parts of the components such as maintaing states, using effects, passing down states are container component's job, also known as stateful component.

Presentational components are stateless components that deal only with JSX. It should be an exported component and should not render itself because a presentational component will always get rendered by a container component.

They can communicate with one another through passing state through props. But for presentational component to update container component about changes, container will have a handler function passed as a prop to the presentational component. Container component should render the presentational component(s) instead of other JSX.

## React styles
Different ways to style: examples are inline styles and style object variable

Inline styles are styles written as an **attribute** of the element. `<h1 style={{ color: 'red' }}>Hello world</h1>` 
- the outer curly braces signal that everything in between is to be read in JS
- inner braces creates a JS object literal

Style object variable is a JS object literal with properties and values to style an element. it is injected to the style attribute of a component. E.g.:
```js
const darkMode = {
  color: 'white',
  background: 'black'
};
...
<h1 style={darkMode}>Hello world</h1>
```
- Reference CSS properties by writing CSS property names as camelCase as in [style object](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/style) of the DOM.
- Write numeric value as string values e.g. "20px", "20%", "2em"


A better way making styles modular, organized, and reusable is to create separate stylesheets for each component, then import the stylesheet using the `import` keyword.
- Use CSS [modules](https://css-tricks.com/css-modules-part-1-need/) to prevent conflicting class names in the style sheets, by scoping the classNames, variables etc. to local scope

## Miscellaneous
useful stuffs that might be overlooked:

- [template literal](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals)
