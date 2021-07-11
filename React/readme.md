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

- Follow imports orders:

  ```js
  1. Packages
  // Line break
  2. Types > constants > content = helpers = utilities = hooks = actions = selectors > other
  // Line break
  3. Components
  4. Images
  5. Styles
  ```

  ```jsx
  // Prefer
  import React from "react";
  import { useSelector } from "react-redux";
  import { Router } from "react-router-dom";
  import cx from "classnames";

  import type { Type } from "@types/app.types";
  import * as constants from "@constants";
  import * as actions from "@actions";
  import { reducer } from "@helpers";
  import { axios } from "@utils";
  import { createLoadingSelector } from "@selectors";

  import { Button, Link, Render } from "@components";
  import logoSvg from "@images/logo.svg";
  import logoImage from "@images/logo.png";
  import "@styles/_component";
  ```

- Component defining:

  ```jsx
  // Avoid
  export default function Component () {};

  // Avoid
  const Component = () => {}

  export Component;

  // Prefer
  const Component = () => {}

  export default Component;
  ```

- `index.js` contains the imports/exports only. The component related re-exporting should be:

  ```jsx
  // Avoid
  export { default as Component } from './Component';

  // Avoid
  import Component from './Component';

  export { Component }

  // Prefer
  import Component from './Component';

  export default Component;

  // Allowed
  import Component from './Component';

  export { default as ComponentPartial } from './ComponentPartial';
  import { default as ComponentInterface } from './ComponentInterface';

  export default Component;

  // Allowed
  export * from './ComponentCollection';

  // Allowed
  export * as ComponentCollection from './ComponentCollection';
  ```

- Follow the variables order:

  ```js
  1. Constants
  2. Hooks
  3. React Hooks: useRef > useState > useEffect > useCallback = useMemo
  4. Functions
  5. Helpers
  ```

  ```jsx
  // Prefer
  const Component = () => {
    // noop = () => {}
    const CONSTANT = 'CONSTANT';

    useCustomHook();
    const state = useState(stateSelector);
    const dispatch = useDispatch();

    const ref = useRef();
    const [state, setState] = useState();

    // Because `useEffect` requires function
    const fetchData = useCallback(noop, []);

    useEffect(() => {
      fetchData();
    }, [fetchData])

    const data = useMemo(noop, []);

    const setter = useCallback(noop);

    const handleButtonClick = noop;

    const makeMap = noop;

    const list = data.map(makeMap);

    const Loader = <div> ... </div>

    return ( ... );
  }
  ```

- Move map functions from returning JSX:

  ```jsx
  // Avoid
  const Component = () => {
    return (
      <ul>
        {links.map((link) => (
          <li>
            <a href={link}>{link}</a>
          </li>
        ))}
      </ul>
    );
  };

  // Prefer
  const Component = () => {
    const makeLink = (link) => (
      <li>
        <a href={link}>{link}</a>
      </li>
    );

    return <ul>{links.map(makeLink)}</ul>;
  };
  ```

- No anonymous function:

  ```jsx
  // Avoid
  const Component = () => {
    <button onClick={() => {}}>Click</button>;
  };

  // Avoid
  const Component = ({ onClick }) => {
    <button onClick={(event) => onClick(event.target.value)}>Click</button>;
  };

  // Prefer
  const Component = ({ onClick }) => {
    const handleButtonClick = (event) = {
      onClick(event.target.value)
    };

    <button onClick={handleButtonClick}>Click</button>;
  };
  ```

- Use curry functions (hof):

  ```js
  const mock = [
    { id: 1, title: "Foo" },
    { id: 2, title: "Bar" },
  ];
  ```

  ```jsx
  // Avoid
  const Component = (onClick) => {
    const makeMock = ({ id, title }) => {
      const handleClick = (id) => onClick(id);

      return <button onClick={handleClick}>{title}</button>;
    };

    return <div>{mock.map(makeMock)}</div>;
  };

  // Prefer
  const Component = (onClick) => {
    const handleClick = (id) => () => onClick(id);

    const makeMock = ({ id, title }) => (
      <button onClick={handleClick(id)}>{title}</button>
    );

    return <div>{mock.map(makeMock)}</div>;
  };
  ```

- Use destructuring:

  ```jsx
  // Avoid
  const Component = (props) => (
    <div>
      <h1>{props.title}</h1>
      <p>{props.text}</p>
    </div>
  );

  // Avoid
  const Component = () => {
    const makeLink = (link) => (
      <li>
        <a key={link.id} href={link.href}>
          {link.text}
        </a>
      </li>
    );

    return <ul>{links.map(makeLink)}</ul>;
  };

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

- Use functional components only;
