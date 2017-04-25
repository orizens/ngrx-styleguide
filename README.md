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

1. [Store Single Directory](#store-single-directory)
1. [Creating A CoreStoreModule](#creating-a-corestoremodule)
1. [combining reducers](#combining-reducers)
1. [using Side Effects](#using-side-effects)
1. [consuming reducers in components](#consuming-reducers-in-components)
1. [using selectors](#using-selectors)

## Store Single Directory
- The store should be placed in the application's core directory.
- each reducer should have a dedicated directory
:

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

## Creating A CoreStoreModule
A single core store module should include:  
1. Bootstraping of the store with ```StoreModule.provideStore()```
2. The application's actions as providers  

**location**: ```app/core/store/index.ts```  

Copyright (c) [Oren Farhi](http://orizens.com)

**[Back to top](#table-of-contents)**