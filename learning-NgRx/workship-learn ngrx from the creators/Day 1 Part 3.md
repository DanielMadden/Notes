```js
class MoviesPageComponent {
  movies$: Observable<MovieModel[]>;

  constructor(store: Store<State>) {
    this.movies$ = store.select(selectAllMovies);
  }
}
```

```html
<app-books-list
  [books]="books$ | async"
  (select)="onSelect($event)"
  (delete)="onDelete($event)"
></app-books-list>
```
