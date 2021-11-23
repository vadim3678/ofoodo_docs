# FAQ

1.  Откуда взять конкретные API для групп на главной странице ? Swagger мы им
    отправили и там конкретно откуда надо взять эту информацию ?

see in [home](home.md)

2.  Если блюдо выбираем на странице ресторана, как понять какой reuqired, а какой optional параметр
    для этого блюда? И как должны отправлять эту информацию в Бэк Энд.

see in [ordering](ordering.md)

3. Каким видом отправляется в бэк информация, после чего происходит оплата (JSON)
4. Какой эндпоинт и какие параметры нужны для оплаты

> 5. Как происходит добавление банковской карты
> 6. Как запросить сохраненную информацию о карте с Бэк энда

see in [payment](payment.md)

7. Как вызвать (посмотреть) стоимость доставки?

8. Нужен API регистрации/входа в facebook и google

9. Конкретно откуда надо взять “teamreferer” параметр, который в HEADERах передается requestам, когда
   берем информацию о конкретном ресторане

10. statusId и checkoutType ENUM нужны нам во всех вариантах, которые есть.

Now **_checkoutType_** is not in use

```ts
checkoutTypeName: tCheckoutTypeName;
type tCheckoutTypeName = "delivery" | "pickUp" | "reservation" | "withoutMenu";
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

11. https://apis.bonee.net/order/api/v1/Orders/orders/{ID ????}/2020-08-03/2021-11-10 21:56:56/-1/-1/ когда берем список ордеров, этот ID параметр, который записан в линке, откуда его взять.

Now work fine with _undefined_. May be it's obsolete
