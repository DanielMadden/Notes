# Why I Chose Akita Over NgRx

## https://dev.to/joaomarcusc/why-i-chose-akita-over-ngrx-4adb

<br/>

## Too much boilerplate

Let's start with the boilerplate issue. Whenever I needed to use NgRx for a specific part of my webapp, I had to:

- Create a set of actions
- Create a reducer function with a big and ugly switch statement
- Add the reducer to the StoreModule.forRoot or StoreModule.forFeature call.
- Call theselect function in my component or create selectors to get the current state.
- Call the dispatch function to dispatch an action.

What if I needed to fetch data from a service? Well, then I'd have to:

- Add an action that will be dispatched when data needs to be fetched
- Add an action that will be dispatched when the call finished successfully
- Add an action that will be dispatched when the call fails
- Add an Effects class that will call the data fetch service itself and do the action dispatching
- Add the Effects class to the EffectsModule call

It's not a big problem if it's not often needed. Data feching is what I mostly do, though! Effects can become huge and not so easy to maintain.

<br/>

## Too many concepts

I have to admit, a part of our problem is that developers only knew AngularJS (1.5), not Angular (2+). They had to learn about components, modules, DI. I know AngularJS had them before, but Angular (2+) is so different it feels like a new framework. They also had to learn about RxJS, Observables, and other concepts that aren't trivial. And then, suddenly, they also had to learn about Actions, Dispatchers, Reducers, Effects, Selectors! Maybe I should've seen it coming, but even if they already felt comfortable with Angular, it seems that those concepts aren't easy to grasp unless you knew Redux(-ey) libraries before.

<br/>

## NgRx feels alien to Angular

Whenever I was using NgRx, I felt like maybe it could make more use of Angular. For example, instead of the big and ugly reducer, decorators should be used by default. Some libraries try to solve that problem, but they felt subpar to me, and they sometimes introduced even more complexity, like needing specific work to avoid problems with AOT compilation. If you're using NgRx, I recommend ngrx-actions.

My coworkers had a very, very difficult time "getting" NgRx, and they spent more time trying to understand NgRx along with Angular than developing the application itself. So, we decided to drop NgRx entirely and letting everyone do as they please, because there was a deadline to meet.

<br/>

## Dropping Redux? Not yet!

I didn't quit trying do use Redux-style libraries in my app, but I decided to try the alternatives. Two of them looked more mature and well-tested:

- NgXs: More simple than NgRx, but it still had some specific parts that irritates developers, such as the need to declare an Action and corresponding specific dispatch method in a separate place.
- Akita: Even simpler than NgXs. Instead of actions and dispatchers, just a plain service, even for async calls. Queries are plain observables.

<br/>

## The winner: Akita

Now, let's see what it takes to introduce Akita in a specific project

- Create a store as a class extending EntityStore
- Create a service that injects the store and expose actions as service methods. No need for actions, reducers, dispatchers, annotated methods, etc. Just plain methods that updates the state.
- Create a class extending QueryEntity so we create selectors
- Need to call a HTTP service? No problem, just create a service method.

It could be even easier, but this seems easy enough I can now talk about it without raising many eyebrows. Maybe I will give NgRx or NgXs another chance, but for now I'll stay with the simpler choice.
