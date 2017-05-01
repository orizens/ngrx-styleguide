# ngrx Style Guide

## Purpose
The idea for this styleguide is to present commonly used techniques for working with ngrx suite and serve as a kind of a cookbook/recipes with a problem/solution theme.  
The purpose of this style guide is to provide guidance on how to integrate ngrx-X-tool by showing the conventions used by users of the community.

[Introduction Blog Post]()

## Projects Following The Styleguide
- [Echoes Player (Angular 4 version)](http://github.com/orizens/echoes-player) 

Please open an issue to add your project/suggestion

-----------------------
## Table of Contents

1. [Creating A CoreStoreModule](#creating-a-corestoremodule)
1. [Store Single Directory](#store-single-directory)
1. [Reducers](#reducers)
    1. [Reducers should have its own directory](#reducers-should-have-its-own-directory)
    1. [Reducers Included File](#reducers-included-file)
    1. [combining reducers](#combining-reducers)
1. [Actions](#actions)
    1. [actions file location](#actions-file-location)
    1. [naming actions (for state)](#naming-actions-for-state)
    1. [naming actions for side effects](#actions-for-side-effects)
    1. [action creators](#action-creators)

### not added yet
1. [using Side Effects](#using-side-effects)
1. [consuming reducers in components](#consuming-reducers-in-components)
1. [using selectors](#using-selectors)

## Creating A CoreStoreModule
**DO** create a single core store module.  
**Why?** it follows the [single responsibility principle](https://wikipedia.org/wiki/Single_responsibility_principle) (SRP) for having a self contained module for managing state (or store)
It should include:  
1. Bootstraping of the store with ```StoreModule.provideStore({})```
2. The application's actions as providers  

**location**: ```app/core/store/index.ts``` 

## Store Single Directory
**DO** place the store in the application's core directory.  
**Why?**: The store is regarded as part of the application's core state layer - a single source of truth.
**Why?**: it's easier to maintain and manage the state layer in one place.

```
- src
  - app
    - core
      - store
        - now-playing
        - player
        - player-search
        - user-profile
```

## Reducers should have its own directory
**DO** place each reducer in its own directory.  
**Why?**: it's easier to locate it.  
**Why?**: other related files will be placed in the same directory (actions, spec, selectors, etc...).  
```
- src
  - app
    - core
      - store
        - now-playing
          - now-playing.reducer.ts
        - player
        - user-profile
```
## Reducers
### Reducers Included Files
**DO** create separated files in the reducer's directory for: reducer, reducer's spec, reducer's actions and reducer's selectors. Finally, use **index.ts** as a barrel for exporting each file's content.  
**Why?** it's easier when developing to locate each relevant class/file

```
- src
  - app
    - core
      - store
        - now-playing
          - index.ts
          - now-playing.reducer.ts
          - now-playing.spec.ts
          - now-playing.actions.ts
          - now-playing.selectors.ts
```
### Reducer "barrel" with "index.ts"
**DO** create an "index.ts" barrel for exporing reducer's files/class
**Why?** it's easier to import any of the relevant reducer's entities through the reducer's directory path.
**Why?** shorter path leads to less verbose path. 

```typescript
export * from './app-player.reducer';
export * from './app-player.actions';
export * from './app-player.selectors';
```

When importing:  
```typescript
import { AppPlayerActions } from '../store/app-player';
```

## Actions
### actions file location
**DO** place actions in a reducer's directory.  
**Why?**: actions are a core part of a reducer.  
**Why?**: it's easier to maintain and manage actions in one place.

### naming actions (for state)  
Note: look at [actions for side effects here](#actions-for-side-effects)  
**DO** name actions with a unique name and captial letters - VERB + NOUN.  
**DO** name actions values with - Prefix + VERB + NOUN.  
**Why?**: it's readable.  
**Why?**: actions can be filtered and viewed in redux dev tool easily.  
**Why?**: uniqueness is for making sure only one reducer handles the action.  
```typescript
const UPDATE_FILTER = '[PlayerSearch] UPDATE_FILTER';
const ADD_RESULTS = '[PlayerSearch] ADD_RESULTS';
```

### naming naming actions for side effects
**DO** name actions with **suffix** that indicate **start** or **end** of async operation.  
**DO** name actions with suffixes which indicate start or end of async operation.  
**Why?**: it's easier to maintain and understand.  
```typescript
const SEARCH_STARTED = '[PlayerSearch] SEARCH_STARTED';
const SEARCH_SUCCESS = '[PlayerSearch] SEARCH_SUCCESS';
```
### action creators 
**DO** use action creators for composing an action object.  
**DO** place action creators in the **reducerName.actions.ts** file.  
**Why?**: it's easier to reference to the actions.    

**DO** use one of the following patterns for creating an action creator.  

```typescript  
// a standalone function
export function updateFilter(payload: string): Action {
  return { type: UPDATE_FILTER, payload }
}
/* as in ngrx-example-app */
export class UpdateFilterAction implements Action {
  readonly type = UPDATE_FILTER;

  constructor(public payload: string) { }
}

// as part of actions class
export const ActionTypes = {
  UPDATE_FILTER: '[PlayerSearch UPDATE_FILTER]'
};

export class PlayerSearchActions {
  
  updateFilter = (payload: string) =>
  ({ type: ActionTypes.UPDATE_FILTER, payload });
}

// use ActionsCreatorFactory at: 
// ~ npm i ngrx-action-creator-factory
// allows type check for the payload when used
export updateFilter = ActionCreatorFactory.create<string>(ActionTypes.UPDATE_FILTER);
```
Copyright (c) [Oren Farhi](http://orizens.com)

**[Back to top](#table-of-contents)**