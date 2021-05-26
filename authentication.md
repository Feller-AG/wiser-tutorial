# Authentication

## Overview

Before you can use the RESTful API you need to create an authentication token
This will enable you the access of the RESTful API.

On sucessfully claiming, you will receive an authenication token that you can use in your API requests.


### Example of a locked API

This example demostrate, that the RESTful API is still locked.

**Example Request:**
```
GET /api/loads
```

**Example Response:**
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

    **Example Request:**
    ``` json
    POST /api/account/claim
    Content-Type: application/json

    {
      "user": "apiuser"
    }
    ```

2) Press any of the physical buttons of the Wiser-uGateway

    [PICTURE]


3) Get the resonse

    **Example Response:**
    ``` json
    {
        "data": {
            "user": "apiuser",
            "secret": "60650cf4-5d26-4294-b1f2-6c06adc9d0d8"
        },
        "status": "success"
    }
    ```
    > The JSON attribute `secret` contains the authentication token.


## Using the authentication code

The authentication token (also called Bearer authentication) is used in the HTTP request-header.

The client must send this token in the HTTP `Authorization` header when making requests:

    Authorization: Bearer <token>

The following example demonstrates how to get all [loads](./loads.md) (lights & blinds) of your installation using the authentication token.

**Example Request:**
```
GET /api/loads
Authorization: Bearer 60650cf4-5d26-4294-b1f2-6c06adc9d0d8
```

**Example Response:**
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