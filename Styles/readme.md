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
│  └─ **/*.scss
├─ utilities
├─ mixins
│  └─ **/*.scss
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
  ```

  ```scss
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
  ```

  ```scss
  // Allowed

  .selector {
    width: 24px;
    height: 24px;
  }
  ```

  ```scss
  // Prefer

  .selector {
    @include box(24);
  }
  ```

  ```scss
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
  ```

  ```scss
  // Allowed

  .selector {
    font-size: 24px;
    line-height: 28px;
  }
  ```

  ```scss
  // Prefer

  .selector {
    @include font-size(24);
  }
  ```

  ```scss
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

There are a few mixins for them:

- `lg` ("large") - desktop;
- `md` ("medium") - tablet;
- `sm` ("small) - mobile;

## BEM Methodology

- The class naming:

  ```scss
  // Avoid

  .selector__container__link {
  }
  ```

  ```scss
  // Prefer

  .selector__link {
  }
  ```

  ```scss
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
  ```

  ```scss
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
  ```

  ```scss
  // Prefer

  .selector__button.disabled {
  }
  ```

## SCSS Nesting

Keep the styles as simple as possible. There are a few utility extendeds like tailwind/bootstrap approaches.

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
  ```

  ```scss
  // Avoid

  .selector {
    &__block {
      &-container {
        button {
        }
      }
    }
  }
  ```

  ```scss
  // Prefer

  .selector {
    &__container {
    }

    .another-selector {
    }

    .another-selector img {
    }
  }
  ```

  ```scss
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
  ```

  ```scss
  // But allowed with styles

  .selector {
    &__image-container img {
    }

    &__button-container button {
    }
  }
  ```

## Style Rules

- Avoid BEM's block styles:

  ```scss
  // Avoid

  .selector {
    padding: 16px;

    &__content {
    }
  }
  ```

  ```scss
  // Prefer

  .selector {
    &__wrapper,
    &__container {
      padding: 16px;
    }

    &__content {
    }
  }
  ```

- Avoid using common class names: `button`, `title`, `form`, `text`, `row`, `block`, `container`, `wrapper`, etc;

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
  ```

  ```scss
  // Prefer

  .selector {
    color: $text-100;
    background-color: rgba($text-700, 0.5);
  }
  ```

- Come uo with the rules order. Out example:

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

- BEM's modifiers, simple pseudo-classes, and simple pseudo-elements can reach second nesting level:

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
  ```

  ```scss
  // Prefer

  .selector {
    &__button:hover .icon {
    }

    &__button:hover img {
    }
  }
  ```

  ```scss
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
  ```

  ```scss
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

- Avoid images via `background-image`;

- Avoid `!important`;

- Prefer `px` unit;

- Do not use `gap` property for flex elements;

- `z-index` value cannot be unreasonable;

- Follow formatting;

## Sources

- [bem.info](https://en.bem.info/methodology/)
- [Official Sass Guide](https://sass-lang.com/guide)
