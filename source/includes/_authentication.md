# API Key
To get an API KEY

> To generate an secret, use

```shell
curl "http://everplans.com/api/v2/oauth/secret/<ORG_ID>"
```

> The ORG_ID is the id of the organization
> The above command will return JSON structured like this:

```json
{
  "secret": "the generated secret"
}
```
To get a secret, use

### HTTP Request

`GET https://everplans.com/api/v2/secret/<ORG_ID>`

### Query Parameters

Parameter | Description
--------- | -----------
ORG_ID | The ID of the organization.

# Authentication

> To authenticate, use this code:

```shell
# With shell, you can just pass the correct header with each request
curl "http://everplans.com/api/v2/oauth/access_token" \
  -d '{
    "ORG_ID: organization id, 
    secret: secret key"
  }'
```

> Make sure to replace `ORG_ID` and `secret` with your API keys.
> The above command returns JSON structured like this:

```json
[
  {
   "access_token": "your_access_token"
  }
]
```


To retrieve an access_token, use

### HTTP Request

`GET https://everplans.com/api/v2/oauth/access_token`

### Query Parameters

Parameter | Description
--------- | -----------
ORG_ID | Your organization id.
secret | your secret key.

<aside class="notice">
You must replace <code>api_key</code> and <code>secret_key</code> with your personal API keys.
</aside>
<aside class="success">
once you get an auth_token back, you're authenticated
</aside>

Everplans expects for the access_token to be included in all API requests to the server in a header that looks like the following:

`Authorization: token: access_token`