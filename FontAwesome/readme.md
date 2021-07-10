# 24Slides Font Awesome Guide

## Table of Contents

1. [Boundary Box](#boundary-box)
1. [NPM Registry](#npm-registry)
1. [Design Icon Naming](#design-icon-naming)
1. [Font Awesome Component](#font-awesome-component)
1. [Font Awesome Global Library](#font-awesome-global-library)
1. [Sources](#sources)

## Boundary Box

We use Pro Font Awesome icons with a design boundary box approach.

**Bounday Box** ([Boundary volume](https://en.wikipedia.org/wiki/Bounding_volume)) is a box with minimum size `24px` and a multiple of `8px` of the theme design approach. The margins will be added to the box and not to icon directly.

To make a boundary box, use class name `boundary-box` or `bb`. To change boundary box size (default: `24px`), use `box-n` class name. There are `24`, `32`, `40`, and `48` box values.

Boundary box examples:

- [Figma mockup](https://tppr.me/xiju5)
- [HTML markup](https://tppr.me/5Xj9X)

## NPM Registry

```js
// .npmrc
@fortawesome:registry=https://npm.fontawesome.com/
//npm.fontawesome.com/:_authToken={PRO_PACKAGE_TOKEN}
```

## Design Icon Naming

Every icon in project has the same name with Font Awesome Icons name. There are a few types of naming in Figma:

- Style / icon-name
- Style / font-awesome-icon
- font-awesome-icon

The examples below:

- [Regular / trash-alt](https://tppr.me/8vbBI)
- [Regular / far fa-search](https://tppr.me/yq9Wc)
- far fa-search

> // todo: add example link

To reference an icon, you need to know two bits of information: name, prefixed with `fa` (meaning "font awesome" naturally) and style.

The available styles:

| Style   | Style Prefix | Package               | Rendering |
| ------- | ------------ | --------------------- | --------- |
| Solid   | fas          | pro-solid-svg-icons   |           |
| Regular | far          | pro-regular-svg-icons |           |
| Light   | fal          | pro-light-svg-icons   |           |
| Duotone | fad          | pro-duotone-svg-icons |           |
| Brands  | fab          | free-brands-svg-icons |           |

## Font Awesome Component

To get the icon you want to, import it from a related package:

```jsx
import { faCofee } from "@fortawesome/pro-regular-svg-icons";
import { FontAwesomeIcon } from "@fortawesome/react-fontawesome";

const Component = () => <FontAwesomeIcon icon={faCoffee} />;
```

## Font Awesome Global Library

Go to `fontAwesome` utility in project. There are icons collection. Import and add to library the icon you want to:

```js
import { faCofee } from "@fortawesome/pro-regular-svg-icons";

library.add(faCoffee);
```

The added icon becomes available by name and style `far cofee`.

```jsx
import { FontAwesomeIcon } from "@fortawesome/react-fontawesome";

const Component = () => <FontAwesomeIcon icon={["far", "coffee"]} />;
```

## Sources

- React `FontAwesomeIcon` attributes - [react-fontawesome.d.ts](https://github.com/DefinitelyTyped/DefinitelyTyped/blob/master/types/react-fontawesome/index.d.ts)
- [24Slides initial issue](https://github.com/24Slides/24slides/issues/1815)
- [Official Font Awesome using with React](https://fontawesome.com/v5.15/how-to-use/on-the-web/using-with/react)
