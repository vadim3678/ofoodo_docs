# Ordering

- [Loading catalog menu](#loading-catalog-menu)
- [Delivery cost](#delivery-cost)
- [Sending an order](#sending-an-order)

## Loading catalog menu

```
  https://apis.bonee.dev/catalog/api/v1/catalog/catalogtree?sellingType={sellingType}
```

sellingType can be the next: 'IsActiveReservation' | 'IsActiveDelivery' | 'IsActivePickup'

specific header:
team referer is a host name of a restaurant. For test ofoodo 'georgia' it wiil be

```
teamreferer: https://georgia.com
```

response is a list of menu groups with list of items. On this step models have not full lists of ingridiets.
When user select product to add to the basket we check the flags

```
activeIngredientExist: true
availableOptionExist: true
```

If true we load the same model with ingridients and options calling

```
https://apis.bonee.dev/catalog/api/v1/catalog/items/single/{id}?sellingType={sellingType}
```

Ingridients can be **'Optional'** for checkbox or **'Required'** for radio button

```ts
{
  ...
  ingridientGroups: [{$id: "14", id: "9f98c3ed-0cd5-39ac-de1a-c69e0a389d12", parentId: null,…},…]
    0: {$id: "14", id: "9f98c3ed-0cd5-39ac-de1a-c69e0a389d12", parentId: null,…}
      $id: "14"
      groupType: "Required"
  ...

  productOptionVariants: [{$id: "10", id: "39b625b8-fb6f-736d-d5d2-11bbbabf703c",…},…]
  productOptionsGroups: [,…]
  ...
}

```

**_productOptionsGroups_** is a list of available options. Flag for default option - **_byDefault: true_**

```ts
  0: {$id: "4", id: "c1e57bfb-fe39-b0d1-c1b7-3aec26421427", name: "a1e9c0aa-127f-0efb-b9b0-f6f84f0a3d6a",…}
    $id: "4"
    deleted: false
    id: "c1e57bfb-fe39-b0d1-c1b7-3aec26421427"
    isNew: false
    name: "a1e9c0aa-127f-0efb-b9b0-f6f84f0a3d6a"
    productOptions: [,…]
    0: {$id: "5", id: "6950d8f9-acc9-6e67-8a66-b30fb0f07d93", header: "bde9efd0-8ea7-d1e1-8249-ddda56bf4b7a",…}
      $id: "5"
      availableCount: 0
      byDefault: true
      deleted: false
      header: "bde9efd0-8ea7-d1e1-8249-ddda56bf4b7a"
      id: "6950d8f9-acc9-6e67-8a66-b30fb0f07d93"
      ingredientGroup: ""
      isNew: false
      sortIndex: 0
      value: ""
    1: {$id: "6", id: "fcd5d592-a51b-46de-e60a-c1a050386802", header: "3c3d1275-f3d4-e488-534d-613bf5d15ff0",…}
    required: false
    sortIndex: 0
    type: "Text"
    ...
```

**_productOptionVariants_** contents intersections of the options with prices for each

```ts
productOptionVariants: [{$id: "10", id: "39b625b8-fb6f-736d-d5d2-11bbbabf703c",…},…]
  0: {$id: "10", id: "39b625b8-fb6f-736d-d5d2-11bbbabf703c",…}
  1: {$id: "11", id: "c50d0f7e-bc96-37e8-15cf-1a2c4f7fd90f",…}
  2: {$id: "12", id: "42df933a-d8ab-6264-0f6e-b70a63038c9e",…}
  3: {$id: "13", id: "080d81e5-d31a-1892-35ea-cd822ebbeab8",…}
  ...
```

where **_optionsIds_** is a list of **_productOption_** id's

```ts
productOptionVariants: [{$id: "10", id: "39b625b8-fb6f-736d-d5d2-11bbbabf703c",…},…]
  0: {$id: "10", id: "39b625b8-fb6f-736d-d5d2-11bbbabf703c",…}
    $id: "10"
    availableCount: 100000
    id: "39b625b8-fb6f-736d-d5d2-11bbbabf703c"
    ingredientGroupIds: null
    optionsIds: ["6950d8f9-acc9-6e67-8a66-b30fb0f07d93", "8400fba1-3189-cb59-3fde-af5591acfbdb"]
    pictureFileName: ""
    pictureUri: ""
    price: 50
  ....
```

[go to start](#ordering)

## Delivery cost

First we get available agents (for now we have singe agent)

```
/marketplace/api/v1.0/ApplicationPortal/GetActiveDelivery?api-version=1.0
```

specific headers:

```
teamreferer: https://{portalHost}.com
authorization: Bearer {token}
```

Response

```json
{
  "existMethods": true,
  "groupType": "DeliverySystem",
  "id": "delivery_agent_id",
  "integrationUrl": "ofoodo.com",
  "isScript": false,
  "logo": "https://ofoodo.ofoodo.com/assets/logo.svg",
  "name": "OfoodoDelivery",
  "secretKey": "secret_key_token",
  "state": "Active",
  "url": "https://d-ofoodo-delivery-az.azurewebsites.net/api"
}
```

To calculate cost we call

```
httpaggregator/api/v1/Order/orderCalculate?api-version=1.0
```

headers:

```
teamreferer: ofoodo
authorization: Bearer {token}
```

payload:

```json
{
  "ApplicationId": "delivery_agent_id",
  "EndCoordinates": {
    "Latitude": 41.74,
    "Longitude": 44.78
  },
  "StartCoordinates": {
    "Latitude": 41.71,
    "Longitude": 44.77
  }
}
```

Response is a number

[go to start](#ordering)

## Sending an order

to create order we call

```
  https://apis.bonee.dev/httpaggregator/api/v1/Basket/paymentauto?api-version=1.0
```

Examples of sent models you can see in **checkout-payloads** folder

### Checkout models

> if time of the order is **_'asap'_** we send to the backend **_time: '00:00'_**

> **_buyerId_** is new guid for every new basket

```ts
export class CheckoutModel {
  name: string;
  lastname: string;
  contactEmail: string;
  countryCode: string;
  country: string;
  phone: string;
  date: string;
  time: string;
  note: string;
  buyerId: string;
  lang: string;
  cardId: string;
  checkoutType: string;
  successPaymentCallback: string;
  failPaymentCallback: string;
  pendingPaymentCallback: string;
  paymentSystem: string;
  asap: boolean;
  items: IBasketItem[];
}
export class CheckoutReservation extends CheckoutModel {
  guestCount: number;
}
export class CheckoutDelivery extends CheckoutModel {
  state: string;
  city: string;
  street: string;
  zipCode: string;
  address: string;
  fullAddress: string;
  applicationId: string;
  lon: string;
  lat: string;
}

export interface IBasketItem {
 /**
   * New guid for added menu item 
   */
  id: string;
  productId: string;
  productName: string;
  description: string;
  unitPrice: number;
  oldUnitPrice: number;
  quantity: number;
  pictureUrl: string;
  pictures: any[];
  /**
    * Represets string of current date and time
    */
  portion: string;
  enableOrder: boolean;
  options: string[];
  optionNames: string[];
  ingredients: string[];
  ingredientNames?: string[];
  isActiveDelivery: boolean;
  isActivePickup: boolean;
  isActiveReservation: boolean;
}
```

Successful response is:

```json
{
  "$id": "1",
  "basketId": null,
  "orderId": 20675,
  "onlinePaymentStatus": null,
  "onlinePaymentMessage": null,
  "isCreated": false,
  "success": true,
  "key": "HDBJT6XMZEAUDNNCVIFWSA",
  "message": "",
  "payUrl": "http://{host}/order/order-detail/georgia/HDBJT6XMZEAUDNNCVIFWSA",
  "successPaymentUrl": null,
  "pendingPaymentUrl": null,
  "failPaymentUrl": null,
  "step": 4
}
```

If **_succes_** is not true, you can handle error based on **_onlinePaymentStatus_**

[go to start](#ordering)

## TO DO
