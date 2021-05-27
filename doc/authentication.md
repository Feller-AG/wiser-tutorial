# Authentication

## Overview

Before you can use the RESTful API you need to create an authentication token
This will enable you the access of the RESTful API.

On successfully claiming, you will receive an authentication token that you can use in your API requests.


### Example of a locked API

This example demonstrate, that the RESTful API is still locked.

**Request header :**
``` http
GET /api/loads HTTP/1.1
host: example.com
```

**Response body:**
``` json
{
  "message":"api is locked, log in to receive an authentication cookie OR unlock the device.",
  "status":"error"
}
```


## Get the authentication code

This example show how to unlock the RESTful API for an user.

As soon you start the request the physical buttons of the Wiser-uGateway will start flashing for 30 seconds.
For a valid request, one of the physical buttons has to be pressed within 30 seconds!


1) Create a new user

    **Request header:**
    ```http
    POST /api/account/claim HTTP/1.1
    Content-Type: application/json
    host: example.com
    ```
    **Request body:**
    ``` json
    {
      "user": "apiuser"
    }
    ```

    **Request body payload:**
    Property | Type | Description
    --- | --- | ---
    user | `string` | user name


2) Press any of the physical buttons of the Wiser-uGateway

    [TODO INSERT PICTURE]


3) Get the response

    **Response header:**
    ``` http
    Content-Type: application/json
    ```

    **Response body:**
    ``` json
    {
      "data": {
        "user": "apiuser",
        "secret": "60650cf4-5d26-4294-b1f2-6c06adc9d0d8"
      },
      "status": "success"
    }
    ```

    **Response body payload:**

    Property | Type | Description
    --- | --- | ---
    user | `string` | user name
    secret | `string` | authentication token


## Using the authentication code

The authentication token (also called Bearer authentication) is used in the HTTP request-header.

The client must send this token in the HTTP `Authorization` header when making requests:

``` http
Authorization: Bearer <token>
```

The following example demonstrates how to get all [loads](./loads.md) (lights & blinds) of your installation using the authentication token.

**Request header:**
``` http
GET /api/loads HTTP/1.1
Authorization: Bearer 60650cf4-5d26-4294-b1f2-6c06adc9d0d8
host: example.com
```

**Response header:**
``` http
Content-Type: application/json
```

**Response body:**
``` json
{
  "data": [
    {
      "id": 1,
      "type": "dim",
      "name": "00012680_0",
      "device": "00012680",
      "channel": 0,
      "unused": false
    },
    {
      "id": 2,
      "type": "motor",
      "name": "0000138a_0",
      "device": "0000138a",
      "channel": 0,
      "unused": false
    },
    {
      "id": 3,
      "type": "onoff",
      "name": "0000138a_1",
      "device": "0000138a",
      "channel": 1,
      "unused": false
    }
  ],
  "status": "success"
}
