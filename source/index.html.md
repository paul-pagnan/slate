---
title: API Reference

language_tabs:
  - javascript

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Lumi API. You can use this API to submit and retrieve leads as a broker/partner.

# Authentication

To use the API you'll need an access token, which can be retrieved by authenticating with your partner credentials. This auth key will be
your ticket to our endpoints.
Endpoints expect an Authorization header with each request, with the contents being your auth key.

`Authorization: lumiauthkey`

<aside class="notice">
You must replace <code>lumiauthkey</code> with your personal API key.
</aside>

# Leads

## Get All Leads

> Example request to the API using Fetch.

```javascript
const leads = await fetch('http://api.sail.com.au/v1/leads', {
    method = 'GET',
    headers: {
        'Authorization': 'lumiauthkey'
    }
});
```
> The above command returns JSON structured like this:

```json
{
    "success": true,
    "result": {
        "leads": [
            {
                "notes": [],
                "events": [],
                "id": "5b3c41aa9e8dec24a3117b3c",
                "status": "WAITING_FOR_CALL",
                "stakeholder": {
                    "first_name": "John",
                    "last_name": "Smith",
                    "email": "john.smith@smithfamily.com",
                    "phone": "0401-234-567",
                    "birth_date": "1994-02-14",
                    "address": {
                        "street": "1 George Street, Sydney NSW, Australia",
                        "country": "AUS"
                    },
                    "drivers_license_number": "123231123123",
                    "drivers_license_state": "NSW"
                },
                "company": {
                    "name": "FLYING SOLO PROPERTIES",
                    "abn": "116213748",
                    "industry": "retail",
                    "address": {
                        "street": "106-108 George Street, The Rocks NSW, Australia"
                    },
                    "average_monthly_turnover": 1234678
                },
                "loan": {
                    "reason_for_loan": [],
                    "requested_amount": 8000,
                    "installments": 52,
                    "notes": "other",
                    "amount": 0
                },
                "created_at": "2018-07-04T13:40:26+10:00",
                "updated_at": "2018-07-04T13:41:56+10:00",
                "loan_id": "5b3c41a59e8dec24a3117b23",
                "application_id": "5b3c41a5ab405559544a573e",
                "lead_application_status": "SUBMITTED"
            }
        ],
        "count": 1
    }
}
```

### HTTP Request
`GET http://api.sail.com.au/v1/leads`


### Query Parameters

Parameter | Type | Description | Optional
--------- | ---- | ----------- | --------
page_size | Int | Specify the number of leads per page you would like to retrieve. | true
page_index | Int | Specify the page you would like to retrieve. | true
status | String | Filter by the status of the lead. For valid values refer below. | true
application_status | String | Filter by the application status of the lead. For valid values refer below. | true
date_from | DateISO |Filter leads from the entered date. | true
date_to | DateISO | Filter leads to the entered date. | true

### Lead Status Values
`1. CLOSED`

`2. DECLINED`

`3. FUNDED`

`4. WAITING_FOR_CALL`

`5. MISSED_CALL`

`6. AWAITING_LOAN_DOCUMENTS`

`7. AWAITING_CREDIT_APPROVAL`

`8. PROCESSING`

`9. AWAITING_DISBURSEMENT`

### Application Status Values
`1. IN_PROCESS`

`2. SUBMITTED`

<aside class="success">
Remember to include your Authorization header!
</aside>

## Get a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.get(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve

## Delete a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.delete(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.delete(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -X DELETE
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.delete(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint deletes a specific kitten.

### HTTP Request

`DELETE http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to delete

