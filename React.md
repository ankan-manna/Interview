# React.js Interview Questions & Concepts Cheat Sheet

## 🔹 Introduction to React

### What is React?
React is a popular open-source JavaScript library developed by Facebook for building user interfaces, especially single-page applications. It allows developers to create reusable UI components that efficiently update and render when data changes, improving performance and maintainability.

### Why use React?
React offers several advantages:
- **Component-based architecture:** Build encapsulated components that manage their own state, then compose them to make complex UIs.
- **Virtual DOM:** React uses a virtual representation of the DOM to optimize updates, minimizing direct manipulation of the real DOM and improving performance.
- **Unidirectional data flow:** Data flows in one direction, making the application easier to understand and debug.
- **Rich ecosystem:** A vast community and numerous libraries support React development.
- **Cross-platform:** React can be used for web development and mobile apps via React Native.

## 🔹 JSX and Rendering

### What is JSX?
JSX (JavaScript XML) is a syntax extension that allows writing HTML-like code within JavaScript. It makes writing React components more intuitive by combining markup and logic in the same file.

Example:

```jsx
const element = <h1>Hello, world!</h1>;
```

JSX is transpiled to `React.createElement` calls by tools like Babel.

### How does React render UI?
React renders UI by creating a tree of React elements (virtual DOM). When state or props change, React compares the new virtual DOM with the previous one (diffing) and updates only the necessary parts of the real DOM (reconciliation).

## 🔹 Components in React

### What is a React component?
A component is a self-contained, reusable piece of UI that can accept inputs (props) and maintain internal state. Components can be functional or class-based.

### Functional Components
Functional components are JavaScript functions that return React elements. They can use hooks to manage state and lifecycle.

Example:

```jsx
function Greeting(props) {
  return <h1>Hello, {props.name}!</h1>;
}
```

### Class Components
Class components extend `React.Component` and have a `render` method that returns React elements. They manage state using `this.state` and lifecycle methods.

Example:

```jsx
class Greeting extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}!</h1>;
  }
}
```

### Props vs State
- **Props:** Read-only inputs passed from parent to child components. Used for configuration.
- **State:** Mutable data managed within a component that affects rendering and behavior.

| Aspect | Props | State |
|--------|-------|-------|
| Mutability | Immutable | Mutable |
| Source | Parent component | Component itself |
| Purpose | Configuration | Dynamic data |

## 🔹 React Hooks

### What are Hooks?
Hooks are special functions that let you use React features like state and lifecycle methods inside functional components.

### Common Hooks

#### useState
Manages state in functional components.

```jsx
const [count, setCount] = useState(0);
```

#### useEffect
Performs side effects such as data fetching or subscriptions.

```jsx
useEffect(() => {
  document.title = `You clicked ${count} times`;
  return () => {
    // Cleanup code here
  };
}, [count]);
```

#### useRef
Creates a mutable reference that persists across renders, often used to access DOM elements.

```jsx
const inputRef = useRef(null);
<input ref={inputRef} />
```

#### useContext
Accesses React context to share data without prop drilling.

```jsx
const theme = useContext(ThemeContext);
```

#### useMemo and useCallback
Optimize performance by memoizing values and functions to prevent unnecessary re-renders.

```jsx
const memoizedValue = useMemo(() => computeExpensiveValue(a, b), [a, b]);
const memoizedCallback = useCallback(() => { doSomething(a, b); }, [a, b]);
```

#### useReducer
Manages complex state logic similar to Redux reducers.

```jsx
const [state, dispatch] = useReducer(reducer, initialState);
```

## 🔹 Component Lifecycle

### Lifecycle Phases in Class Components
- **Mounting:** Initialization (`constructor`), rendering (`render`), and DOM insertion (`componentDidMount`).
- **Updating:** State or props changes trigger `shouldComponentUpdate`, `render`, and `componentDidUpdate`.
- **Unmounting:** Cleanup before removal (`componentWillUnmount`).

