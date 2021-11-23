# Authorization

## Social Authorization

On frontend we using social auth plugin which returns user model if success:

```ts
class SocialUser {
  id: string;
  provider: string;
  email: string;
  name: string;
  photoUrl: string;
  firstName: string;
  lastName: string;
  authToken: string;
  idToken: string;
  authorizationCode: string;
  response: any;
}
```

To bonee api we send **_authToken_** and **_provider_**

```
/ExternalProviderLogin?Token={authToken}&Provider={provider}&TeamReferer=ofoodo.com
```

Response contains auth info

```json
{
  "access_token": "{access_token}",
  "expires_in": 11111111,
  "refresh_token": "{refresh_token}",
  "scope": "offline_access openid profile client locations catalog translation basket webboneeagg orders orders.signalrhub feedback subscriptions payment userprovider",
  "token_type": "Bearer"
}
```
