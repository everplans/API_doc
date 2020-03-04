# Everplan

## Get a Specific Everplan Data

**Note**: You can only retrieve the data in the Everplan that your organization has been given access to by the owner of the Everplan

```shell
curl "http://everplans.com/api/v1/everplans-responses/2"
  -H "Authorization: Token token=<access_token>"
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "data": {
    "id": "2",
    "type": "everplan-responses",
    "links": {"self": "http://everplans.com/api/v1/everplans-responses/2"},
    "attributes": {
      "responses": [],
      "is-household": false, 
      "responses-migrated-at": "2020-02-26T18:57:15.223+00:00"}
  }
}
```

This endpoint retrieves a specific Everplan Data.

To better understand the structure of the data object parameter, check out this [link](#adding-insurance-document-and-meta-data)


### HTTP Request

`GET http://everplans.com/api/v1/everplan-responses/<EVERPLAN_ID>`

### URL Parameters

Parameter | Description
--------- | -----------
EVERPLAN_ID | The ID of the Everplan to retrieve


## Update Everplan Data

```shell
curl -X POST "http://everplans.com/api/v1/everplan-responses/<EVERPLAN_ID>" \
  -H "Authorization: Token token=<access_token>" \
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