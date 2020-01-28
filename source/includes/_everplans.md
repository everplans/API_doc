# Everplan

## Get a Specific Everplan's Data

```shell
curl "http://everplans.com/api/v1/everplans-responses/2"
  -H "Authorization: token <access_token>"
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "data": {}
}
```

This endpoint retrieves a specific Everplan.


### HTTP Request

`GET http://everplans.com/api/v1/everplan-responses/<EVERPLAN_ID>`

### URL Parameters

Parameter | Description
--------- | -----------
EVERPLAN_ID | The ID of the Everplan to retrieve


## Update an Everplan's Data

```shell
curl -X POST "http://everplans.com/api/v1/everplan-responses/<EVERPLAN_ID>" \
  -H "Authorization: token <access_token>" \
  -d '{
    "data": Object
  }'
```

> The above command returns JSON structured like this:

```json
{
  "responses" : [
    {
      "id": 1,
      "data": {}
    }
  ]
}
```

This endpoint updates a plan with responses.


### HTTP Request

`POST http://everplans.com/api/v1/everplan-responses/<EVERPLAN_ID>`

### URL Parameters

Parameter | Description
--------- | -----------
EVERPLAN_ID | The ID of the Everplan responses are being added to
data | A JSON object of the data to be added to the everplan