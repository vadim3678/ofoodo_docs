# FAQ

### statusId  и checkoutType ENUM нужны нам во всех вариантах, которые есть.
Now ***checkoutType*** is not in use
```ts
checkoutTypeName: tCheckoutTypeName;
type tCheckoutTypeName = 'delivery' | 'pickUp' | 'reservation' | 'withoutMenu';

```

```ts
enum StatusIdENum {
  AWAITINGVALIDATION = 2,
  STOCKCONFIRMED = 3,
  SHIPPED = 5,
  CANCELLED = 6,
  COMPLETED = 7,
  INPROCESS = 8,
  READY = 9,
  STARTSHIP = 10,
}
```

### https://apis.bonee.net/order/api/v1/Orders/orders/{ID ????}/2020-08-03/2021-11-10 21:56:56/-1/-1/ когда берем список ордеров, этот ID параметр, который записан в линке, откуда его взять.

Now work fine with *undefined*. May be it's obsolete
