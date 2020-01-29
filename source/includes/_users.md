# Users

## Create an individual user seat

```shell
curl "http://everplans.com/api/v1/clients"
  -X POST
  -H "Authorization: token <access_token>" \
  -d '{
    "last_name": String,
    "first_name": String,
    "email": String
  }'
```
> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "status": "Draft",
  "user_id": null,
  "advisor_id": 3,
  "firm_id": 3
}
```

This endpoint creates a single individual user.

### HTTP Request

`POST http://everplans.com/api/v1/clients`

### URL Parameters

Parameter | Description
--------- | -----------
last_name | The last name of the user
first_name | The first name of the user
email | The email address of the user


## Invite a client

```shell
curl "http://everplans.com/api/v1/clients/<SEAT_ID>/invite"
  -X POST
  -H "Authorization: token <access_token>" \
  -d '{
    "custom_invite_text": String
  }'
```
> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "status": "Draft",
  "user_id": null,
  "advisor_id": 3,
  "firm_id": 3
}
```

This endpoint invites a single individual user.

### HTTP Request

`POST http://everplans.com/api/v1/clients/<SEAT_ID>/invite`

### URL Parameters

Parameter | Description
--------- | -----------
custom_invite_text | A message you want to send as part of the invitation to the user


## Remove a client

```shell
curl "http://everplans.com/api/v1/clients/<SEAT_ID>"
  -X DELETE
  -H "Authorization: token <access_token>"
```
> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "status": "Draft",
  "user_id": null,
  "advisor_id": 3,
  "firm_id": 3
}
```

This endpoint removes a single individual user from the organization.

### HTTP Request

`DELETE http://everplans.com/api/v1/clients/<SEAT_ID>`

