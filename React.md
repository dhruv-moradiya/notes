1. What is Virtual Dom in react and how it is work what algorithm it is use ?

   - The Virtual DOM (VDOM) is a concept used in React (and other libraries) to improve performance and optimize updates to the user interface (UI). It acts as an intermediary between the actual DOM and the React components. The Virtual DOM is essentially a lightweight copy of the actual DOM, allowing React to make updates more efficiently.

#### How the Virtual DOM Works

- Rendering:

  - When a React component is rendered for the first time, a Virtual DOM tree is created. This tree is a JavaScript object representing the structure of the actual DOM.

- Updating

  - When the state or props of a component change, React updates the Virtual DOM rather than the actual DOM.
  - React then compares the updated Virtual DOM with the previous version of the Virtual DOM. This process is called "reconciliation."

- Diffing Algorithm:
  - React uses a highly efficient diffing algorithm to compare the previous and the current Virtual DOM trees. This algorithm is known as the reconciliation algorithm.
  - The algorithm works in two phases: - Diffing Phase: React determines what has changed by comparing the old and new Virtual DOM trees. - Updating Phase: React applies only the necessary changes to the actual DOM based on the differences found in the diffing phase.

2. What is life cycle methods in react ?

- Lifecycle methods in React are special methods that get called at different stages of a component's lifecycle. These methods allow you to hook into the component's lifecycle events, providing opportunities to execute code at specific points in the component's existence. There are three main phases in a React component's lifecycle:

  1. Mounting: When the component is being inserted into the DOM.
  2. Updating: When the component is being re-rendered as a result of changes to its props or state.
  3. Unmounting: When the component is being removed from the DOM.

- https://medium.com/@arpitparekh54/understanding-the-react-component-lifecycle-a-deep-dive-into-the-life-of-a-react-component-74813cb8dfb5
