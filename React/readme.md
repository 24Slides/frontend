# JavaScript / React / JSX

## Table of contents

1. [Components Structure](#components-structure)
1. [Practices](#practices)

## Components Structure

The components structure concept is to keep as simple as possible without styles, helpers, and utilities in component's folder. The current structure we follow:

```
components
├─ FooCollection
│  ├─ **/*.jsx
│  └─ index.js
├─ BarCollection
│  ├─ BarPartial.jsx
│  ├─ BarUserInterface.jsx
│  ├─ ...
│  └─ index.js
├─ Baz.jsx
└─ index.js
```

It makes the components readable and scalable.

## Practices

- Component defining:

  ```jsx
  // Prefer

  export const Component = () => {};
  ```

- `index.js` contains the imports/exports only. The component related re-exporting should be:

  ```jsx
  // Prefer

  export * from "./ComponentCollection";
  ```

  ```jsx
  // Prefer

  export * as ComponentCollection from "./ComponentCollection";
  ```

- No anonymous function:

  ```jsx
  // Avoid

  const Component = ({ onClick }) => {
    <button onClick={(event) => onClick(event.target.value)}>Click</button>;
  };
  ```

  ```jsx
  // Prefer

  const Component = ({ onClick }) => {
    const handleButtonClick = (event) = {
      onClick(event.target.value)
    };

    <button onClick={handleButtonClick}>Click</button>;
  };
  ```

- Use destructuring:

  ```jsx
  // Prefer

  const Component = () => {
    const makeLink = ({ id, href, text }) => (
      <li>
        <a key={id} href={href}>
          {text}
        </a>
      </li>
    );

    return <ul>{links.map(makeLink)}</ul>;
  };
  ```

- Come up with imports orders;

- Use functional components only;
