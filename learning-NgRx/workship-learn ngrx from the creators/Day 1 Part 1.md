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

- Good Action Hygeine
  - Unique events get unique actions
  - Actions are grouped by their source
  - Actions are never reused

```js
export const enter = createAction("[Movies Page] Enter");

store.dispatch(enter());
```

You can also attach metadata:

```js
export const createMovie = createAction(
    '[Movies Page] Create Movie',
    props<{movie: MovieRequiredProps }>()
)

store.dispatch(createMovie({
    movie: movieRequiredProps
}));
```

- Actions will be in their action group file, and the entire group is imported into other classes
- Event Storming:
  1. Using sticky notes, as a group identify all of the events in the system
  2. Identify the commands that cause the event to arise
  3. Identify the actor in the system that invokes the command
  4. Identify the data models attached to each event
- Events in this book app:
  - [Books Page] Create a Book
    - BookRequiredProps
  - [Books Page] Update a Book
    - BookRequiredprops
    - ID of the book being edited
  - [Books Page] Delete a Book
    - ID of the book being deleted
  - [Books Page] Cancel Editing a Book
- Events with the API:

  - [Movies API] Get Movies Success
  - [Movies API] Get Movies Failure

---

- Reducers
  - Produce new states
  - Receive the last state and next action
  - Listen to specific actions
  - Use pure immutable operations

```js
export interface State {
  collection: MovieModel[];
  activeMovieId: string | null;
}

export const initialState: State = {
  collection: [],
  activeMovieId: null,
};
```

```js
export const moviesReducer = createReducer(
  initialState,
  on(
    MoviesPageActions.enter,
    MoviesPageActions.clearSelectedMovie,
    (state, action) => {
      return {
        collection: state.collection,
        activeMovieId: null,
      };
    }
  ),
  on(MoviesPageActions.selectMovie, (state, action) => {
    return {
      collection: state.collection,
      activeMovieId: action.movieId,
    };
  })
);
```
