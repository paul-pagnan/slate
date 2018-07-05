# Errors

> Example Response 400

``` json
[
    {
        "status": false,
        "error": "the error message"
    }
]
```

> Example Response 403

``` json
[
    {
        "status": false,
        "error": "Unauthorized"
    }
]
```

The Loomi API returns the following error codes:

Error Code | Meaning
---------- | -------
400 | Bad Request -- Your request is invalid.
403 | Unauthorized -- You do not have permission to perform the request.
