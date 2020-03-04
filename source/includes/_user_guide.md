# Everplans User Guide
### Context and Assumptions
 The following document is written for a developer who has already signed up for an API secret and client id.
If you haven't done that already, please reach out to our Customer Success Team

This walk-through will take you through authenticating with the API, and posting data to a user's everplan. It will go through 3 endpoints.

1. Authenticating - in this step you'll use existing credentials to get an access token.
2. Upload PDF - in this step you'll upload a PDF document using the uploads endpoint.
3. Create metadata and attach the PDF - in this step you'll use the upload ID created in the previous step to attach it to a record in the everplan so that the user can see the document and associated metadata when they log in to their everplan.



## Authenticating
We assume you've gotten an access token by following the steps [here](#authentication).

Sessions are only valid for 10 minutes after last use.

(_NOTE: Be sure to use the headers and URL patterns as specified in each step._)
 

## Adding Insurance Document and Meta Data
Once you've logged in, and gotten a valid `session_token` and `everplan_id`, you can use the following 2 API endpoints to upload files and metadata respectively.

### Headers

For all subsequent API requests you'll need to set the following two headers.
* `Content-Type: application/vnd.api+json`
* `'Authorization: Token token=access_token' ` (be sure to supply the exact access_token you received from the Authentication request)

```shell
For convenience, here is a cURL command:
curl -X POST \
  https://my.everplans.com/api/v2/uploads \
  -H 'Authorization: Token token=[access_token]' \
  -H 'content-type: multipart/form-data; application/vnd.api+json;' \
  -F file=@PATH_TO_LOCAL_FILE
```
> The response will look something like this, be sure to hold on to the `id` of the upload to use below.

```json
{
  "upload": {
    "id": "f1535090-d17d-46e2-beb8-0f2fd51a069d",
    "everplan_id": 25817,
    "response_id": null,
    "encrypted_file": {
      "url": "https://path-to-file"
    },
    "original_file_key": "policy.pdf",
    "filename": "policy.pdf",
    "filetype": "pdf",
    "status": "uploaded",
    "filesize": 30059,
    "created_at": "2019-02-25T15:04:36.730Z",
    "updated_at": "2019-02-25T15:04:36.730Z"
  }
}
```

### Uploading the PDF
Post the following URL with the following headers. Be sure to include the PDF as a binary attachment in the post payload.

* URL: POST  https://my.everplans.com/api/v2/uploads
* Additional header: `Content-Type: multipart/form-data`


### Attaching the PDF and adding meta data
The everplan is comprised of structured fields in a rich hierarchy. Each `field` of data is called an `element`, and each element has a unique id. In the sample template we've included a `name` field, but this is only for convenience. It's ignored by the server, and can optionally be left out.

Each field needs an `element_id`, `value`, and `group_id`. The `group_id` is used to make sure all fields are grouped into the same record. (For example, that the carrier, death benefit, and PDF document all belong to the same 'policy' record). The `group_id` must be an array of 2 unique UUIDs. For the sake of this walk-through, it's not important to fully understand how grouping works, you can feel free to include the literal values supplied in the sample template below.

```shell
{
  "data": {
    "type": "everplan-responses",
    "id": "[everplan_id]",
    "attributes": {
      "responses": [
        {
          "group-id": [
            "312c90a6-bb1c-4441-9722-3969b3f0dc23",
            "e6dcb151-d320-4f71-a84d-383687cf0557"
          ],
          "name": "Upload a scan, photo, or PDF of Life Insurance policy (even just the cover sheet is helpful)",
          "element-id": "08c924e2-0b97-407c-a787-326f9c889c92",
          "value": [
            {
              "name": "policy.pdf",
              "filetype": "application/pdf",
              "id": "[id from file upload]"
            }
          ]
        },
        {
          "group-id": [
            "312c90a6-bb1c-4441-9722-3969b3f0dc23",
            "e6dcb151-d320-4f71-a84d-383687cf0557"
          ],
          "name": "Whats the policy number?",
          "element-id": "3c2124b2-3df4-4772-957c-0d33b0f6e712",
          "value": "USA--xx--24601"
        },
        {
          "group-id": [
            "312c90a6-bb1c-4441-9722-3969b3f0dc23",
            "e6dcb151-d320-4f71-a84d-383687cf0557"
          ],
          "name": "Value of death benefit",
          "element-id": "11f3c09f-0abf-4b5d-867c-c0ff82dd0775",
          "value": "$100,000"
        },
        {
          "group-id": [
            "312c90a6-bb1c-4441-9722-3969b3f0dc23",
            "e6dcb151-d320-4f71-a84d-383687cf0557"
          ],
          "name": "Name of insurance company",
          "element-id": "f7d54148-1d9c-4556-b8fc-4c1deadeda71",
          "value": "M Financial"
        },
        {
          "group-id": [
            "312c90a6-bb1c-4441-9722-3969b3f0dc23",
            "e6dcb151-d320-4f71-a84d-383687cf0557"
          ],
          "name": "Policy start date",
          "element-id": "fc1538d6-2d21-4116-b21b-968a6ccd7ea6",
          "value": {
            "mask": 7,
            "date": "2019-02-01"
          }
        },
        {
          "group-id": [
            "312c90a6-bb1c-4441-9722-3969b3f0dc23",
            "e6dcb151-d320-4f71-a84d-383687cf0557"
          ],
          "name": "Policy expiration date",
          "element-id": "668fb215-2b74-4227-99b8-bb74f2166394",
          "value": {
            "mask": 7,
            "date": "2029-02-01"
          }
        },
        {
          "group-id": [
            "312c90a6-bb1c-4441-9722-3969b3f0dc23",
            "e6dcb151-d320-4f71-a84d-383687cf0557"
          ],
          "name": "Notes & Instructions",
          "element-id": "67575167-af8c-4cc0-bf5b-23baf793d8a3",
          "value": "Some notes or extra info on the policy"
        },
        {
          "group-id": [
            "312c90a6-bb1c-4441-9722-3969b3f0dc23",
            "e6dcb151-d320-4f71-a84d-383687cf0557"
          ],
          "name": "Type of policy",
          "element-id": "eeca04b1-bfb5-4ada-896f-a9ab0034adad",
          "value": "Term"
        }
      ]
    }
  }
}
```


