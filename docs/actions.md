## Actions
1. [actions file location](#actions-file-location)
1. [naming actions (for state)](#naming-actions-for-state)
1. [naming actions for side effects](#actions-for-side-effects)
1. [action creators](#action-creators)

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

### naming actions for side effects
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
export const updateFilter = ActionCreatorFactory.create<string>(ActionTypes.UPDATE_FILTER);
```