# SHOPLINE SDK

## Installation

`yarn add https://github.com/shoplineapp/shopline-sdk-node.git`

## Usage

---

### Developer OAuth

#### Configuration

```js
const developerOAuth = new DeveloperOAuth({
  endpoint: process.env.DEVELOPER_OAUTH_ENDPOINT,
  clientId: process.env.DEVELOPER_OAUTH_APP_CLIENT_ID,
  clientSecret: process.env.DEVELOPER_OAUTH_APP_CLIENT_SECRET,
  redirectUri: process.env.DEVELOPER_OAUTH_APP_REDIRECT_URI,
  scope: process.env.DEVELOPER_OAUTH_APP_SCOPE,
  logger: log,
}),
```

#### API References

##### Authenticate Middleware

```js
await developerOAuth.authenticate(req, res, next)
```

`developerOAuth.authenticate` will inject `currentMerchantId`, `currentToken`, `performerId` and `performerMerchantIds` into `req.locals`

##### Callback Middleware

```javascript
await developerOAuth.callback(req, res, next)
```

> :warning: **For development environment with multiple machines**: Session redis should be separated for multiple machines, as we will attempt to get latest token for redirect uri, and it may cause problem when redirecting.

`developerOAuth.callback` will handle OAuth callbacks and inject `accessTokens` into `req.session.accessTokens`


---

### OpenAPI Client

##### Configuration

```js
const openApiClient = new OpenApiClient({
  baseURL: process.env.OPEN_API_ENDPOINT,
  accessToken: res.locals.currentToken,
  logger: log,
});
```

#### API References

- Get Merchant
  ```javascript
  await openAPIClient.getMerchant(merchantId, fields)
  ```
- Get Staff
  ```javascript
  await openAPIClient.getStaff(merchantId, fields, include_fields)
  ```
- Get Staff Permission
  ```javascript
  await openAPIClient.getStaffPermission(merchantId, fields)
  ```