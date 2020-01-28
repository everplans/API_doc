# API Key
To get an API KEY

> To generate an API key, use

```shell
curl "http://everplans.com/api/v2/api_key/<ORG_ID>"
```

> The ORG_ID is the id of the organization
> The above command will return JSON structured like this:

```json
{
  "api_key": "the generated api_key"
}
```
To get an api_key, use

### HTTP Request

`GET https://everplans.com/api/v2/api_key/<ORG_ID>`

### Query Parameters

Parameter | Description
--------- | -----------
ORG_ID | The ID of the organization.

# Authentication

> To authenticate, use this code:

```shell
# With shell, you can just pass the correct header with each request
curl "http://everplans.com/api/v1/auth" \
  -d '{
    "api_key: everplan_api_key, 
    secret: secret_key"
  }'
```

> Make sure to replace `everplan_api_key` and `secret_key` with your API keys.
> The above command returns JSON structured like this:

```json
[
  {
   "o_access_token": "your_access_token"
  }
]
```


To retrieve an access_token, use

### HTTP Request

`GET https://everplans.com/api/v1/auth`

### Query Parameters

Parameter | Description
--------- | -----------
api_key | Your api_key.
secret | your secret key.

<aside class="notice">
You must replace <code>api_key</code> and <code>secret_key</code> with your personal API keys.
</aside>
<aside class="success">
once you get an access_token back, you're authenticated
</aside>

Everplans expects for the access_token to be included in all API requests to the server in a header that looks like the following:

`Authorization: token: access_token`