# Subject and BehaviorSubject

## Unicast vs. Multicast

### Observable is Unicast

```
Observable ===> Subscriber

Observable ===> Subscriber
```

### Subject is Multicast

```
         /===> Subscriber
        /
Subject     ===> Subscriber
        \
         \===> Subscriber
```

## Subject

```javascript
private categorySelectedSubject = new Subject<number>();
categorySelectedAction$ = this.categorySelectedSubject.asObservable()
```

```javascript
onSelected(categoryId): void {
    this.categorySelectedSubject.next(+categoryId);
}
```

```javascript
products$ = combineLatest([
  this.productService.products$,
  this.categorySelectedAction$,
]).pipe(
  map(([products, categoryId]) =>
    products.filter((product) =>
      categoryId ? product.categoryid === categoryId : true
    )
  )
);
```
