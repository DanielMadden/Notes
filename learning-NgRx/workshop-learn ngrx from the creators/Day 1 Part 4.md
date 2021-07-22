- Effects
  - Processes that run in the background
  - Connect your app to the outside world
  - Often used to talk to services
  - Written entirely using RxJS streams

```js
// Look similar to services:
@Injectable()
export class MoviesEffects {
    constructor(
        private actions$: Actions,
        private moviesService: MoviesService
    ) {}

    @Effect() loadMovies$ = this.actions$.pipe(
        ofType(MoviesPageActions.enter),
        mergeMap(()=>
            this.moviesService.all().pipe(
                map(movies =>
                MoviesApiActions.moviesLoaded({movies})
                )
            )
        )
    )
}
```

```js
// Register in AppModule:
EffectsModule.forFeature([MoviesEffects]);
```
