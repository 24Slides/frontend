# Folder Structure

## Table of Contents

1. [Sources](#sources)
   - [assets](#assets);
   - [components](#components);
   - [constants](#constants);
   - [content](#content);
   - [hooks](#hooks);
   - [images](#images);
   - [pages](#pages);
   - [redux](#redux);
     - [actions](#actions);
     - [reducers](#reducers);
     - [selectors](#selectors);
   - [services](#services);
   - [styles](#styles);
   - [types](#types);
   - [utils](#utils);
1. [Practices](#practices)

## Sources

```
src
├─ assets
├─ components
├─ constants
├─ content
├─ hooks
├─ images
├─ pages
├─ redux
│  ├─ actions
│  ├─ selectors
│  └─ selectors
├─ services
├─ styles
├─ types
├─ utils
├─ App.tsx
└─ index.tsx
```

### Assets

```
src/assets
├─ fonts
│  └─ **/*.*
├─ translation
│  └─ **/*.*
├─ **/*.*
└─ countries.json
```

`assets` folder contains fonts, translation, and other assets.

### Components

```
src/components
├─ Buttons
│  ├─ Button.tsx
│  ├─ Link.tsx
│  └─ index.ts
├─ **/*.tsx?
└─ index.ts
```

`components` folder contains the components only.

### Constants

`constants` folder contains constants with a duplicate name `*.constants.ts`.

A `*.constants.ts` file consists the constants in upper case only.

```js
export const PRODUCTION = process.env.REACT_APP_ENV === "production";
```

```js
export const HIGH_LEVEL_CONSTANT = {
  LOW_LEVEL_CONSTANT: "LOW_LEVEL_CONSTANT",
};
```

### Content

```
src/content
├─ ui.content.ts
├─ **/*.ts
└─ index.ts
```

`content` folder contains internal static data with a duplicate name `*.content.ts`.

A `*.content.ts` file consists the variables in camel case only.

> If you doesn't believe the data should be a constant, put it as content:

```js
export const labelFaIcons = {
  new: {
    icon: faBookmark,
    label: "New",
  },
  portal: {
    icon: faBuilding,
    label: "Custom portal",
  },
  free: {
    icon: faReceipt,
    label: "Free order",
  },
  other: {
    icon: faLightbulb,
    label: "Other treatment",
  },
};
```

```js
const weekDays = [
  "Sunday",
  "Monday",
  "Tuesday",
  "Wednesday",
  "Thursday",
  "Friday",
  "Saturday",
];
```

### Hooks

`hooks` folder contains the custom hooks.

A custom hook should match with name pattern in camel case `use` + `hook name`.

```
src/hooks
├─ useForceRender.ts
├─ *.ts
└─ index.ts
```

```js
// src/hooks/useForceRender.ts

export const useForceRender = () => useReducer(() => ({}), {})[1];
```

### Images

```
src/images
└─ **/*.*
```

### Pages

```
src/pages
├─ HomePage.tsx
├─ **/*.*
└─ index.ts
```

`pages` folder contains the page related wrappers.

A page name should match with name pattern in pascal case `page name` + `Page`.

### Services

`services` folder contains configs, settings and other external services.

```
src/services
├─ axios.ts
├─ hotjar.ts
├─ *.ts
└─ index.ts
```

### Styles

```
src/styles
├─ components
│  ├─ _button.scss
│  ├─ _ui.scss
│  └─ **/*.s?css
├─ utils
│  ├─ _boundary-box.scss
│  ├─ _box.scss
│  ├─ _display.scss
│  ├─ _flex.scss
│  ├─ _helpers.scss
│  ├─ _position.scss
│  └─ **/*.s?css
├─ mixins
│  ├─ _box.scss
│  ├─ _font-face.scss
│  ├─ _font-size.scss
│  └─ **/*.scss
├─ _bootstrap.scss
├─ _colors.scss
├─ _reset.scss
├─ _typography.scss
├─ _variables.scss
├─ **/*.s?css
└─ index.scss
```

- `/components/**/*.s?css` - custom component styles;
- `/utils/**/*.s?css` - global, general and common style utilities;
- `_reset.scss` - reset default browser CSS styles;
- `_colors.scss` - color utilities;
- `_variables.scss` - global variables: font-family names, media breakpoints, colors, etc;
- `_typography.scss` - default typography styles;
- `index.scss` - entry point of styles;

### Types

```
src/types
├─ app.d.ts
├─ **/*.d.ts
└─ index.ts
```

`types` folder contains types, interfaces, enums, namespaces, and other TypeScript definitions.

```ts
// ui.d.ts

export type BoxSize = 16 | 24 | 32 | 40 | 48;
```

```ts
// app.d.ts

export type Noop<F = () => void> = F;
```

### src/App.tsx

`App.tsx` is main component.

### src/index.jsx

`index.tsx` is entry file.