## Creating A CoreStoreModule
**DO** create a single core store module.  
**Why?** it follows the [single responsibility principle](https://wikipedia.org/wiki/Single_responsibility_principle) (SRP) for having a self contained module for managing state (or store)
It should include:  
1. Bootstraping of the store with ```StoreModule.provideStore({})```
2. The application's actions as providers  

**location**: ```app/core/store/index.ts``` 
