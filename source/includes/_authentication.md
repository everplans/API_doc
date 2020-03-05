# Authentication
To successfully authenticate, you need
- an API Secret Key and client ID
- a user `refresh_token`
- an `access_token`

All calls to our endpoint unless specified require an `access_token`

## API Secret
To get an API Secret and a client ID, please reach out to the **Everplans Customer Success** team


## Refresh token
You need the API secret key and the client ID to retrieve a `refresh_token` which you'll use to get an access_token.
The `refresh_token` never expires

> To retrieve a `refresh_token`, use this code:

```shell
# With shell, you can just pass the correct header with each request
curl "http://everplans.com/api/v2/oauth2/refresh_token" \
  -d '{
    "client_id": client ID, 
    client_secret: secret key"
  }'
```

> Make sure to replace `client_id` and `secret` with your API keys.
> The above command returns JSON structured like this:

```json
[
  {
   "refresh_token": "your_refresh_token"
  }
]
```


To retrieve a `refresh_token`, use

### HTTP Request

`GET https://everplans.com/api/v2/oauth2/refresh_token`

### Query Parameters

Parameter | Description
--------- | -----------
client_id | your client id.
client_secret | your API secret key.

<aside class="notice">
You must replace <code>client_id</code> and <code>secret</code> with your personal API keys.
</aside>
<aside class="notice">
The <code>refresh_token</code> never expires but we invalidate it when another <code>refresh_token</code> is generated
</aside>
<aside class="success">
once you get a <code>refresh_token</code> back, you can then use it to retrieve your <code>access_token</code>
</aside>


> To retrieve the `access_token`, use:

```shell
# With shell, you can just pass the correct header with each request
curl "http://everplans.com/api/v2/oauth2/access_token" \
  -d '{
    "refresh_token: refresh token"
  }'
```

> Make sure to replace `refresh_token` with the `refresh_token` you got in the previous step.
> The above command returns JSON structured like this:

```json
[
  {
   "access_token": "your_access_token"
  }
]
```


To retrieve an `access_token`, use

### HTTP Request

`GET https://everplans.com/api/v2/oauth2/access_token`

### Query Parameters

Parameter | Description
--------- | -----------
refresh_token | Your refresh token.

<aside class="notice">
You must replace <code>refresh_token</code> with the token you got in the previous step.
</aside>
<aside class="notice">
The <code>access_token</code> expires 10 mins after last use
</aside>
<aside class="success">
once you get an <code>access_token</code> back, you're authenticated
</aside>

Everplans expects for the `access_token` to be included in all API requests to the server in an Authorization header that looks like the following:

`Authorization: Token token=access_token`