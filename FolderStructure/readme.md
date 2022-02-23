# Folder Structure

```
src
├── common
│   │
│   │   # contains fonts, translation, and other assets
│   ├── assets
│   │   ├── fonts/
│   │   ├── translations/
│   │   ├── images/
│   │   └── countries.json
│   │
│   │   # reusable generic components
│   ├── components
│   │   └── Input
│   │       ├── index.ts
│   │       ├── Input.module.scss
│   │       └── Input.tsx
│   │
│   │   # only global store, sidebar, top loader, user data, etc.
│   ├── redux 
│   │   ├── actions.ts
│   │   ├── index.ts
│   │   ├── reducer.ts
│   │   └── selectors.ts
│   │
│   │   # axios wrappers, reusable generic data transformation utils, etc.
│   ├── utils
│   │   ├── noop.ts
│   │   └── round.ts
│   │
│   │   # generic utility types
│   ├── types
│   │   ├── NonEmptyArray.ts
│   │   └── Number.ts
│   │
│   │   # reusable generic hooks
│   ├── hooks
│   │   ├── useFastDog.ts
│   │   └── useSlowPoke.ts
│   │
│   ├── styles
│   │   │
│   │   ├── index.scss # entry point
│   │   ├── _reset.scss
│   │   ├── _functions.scss
│   │   ├── _mixins.scss
│   │   │
│   │   │   # could be imported to access colors, variables, functions & mixins
│   │   │   # inside Module's global or local scss, which gets imported in Module.tsx
│   │   ├── shared.scss
│   │   │
│   │   ├── _colors.scss # color variables
│   │   └── _variables.scss
│   │
│   │   # global constants like process.env.REACT_APP_ENV goes here
│   └── constants.ts
│
├── Module
│   │
│   │   # module-specific store subtree which gets imported and nested in a global store
│   │   # globalStore.module
│   ├── redux
│   │   ├── actions.ts
│   │   ├── index.ts
│   │   ├── reducer.ts
│   │   └── selectors.ts
│   │
│   │   # module chunk for code-organization purposes, not reusable
│   ├── SubModule
│   │   ├── index.ts
│   │   ├── SubModule.module.scss
│   │   └── SubModule.tsx
│   │
│   ├── constants.ts # module specific constants (optional)
│   ├── domain.ts # could be a folder if there's a lot of decoders/types there
│   ├── hooks.ts # could be a folder in case there's a lot of hooks
│   ├── index.ts
│   ├── Module.module.scss
│   ├── Module.tsx
│   └── utils.ts # could be a folder if there's a lot of module-specific utils
│
│   # application main module (contains layout, routing, initialization, etc.)
├── App.tsx
└── index.tsx # application entry point
```

The idea behind this folder structure is to organize code according to a
speicific module/domain.

This folder/project structure will let developers focus on a specific area they
currently working on. There will be no need to navigate to other folders that
may contain unrelated stuff, everything is under `<module-name>` folder.

`common` module is very important here and makes a lot of sense. It has a
similar structure to any other module. We can put generic re-usable components
there under `components` folder, global utilities like `http-client` under
`utils` folder and global applications state can be defined under `redux`
folder. The idea is that usually we write things that are only relevant in some
module and if we encounter something that can be re-used in other modules, this
can go to `common` module.