Post the following URL with the following headers. Be sure to include the JSON template as the body.


* URL: POST https://my.everplans.com/api/v2/everplan-responses/[everplan_id]
* Request body:
Be sure to supply the correct eveplan ID and the correct ID for the uploaded file (from the previous API request).




``` shell
For convenience, here is a cURL command:
curl -X PATCH \
  https://my.everplans.com/api/v2/everplan-responses/[everplan_id] \
  -H 'Authorization: Token token=BJ1qQiwpgJm07xAM1cOvw4Q7KgewIR9x8ePb5_NmDOY' \
  -H 'Content-Type: application/vnd.api+json; application/json' \
  -H 'cache-control: no-cache' \
  -d '{
  "data": {
    "type": "everplan-responses",
    "id": "[everplan_id]",
    "attributes": {
      "responses": [
        {
          "group-id": [
            "312c90a6-bb1c-4441-9722-3969b3f0dc23",
            "e6dcb151-d320-4f71-a84d-383687cf0557"
          ],
          "name": "Upload a scan, photo, or PDF of Life Insurance policy (even just the cover sheet is helpful)",
          "element-id": "08c924e2-0b97-407c-a787-326f9c889c92",
          "value": [
            {
              "name": "policy.pdf",
              "filetype": "application/pdf",
              "id": "309c8870-31c0-46a5-aa88-d6a59d28a759"
            }
          ]
        },
        {
          "group-id": [
            "312c90a6-bb1c-4441-9722-3969b3f0dc23",
            "e6dcb151-d320-4f71-a84d-383687cf0557"
          ],
          "name": "Whats the policy number?",
          "element-id": "3c2124b2-3df4-4772-957c-0d33b0f6e712",
          "value": "USA--xx--24601"
        },
        {
          "group-id": [
            "312c90a6-bb1c-4441-9722-3969b3f0dc23",
            "e6dcb151-d320-4f71-a84d-383687cf0557"
          ],
          "name": "Value of death benefit",
          "element-id": "11f3c09f-0abf-4b5d-867c-c0ff82dd0775",
          "value": "$100,000"
        },
        {
          "group-id": [
            "312c90a6-bb1c-4441-9722-3969b3f0dc23",
            "e6dcb151-d320-4f71-a84d-383687cf0557"
          ],
          "name": "Name of insurance company",
          "element-id": "f7d54148-1d9c-4556-b8fc-4c1deadeda71",
          "value": "M Financial"
        },
        {
          "group-id": [
            "312c90a6-bb1c-4441-9722-3969b3f0dc23",
            "e6dcb151-d320-4f71-a84d-383687cf0557"
          ],
          "name": "Policy start date",
          "element-id": "fc1538d6-2d21-4116-b21b-968a6ccd7ea6",
          "value": {
            "mask": 7,
            "date": "2019-02-01"
          }
        },
        {
          "group-id": [
            "312c90a6-bb1c-4441-9722-3969b3f0dc23",
            "e6dcb151-d320-4f71-a84d-383687cf0557"
          ],
          "name": "Policy expiration date",
          "element-id": "668fb215-2b74-4227-99b8-bb74f2166394",
          "value": {
            "mask": 7,
            "date": "2029-02-01"
          }
        },
        {
          "group-id": [
            "312c90a6-bb1c-4441-9722-3969b3f0dc23",
            "e6dcb151-d320-4f71-a84d-383687cf0557"
          ],
          "name": "Notes & Instructions",
          "element-id": "67575167-af8c-4cc0-bf5b-23baf793d8a3",
          "value": "Some notes or extra info on the policy"
        },
        {
          "group-id": [
            "312c90a6-bb1c-4441-9722-3969b3f0dc23",
            "e6dcb151-d320-4f71-a84d-383687cf0557"
          ],
          "name": "Type of policy",
          "element-id": "eeca04b1-bfb5-4ada-896f-a9ab0034adad",
          "value": "Term"
        }
      ]
    }
  }
}'
```