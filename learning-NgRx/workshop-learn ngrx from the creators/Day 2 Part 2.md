## Adapter Collection Methods

| Method       | Description                                                                                  |
| ------------ | -------------------------------------------------------------------------------------------- |
| `addOne`     | Add one entity to the collection                                                             |
| `addMany`    | Add multiple entities to the collection                                                      |
| `addAll`     | Replace current collection with provided collection                                          |
| `setOne`     | Add or Replace one entity in the collection                                                  |
| `removeOne`  | Remove one entity from the collection                                                        |
| `removeMany` | Remove multiple entities from the collection, by id or by predicate                          |
| `removeAll`  | Clear entity collection                                                                      |
| `updateOne`  | Update one entity in the collection                                                          |
| `updateMany` | Update multiple entites in the collection                                                    |
| `upsertOne`  | Add or Update one entity in the collection                                                   |
| `updateMany` | Add or Update multiple entities in the collection                                            |
| `map`        | Update multiple entitites in the collection by defining a map function, similar to Array.map |

## Meta Reducers

- Intercept actions before they are reduced
- Intercept state before it is emitted
- Can change control flow of the Store

```js
function logger(reducer: ActionReducer<any>) {
  return function (state: any, action: Action) {
    console.log("Previous State", state);
    console.log("Next Action", action);

    const nextState = reducer(state, action);

    console.log("Next State", nextState);

    return nextState;
  };
}
```
