# Payment

## Adding a card

First we call

```
/payment/api/v1.0/saleportal/users/processCardSave/tbcbank
```

with specific headers:

```ts
teamreferer: ofoodo;
failurl: http://localhost:4200/pr/profile/payment
successurl: http://localhost:4200/pr/profile/payment
```
if payment system exists we using ***url*** from response model to go to bank page

![Adding a card](images/payment_1.jpg)


if succes we redirecting back to **_http://{host}/pr/profile/payment_**

if failed now backend returns call with status code 400 and error message

```
https://apis.bonee.net/payment/api/v1.0/partners/order/payment/tbcbank/fail
```
