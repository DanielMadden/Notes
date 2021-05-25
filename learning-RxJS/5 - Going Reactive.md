# Introduction

## Module Overview

- Working with the async pipe
- Handling errors
- Improving change detection
- Declarative pattern for data retrieval

## RxJS Features

- catchError
- EMPTY
- throwERror

<br>
<br>

# Async Pipe

## `'products$ | async'`

- Subscribes to the Observable when component is initialized
- Returns each emitted value
- When a new item is emitted, component is marked to be checked for changes
- Unsubscribes when component is destroyed

<br>

## Class with async pipe

```javascript
// UNREACTIVE
products: Product[] = [];

constructor(private productService: ProductService) {}

ngOnInit() {
    this.productService.getProducts()
    .subscribe(products => this.products = products);
}

// REACTIVE
products$: Observable<Product[]>;

constructor(private productService: ProductService) {}

ngOnInit() {
    this.products$ = this.productService.getProducts();
}
```

<br>

## Template with an async pipe

```html
<!-- UNREACTIVE -->
<div *ngIf="products">
  <table>
    <tr *ngFor="let product of products">
      <td>{{ product.productName }}</td>
      <td>{{ product.productCode }}</td>
    </tr>
  </table>
</div>

<!-- UNREACTIVE -->
<div *ngIf="products$ | async as products">
  <table>
    <tr *ngFor="let product of products">
      <td>{{ product.productName }}</td>
      <td>{{ product.productCode }}</td>
    </tr>
  </table>
</div>
```

<br>
<br>

# Handling Errors: `catchError`

- ## Catches any errors that occur on an Observable
  - `catchError(this.handleError)`
- ## Used for catching errors and
  - Rethrowing an error
  - ### Replacing the errored Observable to continue after an error occurs
    - An Observable created from hard-coded or local data
    - An Observable that emits an empty value or empty array
    - The EMPTY RxJS constant
      - Emits no items and then completes

## Catch and Replace:

- Catches and replaces the stream
- The error handler in the subscription won't be triggered, since it was already "caught" and handled appropriately. The mock observer continues emitting

```javascript
// Product Service
return this.http.get<Product[]>(this.productsUrl)
  .pipe(
    catchError(err => {
      console.error(err);
      return of(
        [
          {id:1, productName: 'card'},
          {id:2, productName: 'hammer'}
        ]
    );
  });
```

```javascript
// Product List Component
ngOnInit() {
  this.productService.getProducts()
    .subscribe(
      products => this.products = products,
      err => this.errorMessage = err
    );
}
```

## `catchError`

- `catchError` is an error handling oeprator
  - Takes in an input stream, subscribes
  - Creates an output stream
- When a source item is emitted
  - Item is emitted to the output stream
- If an error occurs
  - Catches the error
  - Unsubscribes from the input stream
  - Returns a replacement Observable
  - Optionally rethrows the error

## Catch and Rethrow:

```javascript
// Product Service
return this.http.get<Product[]>(this.productsUrl)
  .pipe(
    catchError(err => {
      console.error(err);
      return throwError(err);
    );
  });
```

## `throwError`

- Creates an Observable that emits no items
- Immediately emits an error notification
- Used for
  - Propogating an error

## `EMPTY`

- Creates an Observable that emits no items
- Immediately emits a complete notification
- Used for
  - Returning an empty Observable

```javascript
// Product List Component
this.products$ = this.productService.getProducts().pipe(
  catchError((err) => {
    this.errorMessage = err;
    return EMPTY;
  })
);
```

<br>
<br>

# Improving Change Detection

## Benefits of an Async Pipe

- No need to subscribe
- No need to unsubscribe
- Improve change detecion

## Change Detection Strategies

| Default                               | OnPush                                                     |
| ------------------------------------- | ---------------------------------------------------------- |
| Uses the default checkAlways strategy | Improves performance by minimizing change detection cycles |
| **Every component is checked when:**  | **Component is only checked when:**                        |
| - Any change is detected              | - @Input properties change                                 |
|                                       | - Even emits                                               |
|                                       | - A bound Observable emits                                 |

<br>
<br>

# Declarative Pattern for Data Retrieval

## Common Pattern

```javascript
// Product Service
private productsUrl = 'api/products';
getProducts(): Observable<Product[]> {
  return this.http.get<Product[]>(this.productsUrl)
  .pipe(
    catchError(this.handleError)
  );
}
```

```javascript
// Product List Component
ngOnInit() {
  this.products$ = this.productService.getProducts()
  .pipe(
    catchError(err +> {
      this.errorMessage = err;
      return EMPTY;
    })
  );
}
```

## Declarative Pattern

```javascript
// Product Service
private productsUrl = 'api/products';

products$ = this.http.get<Product[]>(this.productsUrl)
  .pipe(
    catchError(this.handleError)
  );
```

```javascript
// Product List Component
products$ = this.productService.products$.pipe(
  catchError((err) => {
    this.errorMessage = err;
    return EMPTY;
  })
);
```

## Benefits of a Declarative Approach

- Leverages the power of RxJS Observables and operators
- Effectively combine streams
- Easily share Observables
- Readily react to user actions
