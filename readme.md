# 24Slides Front-End Style Guide

## Guides

1. [Font Awesome Guide](FontAwesome/readme.md)

## Table of Contents

1. [Development Process](#development-process)

## Development Process

- Every task should be implemented in a new branch. The branch name should correspond to the following formula: `TFL` + `task number` + `task name`.  
  `TFL` means "Twenty Four Linear".  
  `Task number` is a number that Linear generates on task creation and it is unique.  
  `Task name` is a short name to define an implementation scope.

```js
// Avoid; "tfl" should be in uppercase
tfl-111-header:

// Avoid; No context
TFL-111-fixes:

// Prefer
TFL-111-header-refactoring:

// Prefer
TFL-111-public-page-fixes:
```

- Follow [Linear's task statuses](https://tppr.me/8EemA);

- The commit message should start with the task number. Example: TFL-179: Add new feature. Follow commit scope and message. Avoid messages like "fixed styles", prefer - "fixed login form styles";

> Note: there is `:` sumbol at the end of every example because of VS Code auto-formatting

```js
// Avoid; No task identifies
Fixed header styles

// Avoid; `tfl` should be in uppercase
tfl-111: Commit message

// Avoid; no colon after task identifier
TFL-111 Commit message

// Avoid; No context
TFL-111: Fixed styles

// Avoid; No context
TFL-111: Fixes after code review

// Avoid; No context
TFL-111: Fixes after testing

// Prefer
TFL-111: Created header markup, styles
```

- When a task is completed, create Pull Request (PR) in GitHub, request Andriy to code review. You are able to move forward with other tasks while the current task in code review status.

- PR's title should contain the Linear's task identifier according to the next formula: `TFL` + `task number`. LinearBot tracks the PRs and titles. When the title corresponds to Linear's task identifier, Linear's link, task title, and its description will be added as a comment by the bot automatically. Follow next title template:

```js
// Avoid; `tfl` should be in uppercase
tfl-11: Header refactoring

// Avoid; No colons
TFL-11 Header refactoring

// Avoid; No context
TFL-11: Header

// Prefer
TFL-11: Header refactoring

// Prefer
TFL-11: Update treatments page styles
```

- Fill PR description. Add a changelog, what you have done, some special cases or comments, you would like to note.

- Don't merge PR, even if it is approved.
