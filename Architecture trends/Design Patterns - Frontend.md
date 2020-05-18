### React Hooks and Container Pattern
* **React Hooks let you manage state, as well as component lifecycle, in functional React components**. That effectively makes everything functional and arguably, even eliminates the need for using class-based components.
* **Container Pattern is commonly used to separate data fetching/logic, events, and state from presentational components** (aka, dumb components).
  * This can be particularly helpful if you want to reuse your presentational components in other use-cases, in your current project/codebase or in other projects.
  * This pattern is really useful when having a single codebase for ios and web.
    * Web - React Router 
    * iOS - React Navigation
  * I think using the container pattern in small scale apps is a bit of an overkill, no that we have React Hooks. 
