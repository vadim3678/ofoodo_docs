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
### Getting token endpoint. The request must contain above headers and ***teamreferer: ofoodo*** 
```
https://accounts.bonee.dev/.well-known/openid-configuration
```
endpoint will be in the ***token_endpoint*** field of the response model 


### Authorized request must include
```
authorization: Bearer {auth_token}
```