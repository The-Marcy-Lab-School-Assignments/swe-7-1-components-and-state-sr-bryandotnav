# Short Response: Intro to React, Components, and useState

Answer each question below. Write in complete sentences (3–5 per answer).

---

## Question 1 — Components and JSX

What is a React component, and what is JSX? Explain how JSX differs from plain HTML. Use a brief code example to support your answer.

**Your answer:**

A react component is a js function that is self contained and reusable for user interface. JSX is the syntax that lets you write an HTML-like markup inside a js file and under the hood JSX gets transpiled into standard `React.createElement()` function calls. Some of the differences include attribute naming; the attributes use camelCase rather than standard HTML syntax and you can embed any javascript expression directly inside curly braces

EX:

```jsx
function Greeting({ name }) {
  const isLoggedIn = true;

  return (
    <div className="card">
      <h1>Hello, {name}!</h1>
      {isLoggedIn && <p>Welcome back.</p>}
    </div>
  );
}
```

## Question 2 — The Build Step and Vite

A browser cannot run a `.jsx` file directly. Why not? Explain the role of a build step and what it means to "compile" code in simple terms.

**Your answer:**

A browser cannot run a JSX file directly because browsers only natively understand standard javascript, HTML and CSS. JSX is a non standard syntax which means that browsers will throw a syntax error if you try and execute a .jsx file directly. The role of a build step is to automate the process of preparing raw source code for production. It uses tools like esbuild or babel to compile JSX into plain `React.createElement()` function calls, and compiling JSX basically means to take code written in one format like JSX in this instance and translating it into another format that the target environment can actually execute.

## Question 3 — useState

What does `useState` return, and what are the two things you get back from it? Describe how to use those values to render data and to update that data.

**Your answer:**

`useState` returns the current state and the setter function, the current state is the current data and the setter function is the function that updates the current state and triggers a re-render.

## Question 4 — Lifting State Up

What does it mean to "lift state up," and when is it necessary? Use a concrete example.

**Your answer:**

Lifting state up means moving state from a child component into a shared parent component. You use this when two or more components need to stay in sync with the same piece of data. An example of this is when you have a product list and a cart summary that both need to know what's been added.

## Question 5 — Bug Fix

The component below has a bug. When the user clicks "Add Cherries," the list never updates on screen. Identify what is wrong, write the corrected code, and explain **why** the original code fails in React.

```jsx
const ShoppingList = () => {
  const [items, setItems] = useState(["apples", "bananas"]);

  const addItem = () => {
    items.push("cherries");
    setItems(items);
  };

  return (
    <>
      <ul>
        {items.map((item, i) => (
          <li key={i}>{item}</li>
        ))}
      </ul>
      <button onClick={addItem}>Add Cherries</button>
    </>
  );
};
```

**Your answer:**

Whats wrong is that items.push() mutates the existing array in place so that `items` keeps the same reference and setItems(items) passes that same reference, since react checks the reference and sees that there is no change it does not rerender so you would need to create a new array
Correct code:

```js
const addItem = () => {
  setItems([...items, "cherries"]);
};
```