### Lifecycle with Hooks
`useEffect` hook can replicate lifecycle behavior:
- `useEffect(() => {}, [])` runs once after mount.
- `useEffect(() => {})` runs after every render.
- Cleanup function in `useEffect` runs before unmount or before next effect.

## 🔹 Advanced React Concepts

### Lifting State Up
Sharing state between components by moving it to their closest common ancestor.

### React Context API
Provides a way to pass data through the component tree without manually passing props at every level.

### Controlled vs Uncontrolled Components
- **Controlled:** Form inputs controlled by React state.
- **Uncontrolled:** Form inputs managed by the DOM, accessed via refs.

### Higher-Order Components (HOC)
Functions that take a component and return a new component with enhanced behavior.

### Render Props
Technique where a component’s prop is a function that returns React elements, allowing code reuse.

### React.memo
Optimizes functional components by memoizing them to avoid unnecessary re-renders.

### Lazy Loading and Code Splitting
Load components or code chunks on demand to improve initial load time.

```jsx
const OtherComponent = React.lazy(() => import('./OtherComponent'));
```

## 🔹 Forms and Events

### Handling Forms
React manages form inputs via state and event handlers.

Example:

```jsx
function Form() {
  const [value, setValue] = useState('');

  const handleSubmit = (e) => {
    e.preventDefault();
    alert(value);
  };

  return (
    <form onSubmit={handleSubmit}>
      <input value={value} onChange={(e) => setValue(e.target.value)} />
    </form>
  );
}
```

### Prevent Default Behavior
Use `e.preventDefault()` to stop default form submission or event behavior.

## 🔹 Routing in React

### React Router
A popular library for client-side routing in React applications.

Example:

```jsx
<BrowserRouter>
  <Route path="/about" component={About} />
</BrowserRouter>
```

### Link vs Anchor Tag
- `<Link>` enables client-side navigation without page reload.
- `<a>` tag causes full page reload.

## 🔹 State Management

### Redux vs Context API
- **Redux:** Centralized state management with middleware and devtools, suitable for complex apps.
- **Context API:** Simpler state sharing without prop drilling, suitable for less complex scenarios.

### Redux Core Concepts
- **Store:** Holds the application state.
- **Actions:** Plain objects describing state changes.
- **Reducers:** Pure functions that update state based on actions.

## 🔹 Testing and Optimization

### Testing React Components
Use tools like React Testing Library or Enzyme to write unit and integration tests.

Example:

```jsx
test('renders button', () => {
  render(<Button />);
  expect(screen.getByRole('button')).toBeInTheDocument();
});
```

### Performance Optimization
- Use `React.memo` to memoize components.
- Use `useMemo` and `useCallback` to memoize values and functions.
- Avoid inline object and function declarations in props.

## 🔹 Miscellaneous Concepts

### Keys in React
Keys help React identify which items have changed, added, or removed in lists, improving rendering performance.

### Fragment
`<Fragment>` lets you group multiple elements without adding extra nodes to the DOM.

### Reconciliation
React’s process of diffing virtual DOM trees to update the real DOM efficiently.

### Strict Mode
A tool for highlighting potential problems in an application during development.

### Error Boundaries
Components that catch JavaScript errors anywhere in their child component tree and display a fallback UI.

## 🧠 Top 20 React.js Topics (Summary)
- JSX: HTML-like syntax extension
- Components: Building blocks of React apps
- Props vs State: Immutable vs mutable data
- useState: Hook for state management
- useEffect: Hook for side effects
- useRef: Hook for accessing DOM/values
- useMemo: Hook for memoizing values
- useCallback: Hook for memoizing functions
- useContext: Hook for accessing context
- Context API: Alternative to prop drilling
- Lifecycle: Mounting, updating, unmounting
- Conditional Rendering: &&, ternary operators
- Event Handling: Synthetic events
- Forms: Controlled vs uncontrolled
- React Router: Client-side routing
- Lifting State: Sharing state between components
- Code Splitting: Loading code on demand
- Error Boundaries: Catching JavaScript errors
- HOCs: Reusing component logic
- Performance: Memoization, virtualization
