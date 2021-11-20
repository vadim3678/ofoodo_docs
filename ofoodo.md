# Ofoodo

- [Get Started](#get-started)
- [Ofoodo products](#ofoodo-products)
- [Server Side Rendering](#server-side-rendering)

## Get Started

### Apis required headers

token for an application (the same for android and ios app)

```
clienttoken: 'example_LRoDLYJc5wVq/Tmc5u3BdnfR/sQ7LSgG7HTI48zQgmpHYkUEjr3/bPg6YjIzYjIwYTJjODMzNDA4NQ=='
```

token for all ofoodo applications

```
salePortalId: 'HfJSPUtdc50c5zbsQo2vjNpKV9yoBwbscdyz+uDo0c9fjWx2Pe0m0CcoqKivztBrKBYfaxv84X3TNHvhaK5X3w=='
```

## Ofoodo products

### Loading catalog menu

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
Ingridients can be 'Optional' for checkbox or 'Required' for radio button 
```
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
productOptionsGroups is a list of available options. Flag for default option - *byDefault: true*
```
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
```
productOptionVariants contents intersections of the options with prices for each
```
productOptionVariants: [{$id: "10", id: "39b625b8-fb6f-736d-d5d2-11bbbabf703c",…},…]
  0: {$id: "10", id: "39b625b8-fb6f-736d-d5d2-11bbbabf703c",…}
  1: {$id: "11", id: "c50d0f7e-bc96-37e8-15cf-1a2c4f7fd90f",…}
  2: {$id: "12", id: "42df933a-d8ab-6264-0f6e-b70a63038c9e",…}
  3: {$id: "13", id: "080d81e5-d31a-1892-35ea-cd822ebbeab8",…}
```
where _optionsIds_ is a list of _productOption_ id's
```
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
```
to create order we call 
```
  https://apis.bonee.dev/httpaggregator/api/v1/Basket/paymentauto?api-version=1.0
```
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


```

## Server Side Rendering

<details>
<summary> Server Side Rendering
</summary>

> An Angular starter kit featuring [Angular 10.1.2](https://angular.io), [Angular CLI 10.1.2](https://cli.angular.io/)

> it's part of a repo series designed to create a Web Application with Angular

- [Step 1 : Example Starter](https://github.com/ganatan/angular-example-starter)
- [Step 2 : Example Routing](https://github.com/ganatan/angular-example-routing)
- [Step 3 : Example Lazy-loading](https://github.com/ganatan/angular-example-lazy-loading)
- [Step 4 : Example Bootstrap](https://github.com/ganatan/angular-example-bootstrap)
- [Step 5 : Example Modules](https://github.com/ganatan/angular-example-modules)
- [Step 6 : Example Server Side Rendering](https://github.com/ganatan/angular-example-ssr)
- [Step 7 : Example HTTP Client](https://github.com/ganatan/angular-example-httpclient)
- [Step 8 : Example Transfer State](https://github.com/ganatan/angular-example-transferstate)
- [Step 9 : Example PWA](https://github.com/ganatan/angular-example-pwa)
- [Step 10 : Example SEO](https://github.com/ganatan/angular-example-seo)

- [Step 11 : Angular 10 Application](https://github.com/ganatan/angular10-app)

## Web Application Live Demo

[https://angular.ganatan.com](https://angular.ganatan.com)

## Quick start

```bash
# clone the repo
git clone https://github.com/ganatan/angular-example-ssr.git

# change directory
cd angular-example-ssr

# install the repo with npm
npm install

# start the server
npm start

```

in your browser go to [http://localhost:4200](http://localhost:4200)

### Prerequisites

What do you need to run this app:

- Angular version 10.1.2
- Angular CLI version 10.1.2
- Jquery version 3.5.1
- Bootstrap version 4.5.2
- Fontawesome version 5.14.0

## Getting Started

### Installation

- `npm install` (installing dependencies)
- `npm outdated` (verifying dependencies)

### Development

- `npm run start`
- in your browser [http://localhost:4200](http://localhost:4200)

### Compilation

- `npm run build` ( without SSR)
- `npm run build:ssr` ( with SSR)

### Production

- `npm run serve:ssr`
- in your browser [http://localhost:4000](http://localhost:4000)

### Use Chrome version 85 min !!!!

## Tests

- `npm run lint`
- `npm run test`
- `npm run e2e`

## Chrome Installation on Linux

```bash
sudo sh -c 'echo "deb [arch=amd64] https://dl.google.com/linux/chrome/deb/ stable main" > /etc/apt/sources.list.d/google-chrome.list'

wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | sudo apt-key add -

sudo apt-get update

sudo apt-get install google-chrome-stable --yes

```

### Compilation

- `npm run build` ( without SSR)
- `npm run build:ssr` ( with SSR)

### Production

- `npm run serve:ssr`
- in your browser [http://localhost:4000](http://localhost:4000)

### Documentation

English Tutorials

- Installation - https://www.ganatan.com/tutorials/server-side-rendering-with-angular-universal
- Tutorials Step by Step - https://www.ganatan.com/tutorials/en

</details>

## TO DO
