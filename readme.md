# 24Slides Front-End Style Guide

## Guides

1. [Folder Structure](FolderStructure)
1. [JavaScript / React Guide](React)
1. [Styles Guide](Styles)
1. [Font Awesome Guide](FontAwesome)

## Table of Contents

1. [Development Process](#development-process)
1. [Re-exporing and Aliases Approach](#re-exporing-and-aliases-approach)

## Development Process

- Every task should be implemented in a new branch. The branch name should correspond to the following formula: `TFL` + `task number` + `task name`.

  - `TFL` - "Twenty Four Linear".
  - `Task number` - a number that Linear generates on task creation and it is unique.
  - `Task name` - a short name to define an implementation scope.

    ```php
    // Avoid; No context; "tfl" should be in uppercase;
    tfl-111-fixes
    ```

    ```php
    // Prefer
    TFL-111-header-refactoring
    ```

    ```php
    // Prefer
    TFL-111-public-page-fixes
    ```

- Follow [Linear's task statuses](https://tppr.me/8EemA);

- The commit message should start with the task number. Example: `TFL-179: Add new feature`. Follow commit scope and message. Avoid messages like `"fixed styles"`, prefer - `"fixed login form styles"`;

  ```js
  // Avoid; No task identifies
  Fixed header styles
  ```

  ```js
  // Avoid; No context
  TFL-111: Fixed styles
  ```

  ```js
  // Avoid; No context
  TFL-111: Fixes after code review
  ```

  ```js
  // Prefer
  TFL-111: Created header markup, styles
  ```

- When a task is completed, create Pull Request (PR) in GitHub, request Andriy to code review. You are able to move forward with other tasks while the current task in code review status.

- PR's title should contain the Linear's task identifier according to the next formula: `TFL` + `task number`. LinearBot tracks the PRs and titles. When the title corresponds to Linear's task identifier, Linear's link, task title, and its description will be added as a comment by the bot automatically. Follow next title template:

  ```js
  // Avoid; No context
  TFL-11: Header
  ```

  ```js
  // Prefer
  TFL-11: Update treatments page styles
  ```

- Fill PR description. Add a changelog, what you have done, some special cases or comments, you would like to note.
