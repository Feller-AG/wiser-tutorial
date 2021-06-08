# Access the Wiser-by-Feller RESTFul API using curl

## Overview

This page shows you some examples how to use the Wiser-by-Feller RESTFul API with `curl`.

Change the IP-Address according your Gateway IP-Address.

**Set IP-Address:**

``` bash
export GATEWAY_IP_ADDRESS="192.168.1.123"
```

## Get the authentication code

See [authentication](./authentication.md) for more information.

**Request:**

``` bash
curl -X 'POST' \
  "http://${GATEWAY_IP_ADDRESS}/api/account/claim" \
  -H 'Content-Type: application/json' \
  -d '{"user": "apiuser"}'
```

**Response:**

``` json
{
  "data": {
    "user": "apiuser",
    "secret": "60650cf4-5d26-4294-b1f2-6c06adc9d0d8"
  },
  "status": "success"
}
```

**Set authentication code:**

``` bash
export GATEWAY_TOKEN="60650cf4-5d26-4294-b1f2-6c06adc9d0d8"
```

## Get all loads

See [loads](./api_loads.md) for more information.

**Request:**

``` bash
curl -X 'GET' \
  "http://${GATEWAY_IP_ADDRESS}/api/loads" \
  -H "Authorization: Bearer ${GATEWAY_TOKEN}"
```

**Response:**

``` json
{
  "data": [
    {
      "id": 1,
      "type": "onoff",
      "name": "0000133a_0",
      "device": "0000133a",
      "channel": 0,
      "unused": false
    },
    {
      "id": 2,
      "type": "dim",
      "name": "0000144b_0",
      "device": "0000144b",
      "channel": 0,
      "unused": false
    },
    {
      "id": 3,
      "type": "motor",
      "name": "0000155c_0",
      "device": "0000155c",
      "channel": 0,
      "unused": false
    }
  ],
  "status": "success"
}
```

## Modify the state of a load

See [loads](./api_loads.md) for more information.

**Request:**

``` bash
curl -X 'PUT' \
  "http://${GATEWAY_IP_ADDRESS}/api/loads/1/target_state" \
  -H "Authorization: Bearer ${GATEWAY_TOKEN}" \
  -d '{"bri": 0}'
```

**Response:**

``` json
{
  "data": {
    "id": 1,
    "target_state": {
      "bri": 0
    }
  },
  "status": "success"
}
