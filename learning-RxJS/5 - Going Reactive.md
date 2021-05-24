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
