- Open source libraries for Angular
- Built with reactivity in mind
- State management and side effects
- Community driven

- How does NgRx work?

  - NgRx prescribes an architecture for managing the state and side effects in your Angular application. It works by deriving a stream of updates for your application's components called the "action stream."
  - You apply a pure function called a "reducer" to the action stream as a means of deriving state in a deterministic way.
  - Long running processes called "effects" use RxJS operations to trigger side effects based on thses updates and can optionally yield new changes back to the actions stream.

- Terms

  - **Side Effect:** Anything reaching out into the outside world that will potentially give back an unknown.
  - **State Change:** Anything in memory that is updated

- NgRx Mental Model: _state flows down, changes flow up_

- In an NgRx application, components simply connect data. They don't have side effects and they don't manage state.

- Inputs & Outputs offer indirection.

  - The components have no idea who the parent ever is.

- NgRx Mental Model: There is indirection between consumer of state, how state changes, and side effects

- Actions

  - A string, clearly describing the event
  - Dispatched by the store service
  - Kinda like a Global @Output() for the whole app

- Effects

  - Trigger side effects
  - Built with observables
  - Can then research out to some service
  - Can be piped

- Reducers

  - Pure functions that handle the actions being dispatched
  - Handle state transitions

- Selectors

  - Responsible for combining and composing data for components
  - Like reducers, just functions
  - Like a Global @Input() for the whole app

- Containers
  - Connect data to components

```html
<search-movies-box (search)="onSearch($event)"></search-movies-box>
<movies-list
  [movies]="movies$ | async"
  (favoriteMovie)="onFavoriteMovie($event)"
></movies-list>
```

```javascript
@Component()
export class SearchMoviesPageComponent {
    movies$: Observable<Movie[]>;

    constructor(private store: Store<AppState>) {
        this.movies$ = store.select(selectMovies);
    }

    onSearch(searchTerm: string) {
        this.store.dispatch(searchMoviesAction(searchTerm))
    }
}
```

"Selectors are like an NgRx-ified version of inputs"

```javascript
@Input() movies: Movie[]

store.select(selectMovies)
```

"Dispatchers/Actions are like an NgRx-ified version of outputs"

```javascript
@Output() search: EventEmitter<string>()

this.store.dispatch(searchMoviesAction(searchTerm))
```
