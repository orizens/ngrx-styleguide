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