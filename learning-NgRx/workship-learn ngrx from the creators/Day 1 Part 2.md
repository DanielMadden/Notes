- Store
  - State contained in a single state tree
  - State in the store is immutable
  - Slices of state are updated with reducers
- Selectors
  - Allow us to query our store for data
  - Recompute when their inputs change
  - Fully leverage memoization for performance
  - Selectors are fully composable

```js
export const selectActiveMovieId = (state) => {
  return state.activeMovieId;
};
```

```js
export const selectActiveMovie = (state: State) => {
  const movies = selectMovies(state);
  const activeMovieId = selectActiveMovieId(state);

  return movies.find((movie) => movie.id === activeMovieId) || null;
};
```

```js
export const selectActiveMovie = createSelector(
  selectMovies,
  selectActiveMovieId,
  (movies, activeMovieId) => {
    return movies.find((movie) => movie.id === activeMovieId) || null;
  }
);
```

```js
export const selectEarningsTotals = createSelector(selectAll, (movies) => {
  return calculateGrossMoviesEarnings(movies);
});
```

```js
export const selectEarningsTotals = createSelector(
  selectAll,
  calculateGrossMoviesEarnings
);
```

```js
// Getter Selectors
export const selectAll = (state: State) => state.collection;
export const selectActiveBookId = (state: State) => state.activeBookId;

// Complex Selector, UNOPTIMIZED
export const selectActiveBook_unoptimized = (state: State) => {
  // Inputs
  const books = selectAll(state);
  const activeBookid = selectActiveBookId(state);

  // Computation
  return books.find((book) => book.id === activeBookId);
};

// Complex Selector, OPTIMIZED
export const selectActiveBook = createSelector(
  selectAll,
  selectActiveBookId,
  (books, activeBookId) => {
    return books.find((book) => book.id === activeBookId);
  }
);
```
