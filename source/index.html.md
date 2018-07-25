---
title: lumi Leads API

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
const leads = await fetch('http://api.lumi.com.au/v1/leads', {
    method = 'GET',
    headers: {
        'Authorization': 'lumiauthkey'
    }
});
```

> Filter/Search leads by utilising the listed parameters. The following snippet will return leads which are
under the **Waiting For Calls** status.

```javascript
const leads = await fetch('http://api.lumi.com.au/v1/leads?status=WAITING_FOR_CALL', {
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
                    "birth_date": Date("1994-02-14"),
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
`GET http://api.lumi.com.au/v1/leads`

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

# Create Lead

> Example request

``` json
{
    "customer": {
        "first_name": "Ben",
        "last_name": "Blah",
        "email": "ben@lumi.com.au",
        "phone": "0412312312",
        "date_of_birth": "2017-06-30",
        "address": {
            "street_number": 2,
            "street": "Sprint St",
            "street_type": "Street",
            "suburb": "Bondi Junction",
            "postcode": 2022,
            "state": "NSW",
            "country": "Australia",
        },
        "credit_score": 500,
        "defaults": "1",
        "drivers_license_number": 12312312,
        "drivers_license_state": "NSW",
    },
    "company": {
        "name": "Bens Burgers",
        "defaults": 1,
        "months_in_business": 24,
        "accounting_software": "Xero",
        "business_description": "Restaurant",
        "industry": "Customer Service",
        "average_monthly_turnover": 50000,
        "abn": 115213748,
        "address": {
            "street_number": 2,
            "street": "Sprint St",
            "street_type": "Street",
            "suburb": "Bondi Junction",
            "postal_code": 2022,
            "state": "NSW",
            "country": "Australia",
        },
        "website": "www.examplewebsite.com.au",
        "number_of_employees": 27,
    },
    "loan": {
        "notes": "Example note",
        "requested_amount": 15000,
        "installments": 52
    }
}
```

> The created lead id is returned is returned on success

```json
[
    {
        "id": "58f554ea2aaf6f0011dffabd"
    }
]
```


### HTTP Request
`POST http://api.lumi.com.au/v1/leads`

### Allowed Loan Reasons:
`1. hiring`

`2. inventory`

`3. debtConsolidation`

`4. marketing`

`5. wages`

`6. equipmentPurchasing`

`7. expansion`

`8. workingCapital`

`9. other`

### Allowed License States:
`1. ACT`

`2. NSW`

`3. NT`

`4. QLD`

`5. SA`

`6. TAS`

`7. VIC`

`8. WA`

## Query Properties
### Required Properties

> Schema

```
{
    "customer": {
        "first_name": String,
        "last_name": String,
        "email": String,
        "phone": String,
        "date_of_birth": ISODate,
        "address": {
            "street_number": Number,
            "street": String,
            "street_type": String,
            "suburb": String,
            "postcode": Number,
            "state": String,
            "country": String,
        },
        "credit_score": Number,
        "defaults": Number,
        "drivers_license_number": Number,
        "drivers_license_state": String,
    },
    "company": {
        "name": String,
        "defaults": String,
        "months_in_business": Number,
        "accounting_software": String,
        "business_description": String,
        "industry": String,
        "average_monthly_turnover": Number,
        "abn": Number,
        "address": {
            "street_number": Number,
            "street": String,
            "street_type": String,
            "suburb": String,
            "postal_code": Number,
            "state": String,
            "country": String,
        },
        "website": String,
        "number_of_employees": Number,
    },
    "loan": {
        "notes": String,
        "requested_amount": Number,
        "installments" : Number,
    }
}
```

Parameter | Type
--------- | ----
customer.first_name | String
customer.email | String
customer.phone | Number
company.name | String
company.abn | Number
loan.requested_amount | Number
loan.installments | Number


### Skip Mandatories
`customer.phone`

`company.name`

`company.abn`

`loan.requested_amount`

`loan.installments`


<aside class="notice">
    These properties can be skipped if enforce_mandatories=false
</aside>

# Upload lead document
### Request
> Headers

```json
    "Constent Type: multipart/form-data;boundary=----WebKitFormBoundary8M3sSU13ul5lXSJm"
    "Authentication: Basic authentication with base64(user:pass) in the header [BASIC AUTHENTICATION]"
```

> Body

```
    ------WebKitFormBoundary8M3sSU13ul5lXSJm
    Content-Disposition: form-data; name="document"; filename="image.jpg"
    Content-Type: image/jpeg
    Content-Transfer-Encoding: base64
    /9j/4AAQSkZJRgABAQEAYABgAAD/2wBDAAgGBgcGBQgHBwcJCQgKDBQNDAsLDBkSEw8UHRofHh0a
    HBwgJC4nICIsIxwcKDcpLDAxNDQ0Hyc5PTgyPC4zNDL/2wBDAQkJCQwLDBgNDRgyIRwhMjIyMjIy
    MjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjL/wAARCAABAAEDASIA
    AhEBAxEB/8QAFQABAQAAAAAAAAAAAAAAAAAAAAf/xAAUEAEAAAAAAAAAAAAAAAAAAAAA/8QAFAEB
    AAAAAAAAAAAAAAAAAAAAAP/EABQRAQAAAAAAAAAAAAAAAAAAAAD/2gAMAwEAAhEDEQA/AL+AD//Z
    ------WebKitFormBoundary8M3sSU13ul5lXSJm--
```

`POST http://api.lumi.com.au/lead/{lead_id}/documents`

> The following response is returned

```json
{
    "success": true,
    "file": {
        "id": "59945662f5b3f9b41076cc07",
        "filename": "image.jpg",
        "size": 250,
    }
}
```

## Parameters
Parameter | Type 
--------- | ---- 
lead_id | String

# Lead Details
> Example using the Fetch API

```javascript
const leads = await fetch('http://api.lumi.com.au/v1/leads?id=5b3c41aa9e8dec24a3117b3c', {
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
                    "birth_date": Date("1994-02-14"),
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
`GET http://api.lumi.com.au/v1/leads`

### Query Parameters

Parameter | Type | Description | Optional
--------- | ---- | ----------- | --------
id | String | The ID of the lead you are retrieving. | false

<aside class="success">
Remember to use the lead id in the request and not an id referenced to another property!
</aside>
