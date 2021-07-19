## Akita over NgRx: https://dev.to/joaomarcusc/why-i-chose-akita-over-ngrx-4adb

- Nice breakdown article as to why Akita can be a better option
- Somewhat outdated, since the main issue with NgRx was the boilerplate code. Since then NgRx has made efforts to make the library more concise.
- Akita is much simpler than both NgRx and NgXs. Instead of actions and dispatchers, it just uses a plain service, even for async calls. Queries are plain observables.
- Benefits of Akita:
  - Creates a store as a class extending EntityStore
  - Creates a service that injects the store and exposes actions as service methods.
  - No need for actions, reducers, dispatchers, annotated methods, etc. Just plain methods that update the state.
  - Creates a class extending QueryEntity for creating selectors
  - Calling an HTTP service is as simple as creating a service method.
- Gleaning from the comments:
  - "We are currently facing the same problem with ngrx. We have a quite complex angular app that grew over time and now **_has a ridiculous amount of boilerplate code for ngrx._** _my biggest fear is that new team members will have a really hard time understanding what is going on._ and **_the biggest problem of all that boilerplate code is that you can't understand what are the vital parts, as the concept is not self-explanatory at all._** akita looks like a good alternative."
    - "Did you give Akita a try? How is that working for you?"
      - "Yes, we actually did. We switched one single page application completely and will start with the second soon. So far it's working really well. **_We were able to reduce complexity and increase maintainability along the way._**"
  - "Hey, I have been working with Angular+NGRX for the last 2.5 years. I think the strongest part of ngrx is the actions. Once we done with one action stream(with side effects), yes its like a boilerplate. To me ngrx is super awsome. **_But for a fresher its very difficult to understand._** I recently read about AKITA, yes what you said was absolutely correct and AKITA is super cool. I am trying to migrate my application from ngrx to AKITA."
    - "IMHO NgRx would really benefit from a Akita-like solution that transforms a service into methods in actions+reducers. **_For a larger project, actions+reducers start multiplying like there's no tomorrow._** There are pet peeves of mine I didn't mention, like the need to declare the reducers in StoreModule (when Angular has builtin Dependency Injection), weird AOT issues when dealing with different libraries, such as ngrx-forms + ngrx-actions. **_I would still recommend NgRx to a team that's familiar with React, though._**"
  - "I think NGRX Entities and NGRX Data solves most of the boilerplate everyone hate so much.
    You can use the cli to generate entities just like you do in Akita
    "ng generate entity my-entity"
    You gain the full redux + redux devtools
    Effects are also very well handled in NGRX.
    Selectors are now memoized (cache) and they can use rxjs operators of course
    Data normalization is also something that comes out of the box when using NGRX.
    So **_I agree that NGRX in the past had a lot of issues and the boilerplate was a mess but it is changing rapidly and in a good direction._**
    I would still open up the discussion with the team for every new project cause stuff can change over time."
    - "I think right now Ngrx and Akita are very similar. NGRX improves a lot on reducing boilerplate. And NGRX can work with REDUX DEVTOOLS. Akita is a pretty neat library for other framework like vue but in Angular, I think NGRX is still the best choice."

---

## Choosing A State Management Library for Angular Enterprise Applications: https://blogs.perficient.com/2020/07/21/choosing-a-state-management-library-for-angular-enterprise-applications/

- NgRx
  - The most popular state management library in Angular
  - 5,900 stars on Github
  - In 2020 made many efforts to reduce boilerplate code as much as possible
- NgXs
  - Requires less of a dependency on knowledge of RxJs
  - Combines actions and reducers into one source file
  - More concise than NgRx
  - Also allows you to mutate the store directly
- Akita
  - Backed by Datorama, giving them a degree of accountability
  - Main focus was to eliminate boilerplate, which is the most common developer grievance with NgRx
  - Not exclusive to Angular (not important for this project but is a good benefit to personal growth as a developer)
  - May not be as concise as NgXs, but is the most readable implementation of the Redux design pattern
  - Reminiscent of traditional Angular services (makes it more approachable)
  - More geared towards object-oriented design principles as opposed to the functional programming style of the preceding options.

---

## 10 Reasons why you should use Akita: https://engineering.datorama.com/10-reasons-why-you-should-start-using-akita-as-your-state-management-solution-66b63d033fec

1. Akita is a vertan in the field
2. Akita has the backing of **Datorama**
3. Akita is easy to pick up
4. Akita isn't coupled with Angular
5. Akita has a 0 bugs policy
6. Akita is well documented
7. Akita's community is growing, fast
8. Akita is well suited for full-stack developers
   - Objected Oriented over Functional Programming
9. Akita developers are easy to reach
10. Full suite of accompanying plugins
    - Redo-Undo
    - Persist State
    - Dirty Check
    - Pagination
    - Devtools
    - Router integration
    - CLI

---

### Reddit conversation: https://www.reddit.com/r/angular/comments/g6tx8y/ngrx_vs_ngxs_vs_rxjs_vs_akita/

- Cool to get different perspectives

### NgRx, NgXs, or Akita: https://www.youtube.com/watch?v=4OliKx8wxSI

- Boring video, but good walkthrough of approaching the same problem with different libraries

### **X:** Comparison of NgRx, Akita, and @ng-state/store: https://medium.com/@vpranskunas/deep-comparison-of-state-management-solutions-in-angular-562985d4474e

- **X:** Completely biased, trying to sell off idea of using HIS library. The comments proved that the writer didn't even know how to use Akita efficiently
