Akita over NgRx: https://dev.to/joaomarcusc/why-i-chose-akita-over-ngrx-4adb

- Nice breakdown article as to why Akita can be a better option
- Somewhat outdated, since

10 Reasons why you should use Akita: https://engineering.datorama.com/10-reasons-why-you-should-start-using-akita-as-your-state-management-solution-66b63d033fec

Choosing A State Management Library for Angular Enterprise Applications: https://blogs.perficient.com/2020/07/21/choosing-a-state-management-library-for-angular-enterprise-applications/

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

NgRx, NgXs, or Akita: https://www.youtube.com/watch?v=4OliKx8wxSI

- Boring video, but good walkthrough of approaching the same problem with different libraries

Reddit conversation: https://www.reddit.com/r/angular/comments/g6tx8y/ngrx_vs_ngxs_vs_rxjs_vs_akita/

- Cool to get different perspectives

Comparison of NgRx, Akita, and @ng-state/store: https://medium.com/@vpranskunas/deep-comparison-of-state-management-solutions-in-angular-562985d4474e

- X: Completely biased, trying to sell off idea of using HIS library. Doesn't know how to use Akita efficiently
