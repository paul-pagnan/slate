---
title: Sail Leads API

language_tabs:
  - javascript

includes:
  - errors

search: true
---

# Introduction

Welcome to the Lumi API. You can use this API to submit, retrieve and update leads as a broker/partner.

# Authentication

To use the API you'll need an access token, which can be retrieved by authenticating with your partner credentials. You will need to use
your broker credentials in the request header via BASIC Authentication.

# Retrieving Leads

Use this endpoint to retrieve all your leads. You can provide extra parameters in the request to filter the response.

> Example request to the API using Fetch.

```javascript
const leads = await fetch('http://api.sail.com.au/v1/leads', {
    method = 'GET',
    headers: {
        'Authorization': 'lumiauthkey'
    }
});
```

> Filter/Search leads by utilising the listed parameters. The following snippet will return leads which are
under the **Waiting For Calls** status.

```javascript
const leads = await fetch('http://api.sail.com.au/v1/leads?status=WAITING_FOR_CALL', {
    method = 'GET',
    headers: {
        'Authorization': 'lumiauthkey'
    }
});
```

> The above commands return JSON structured like this:

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

### URL Parameters

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

# Lead Details
> Example using the Fetch API

```javascript
const leads = await fetch('http://api.sail.com.au/v1/leads?id=5b3c41aa9e8dec24a3117b3c', {
    method = 'GET',
    headers: {
        'Authorization': 'lumiauthkey'
    }
});
```

> The above command returns JSON structured like so:

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

Retrieves all the details for a specific lead.

### HTTP Request
`GET http://api.sail.com.au/v1/leads`

### Query Parameters

Parameter | Type | Description | Optional
--------- | ---- | ----------- | --------
id | String | The ID of the lead you are retrieving. | false

<aside class="success">
Remember to use the lead id in the request and not an id referenced to another property!
</aside>

