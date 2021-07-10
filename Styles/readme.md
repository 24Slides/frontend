# SCSS and Styles

## Table of contents

1. [Styles Structure](#styles-structure)
1. [Styles Usage](#styles-usage)
   1. [Responsive Styles](#responsive-styles)
1. [BEM Methodology](#bem-methodology)
1. [SCSS Nesting](#scss-nesting)
1. [Style Rules](#style-rules)

## Styles Structure

The project's structure concept avoids `.scss` files in components' folder. We are moving styles to `styles`/`scss` folders. `/styles` folder structure:

```
styles
├─ components
│  ├─ **/*.scss
├─ utilities
├─ mixins
│  ├─ _box.scss
│  ├─ _font-face.scss
│  └─ _font-size.scss
├─ _animations.scss
├─ _compatibility.scss
├─ _fonts.scss
├─ _functions.scss
├─ _import.scss
├─ _mixins.scss
├─ _normalize.scss
├─ _reset.scss
├─ _variables.scss
└─ index.scss
```

- `index.scss` - entry point of styles;
- `_variables.scss` - global variables: font-family names, media breakpoints, colors, other;
- `_reset.scss` - reset CSS [source](https://meyerweb.com/eric/tools/css/reset/);
- `_normalize.scss` - own default styles over `_reset.scss`;
- `_mixins.scss` - mixin collection;
- `_import.scss` - a single import file for separated style files of a project;
- `_functions.scss` - function collection;
- `_fonts.scss` - the font settings;
- `_compatibility.scss` - styles for compatibility;
- `/mixins` - mixin collection;
- `/utilities` - helpers collection;
- `/components` - independed, separated component/section/page styles;

In general, all styles are static and unchangable. Except `components` folder. The `components`'s purpose is UI component styles storage. A developer is able to create the files or folder structure he needs to.

## Styles Usage

Learn utility helpers `styles/utilities`.

To get access to mixins, functions, and variables in style file, import them by import collection:

```scss
@import "~styles/import";
```

To import style file into any component from `styles/components` folder, use alias:

```jsx
// File is located at `styles/components/_example.scss`
import '@styles/_example';

const Component = () => { ... }
```

- Use `~styles` alias to get `styles` folder access:

  ```scss
  // Avoid
  @import "../../variables";

  .selector {
    background-color: $secondary-100;
  }

  // Prefer
  @import "~styles/variables";

  .selector {
    background-color: $secondary-100;
  }
  ```

- Use `box` mixin to add a container's size `width` and `height`:

  ```scss
  // Allowed
  .selector {
    width: 24px;
    height: 48px;
  }

  // Allowed
  .selector {
    width: 24px;
    height: 24px;
  }

  // Prefer
  .selector {
    @include box(24);
  }

  // Prefer
  .selector {
    @include box(24, 48);
  }
  ```

- Use `font-size` mixin to add `font-size` and `line-height` style rules:

  ```scss
  // Allowed
  .selector {
    font-size: 24px;
    line-height: normal;
  }

  // Allowed
  .selector {
    font-size: 24px;
    line-height: 28px;
  }

  // Prefer
  .selector {
    @include font-size(24);
  }

  // Prefer
  .selector {
    @include font-size(24, 28);
  }
  ```

### Responsive Styles

Currently, we support devices with a screen's width `320px` and above. The breakpoints are:

- Desktop - from `1025px`;
- Tablet - from `768px` to `1024px`;
- Mobile - to `767px`;

We created mixins for them:

- `lg` ("large") - desktop;
- `md` ("medium") - tablet;
- `sm` ("small) - mobile;

We moved forward and combined them to make a coverage of all responsive style cases: `md-lg`, `lg-md`, `sm-md`, and `md-sm`.

The responsive style concept is preventing re-setting styles on different devices.

- Use adaptive mixins to add responsive styles:

  ```scss
  // Avoid
  @media (min-width: 1024px) {
    .selector {
    }
  }

  // Prefer
  .selector {
    @include lg {
    }
  }
  ```

- Combine adaptive mixins to reduce unnecessary code:

  ```scss
  // Avoid
  .selector {
    @include lg {
      display: none;
    }

    @include md {
      display: none;
    }
  }

  // Prefer
  .selector {
    @include lg-md {
      display: none;
    }
  }
  ```

- Prevent style conflicts between devices:

  ```scss
  // Avoid
  .selector {
    // It fires on always
    padding: 16px;

    @include sm {
      // It fires on mobile only
      padding: 8px;
    }
  }

  // Prefer
  .selector {
    @include lg-md {
      // It fires on tablet and desktop only
      padding: 16px;
    }

    @include sm {
      // It fires on mobile only
      padding: 8px;
    }
  }
  ```

## BEM Methodology

- The class naming:

  ```scss
  // Avoid
  .selector__container__link {
  }

  // Prefer
  .selector__link {
  }

  // Prefer
  .selector__link-container {
  }
  ```

- Define blocks:

  ```scss
  // Avoid
  .selector__nav-container {
  }

  .selector__nav-link {
  }

  .selector__nav-button {
  }

  // Prefer
  .selector-nav__container {
  }

  .selector-nav__link {
  }

  .selector-nav__button {
  }
  ```

- It is different with BEM, but more useful on practice with [`classames`](https://www.npmjs.com/package/classnames) package. Use separated modifiers:

  ```scss
  // Avoid
  .selector__button--disabled {
  }

  // Prefer
  .selector__button.disabled {
  }
  ```

## SCSS Nesting

Keep the styles as simple as possible. There are a few utility extendeds like tailwind/bootstrap approaches.

- Follow the next selectors order:

  ```js
  1. Extends via `&`
  2. Classes
  3. Elements
  ```

  ```scss
  // Prefer
  .selector {
    // Extends
    &__container {
    }

    &__button {
    }

    &__link {
    }

    // Classess
    .boundary-box {
    }

    .specific-name {
    }

    // Elements
    button {
    }

    a {
    }
  }
  ```

- Keep only one nesting level:

  ```scss
  // Avoid
  .selector {
    &__container {
      .another-selector {
        img {
        }
      }
    }
  }

  // Avoid
  .selector {
    &__block {
      &-container {
        button {
        }
      }
    }
  }

  // Prefer
  .selector {
    &__container {
    }

    .another-selector {
    }

    .another-selector img {
    }
  }

  // Prefer
  .selector {
    &__block {
    }

    &__block-container {
    }

    &__block-container button {
    }
  }
  ```

- Avoid element styling:

  ```scss
  // Avoid
  .selector {
    ul {
    }

    ul li {
    }

    a {
    }
  }

  // But allowed with styles
  .selector {
    &__image-container img {
    }

    &__button-container button {
    }
  }
  ```

## Style Rules

- Prefer `px` unit:

  ```scss
  // Avoid
  .selector {
    padding: 10%;
  }

  // Avoid
  .selector {
    font-size: 1.2em;
    line-height: 1.6;
  }

  // Prefer
  .selector {
    padding: 16px;
  }

  // Prefer
  .selector {
    font-size: 16px;
    line-height: 20px;
  }
  ```

- `z-index` value cannot be unreasonable:

  ```scss
  // Avoid
  .selector {
    z-index: 99;
  }

  // Prefer
  .selector {
    z-index: 1;
  }
  ```

- Avoid BEM's block styles:

  ```scss
  // Avoid
  .selector {
    padding: 16px;

    &__content {
    }
  }

  // Prefer
  .selector {
    &__wrapper {
      padding: 16px;
    }

    &__content {
    }
  }
  ```

- Avoid using too common class names: `button`, `title`, `form`, `text`, `row`, `block`, `container`, `wrapper`, etc;

  ```scss
  // Avoid
  .button {
  }

  // Avoid
  .container {
  }

  // Avoid
  .block {
  }

  // Avoid
  .title {
  }
  ```

- The designers set [colors](https://tppr.me/fe3Ek) from [color palette](https://www.figma.com/file/zvVjskkyUJZ73Yaal2W0Uv/Style-Components?node-id=1715%3A1071) only. Only color from palette is allowed;

  ```scss
  // Avoid
  .selector {
    color: #fff;
    background-color: rgba(0, 0, 0, 0.5);
  }

  // Prefer
  .selector {
    color: $text-100;
    background-color: rgba($text-700, 0.5);
  }
  ```

- Follow the next rules order:

  ```js
  1. content
  2. display/
  3. position + direction properties: positon > top > right > bottom > left > z-index;
  4. margin: margin > margin-top > margin-right > margin-bottom > margin-left;
  5. padding: padding > padding-top > padding-right > padding-bottom > padding-left;
  6. flex properties: direction > wrap > alignment > other > order;
  7. dimensions: max-width > width > min-width > max-height > height > min-height;
  8. font and text: family > weight > style > size > line-height > color > other;
  9. border: border > border-radius;
  10. background;
  11. other;
  12. cursor;
  ```

  ```scss
  // Prefer
  .selector {
    // content
    content: "";

    // display
    display: flex;

    // position + direction properties: positon > top > right > bottom > left > z-index
    position: absolute;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    z-index: 1;

    // margin
    margin: 24px;
    // or
    margin-top: 12px;
    margin-right: 24px;

    // padding
    padding: 16px;
    // or
    padding-bottom: 0;
    padding-left: 24px;

    // flex properties: direction > wrap > alignment > other > order
    flex-direction: column;
    flex-wrap: wrap;
    justify-content: center;
    align-items: center;
    flex: 1;
    flex-basis: 100%;
    // ...
    order: 1;

    // dimensions: max-width > width > min-width > max-height > height > min-height;
    max-width: 1920px;
    width: 100%;
    min-width: 1024px;
    max-height: 100%;
    height: auto;
    min-height: 480px;

    // font and text: family > weight > style > size > line-height > color > other
    font-family: "Inter", sans-serif;
    font-weight: 700;
    font-style: italic;
    font-size: 40px;
    line-height: 48px;
    color: $text-700;
    text-decoration: none;
    text-transform: uppercase;

    // border: border > border-radius
    border: 1px solid $other-300;
    border-right: none;
    border-bottom: 0;
    border-radius: 8px;

    // background
    background-color: $secondary-400;

    // other
    transform: rotate(180deg);
    transition: all 400ms linear;
    overflow: hidden;
    pointer-events: none;

    // cursor
    cursor: pointer;
  }
  ```

- BEM's modifiers, pseudo-classes, and pseudo-elements can reach second nesting level:

  ```scss
  // Avoid
  .selector {
    &__button {
      &:hover img {
      }

      &:hover .icon {
      }
    }
  }

  // Prefer
  .selector {
    &__button:hover .icon {
    }

    &__button:hover img {
    }
  }

  // Allowed
  .selector {
    &__button.disabled {
    }

    &__button:hover {
    }

    &__button:first-child {
    }

    &__button::before {
    }
  }

  // Allowed
  .selector {
    &__button {
      &:hover {
      }

      &::before {
      }

      &:first-child {
      }

      .disabled {
      }
    }
  }
  ```

- Skip unneseccary selectors:

  ```scss
  // Avoid
  .selector {
    & .disabled {
    }

    & > img {
    }
  }

  // Prefer
  .selector {
    .disabled {
    }

    > img {
    }
  }
  ```

- Use `::` for `before`/`after` pseudo-elements;

- Avoid images via `background-image`;

- Avoid `!important`. It is not a good practice;
- Follow formatting;

## Sources

- [bem.info](https://en.bem.info/methodology/)
- [Official Sass Guide](https://sass-lang.com/guide)
