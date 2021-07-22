## Advanced Effects

<br/>

What Map Operator Should I Use?

---

| map        | effect                                         | use                        |
| ---------- | ---------------------------------------------- | -------------------------- |
| mergeMap   | Subscribe immediately, never cancel or discard | Deleting items             |
| concatMap  | Subscribe after the last one finishes          | Updating or creating items |
| exhaustMap | Discard until the last one finishes            | Non-parameterized queries  |
| switchMap  | Cancel the last one if it has not completed    | Parameterized queries      |

---

<br/>
**concatMap** is great for making sure _every stream gets completed in order_, but it does create a lot of **backpressure**.
<br/>
<br/>
<br/>
Wow... okay... I just broke down and stepped through the effect code and it all makes a lot more sense now:

```js
// Create the effect
getAllBooks$ = createEffect(() => {
  // Return an observable
  return this.actions$.pipe(
    // ofType() takes in an observable of actions
    ofType(BooksPageActions.enter),
    // Exhaust map discards any new streams until the current stream finishes
    exhaustMap((actions) => {
      // Return an Http Observable
      return (
        this.booksService
          // Get all books
          .all()
          // Pipe the Http Observable into a map operator that sends the books to the booksLoaded action. This action will trigger the reducer that will then place these books into the state.
          .pipe(map((books) => BooksApiActions.booksLoaded({ books })))
      );
    })
  );
});
```

## Effects Examples

```js
// Doesn't need to start with an action. Can be an observable.
@Effect() tick$ = interval(60000).pipe(
    map(()=>Clock.tickAction(new Date()))
)
```

```js
// Websocket Observable:
@Effect() ws$ = fromWebSocket("/ws").pipe(map(message => {
    switch(message.kind) {
        case "book_created":{
            return WebSocketActions.bookCreated(message.book);
        }
        case "book_updated":{
            return WebSocketActions.bookUpdated(message.book);
        }
        case "book_deleted":{
            return WebSocketActions.bookDeleted(message.book);
        }
    }
}))
```

```js
// Error Handling:
@Effect()
createBook$ = this.actions$.pipe(
    ofType(BooksPageActions.createBook.type),
    mergeMap(action => this.bookService.create(action.book).pipe(
        map(book => BooksApiActions.bookCreated({book})),
        catchError(error => of(BooksApiActions.createFailure({
            error,
            book: action.book
        })))
    ))
)
```

```js
// Toasts:
@Effect() promptToRetry$ = this.actions$.pipe(
    ofType(BooksApiActions.createFailure),
    mergeMap(action =>
        this.snackBar
            .open("Failed to save book.", "Try Again", {
                duration: 12000
            })
            .onAction()
            .pipe(
                    map(()=>BooksApiActions.retryCreate(action.book))
            )
    )
)
```

```js
// Opening Dialogs ({dispatch: false})
@Effect({dispatch: false})
openUploadModal$ = this.actions$.pipe(
    ofType(BooksApiActions.openUploadModal),
    tap(()=> {
        this.dialog.open(BooksCoverUploadModalComponent)
    })
)
```

## Entities

- Working with collections should be fast
- Collections are very common
- Common set of basic state operations
- Common set of basic state derivations

```js
// Faster to pull from dictionary
interface EntityState<Model> {
  ids: string[] | number[];
  entities: { [id: string | number]: Model };
}
```

```js
export interface MoviesState extends EntityState<Movie>
{
    // No collection array is necessary since the EntityState type handles the collection/dictionary on its own
    activeMovieId: string | null;
}
export const adapter = createEntityAdapter<Movie>();
export const initialState: Movie = adapter.getInitialState(
    {
        // Again, no (initial) collection need be set
        activeMovieId: null
    }
)
```

```js
// Selectors...
export const {
  selectIds, // Give array of ids
  selectEntities, // Give dictionary of models by id
  selectAll, // The array of items
  selectTotal, // Total number of items
} = adapter.getSelectors();
```

```js
// Before Entity
export const booksReducer = createReducer(
  initialState,
  on(BooksApiActions.booksLoaded, (state, action) => {
    return {
      ...state,
      collection: action.books,
    };
  })
);
// After Entity
export const booksReducer = createReducer(
  initialState,
  on(BooksApiActions.booksLoaded, (state, action) => {
    return adapter.addAll(action.books, state);
  })
);
```

```js
// Before Entity
export const selectActiveBook = createSelector(
  selectAll,
  selectActiveBookId,
  (books, activeBookid) => {
    return books.find((book) => book.id === activeBookid) || null;
  }
);
// After Entity
export const selectActiveBook = createSelector(
  selectAll,
  selectActiveBookId,
  (entities, activeBookid) => {
    return activeBookId ? entities[activeBookId] : null;
  }
);
```
