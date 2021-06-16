# Classes

We've focused on writing lines and blocks of code well. But we need to pay attention to higher levels of code organization.

## Class Organization

- Begin with list of variables
  1. Public static constants
  2. private static variables
  3. Private instance variables
  - Seldom reason to have a public variable

### Encapsulation

- Loosening encapsulation is always a last resort.

## Classes Should Be Small!

1. Should be small
2. Should be smaller than that.

- With functions, we measured size by physical lines.
- With classes, we measure with _responsibilities_

## Single Responsibility

- Classes should have one responsibility

## Cohesion

- Classes should have a small number of instance variables.
- The more vriables a method manipulates the more cohesive that methodis to its class.
- A class in which each variable is used by each method is maximally cohesive.

## Organizing for Change

- Change is continual
- Every change subjects us to the risk of breaking current functionality
- In a clean system, we organize our classes _so as to reduce the risk of change_

## Isolating from Change

- Needs will change, therefore code will change.
- Our classes should adhere to the Dependency Inversion Principle
  - Our classes should depend upon abstractions, not on concrete details
  - We can do this by decoupling our system. Interfaces are always a go-to.
