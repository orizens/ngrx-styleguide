## Reducers

1. [Reducers should have its own directory](#reducers-should-have-its-own-directory)
1. [Reducers Included File](#reducers-included-file)
1. [combining reducers](#combining-reducers)

### Reducers should have its own directory
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
