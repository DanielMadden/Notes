Why use for State Management?

- Creates maintainable, explicit applications through the use of single state and actions in order to express state changes
- For cases where one does not need global, application-wide solutions for state

Do I need NgRx Store?

- **S**hared: state that is accessed by many components and services
- **H**ydrated: state that is persisted and rehydrated from external storage
- **A**vailable: state that needs to be available when re-entering routes
- **R**etrieved: state that must be retrieved with a side-effect
- **I**mpacted: state that is impacted by actions from other sources

NgRx is not the quickest way to write code. It encourages the use of _many_ files.

A solid understanding of **RxJS** and **Redux** will be very beneficial before learning to use NgRx Store and the other state management libraries.

Key Concepts

- Type Safety
- Immutability and Performance
- Encapsulation
- Serializability
- Testable
