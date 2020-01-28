# Firms

## Get All Firms


```shell
curl "https://everplans.com/api/v1/firms"
  -H "Authorization: token: access_token"
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Firm one",
    "status": "active",
    "seat_id": 1
  },
  {
    "id": 2,
    "name": "Firm two",
    "status": "inactive",
    "seat_id": 2
  }
]
```

This endpoint retrieves all firms.

### HTTP Request

`GET http://everplans.com/api/v1/firms`

## Get a Specific Firm

```shell
curl "http://everplans.com/api/v1/firms/2"
  -H "Authorization: token <access_token>"
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Firm two",
  "status": "active",
  "seat_id": 2
}
```

This endpoint retrieves a specific firm.


### HTTP Request

`GET http://everplans.com/api/v1/firms/<FIRM_ID>`

### URL Parameters

Parameter | Description
--------- | -----------
FIRM_ID | The ID of the Firm to retrieve


## Create a Firm

```shell
curl "http://everplans.com/api/v1/firms"
  -X POST
  -H "Authorization: token <access_token>" \
  -d '{
    "name": "Firm two",
    "billing_address1": "2W 2nd St"
  }'
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Firm two",
  "billing_address1": "2W 2nd St",
  "status": "active",
  "seat_id": 2
}
```

This endpoint creates a firm.


### HTTP Request

`POST http://everplans.com/api/v1/firms`

### URL Parameters

Parameter | Default | Description
--------- | ------- | -----------
name | required | The name of the Firm to retrieve
billing_address1 | null | 'address for the firm'
billing_city | null | 'address for the firm'
billing_state | null | 'address for the firm'
billing_zip | null | 'address for the firm'
billing_phone | null | 'address for the firm'