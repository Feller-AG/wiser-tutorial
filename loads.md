# Manage your loads via the RESTful API

## Overview

The loads services provides access to all loads (lights & blinds) of your installation.

 > Do not forget to include an authentication token in all your requests! Read more about [here](./authentication.md).

## GET /api/loads

This example demonstrates how to get all loads (lights & blinds) of your installation.

**Request header:**
``` http
GET /api/loads HTTP/1.1
Authorization: Bearer 60650cf4-5d26-4294-b1f2-6c06adc9d0d8
host: example.com
```

**Response header:**
``` http
HTTP/1.1 200 OK
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
```


## GET /api/loads/state

**Request header:**
``` http
GET /api/loads/state HTTP/1.1
Authorization: Bearer 60650cf4-5d26-4294-b1f2-6c06adc9d0d8
host: example.com
```

**Response header:**
``` http
HTTP/1.1 200 OK
Content-Type: application/json
```

**Response body:**
``` json
{
  "data": [
    {
      "id": 1,
      "state": {
        "level": 8160,
        "tilt": 0,
        "moving": "stop",
        "flags": {
          "direction": 0,
          "learning": 0,
          "moving": 0,
          "under_current": 0,
          "over_current": 0,
          "timeout": 0,
          "locked": 0
        }
      }
    },
    {
      "id": 2,
      "state": {
        "bri": 0,
        "flags": {
          "over_current": 0,
          "fading": 0,
          "noise": 0,
          "direction": 0,
          "over_temperature": 0
        }
      }
    },
    {
      "id": 3,
      "state": {
        "bri": 10000
      }
    }
  ],
  "status": "success"
}
```

## PUT /api/loads/< id >/target_state

Let's set the load state connected on a `onoff` output.

**Request header:**
``` http
PUT api/loads/3/target_state HTTP/1.1
Authorization: Bearer 60650cf4-5d26-4294-b1f2-6c06adc9d0d8
host: example.com
```

**Request body:**
``` json
{
  "bri": 0
}
```

**Response header:**
``` http
HTTP/1.1 200 OK
Content-Type: application/json
```

**Response body:**
``` json
{
  "data": {
    "id": 3,
    "target_state": {
      "bri": 0
    }
  },
  "status": "success"
}
```

Let's set the load state connected on a `dim` output.

**Request header:**
``` http
PUT api/loads/1/target_state HTTP/1.1
Authorization: Bearer 60650cf4-5d26-4294-b1f2-6c06adc9d0d8
host: example.com
```

**Request body:**
``` json
{
  "bri": 500
}
```

**Response header:**
``` http
HTTP/1.1 200 OK
Content-Type: application/json
```

**Response body:**
``` json
{
  "data": {
    "id": 1,
    "target_state": {
      "bri": 500
    }
  },
  "status": "success"
}
```

Let's set the load state connected on a `motor` output.

**Request header:**
``` http
PUT api/loads/2/target_state HTTP/1.1
Authorization: Bearer 60650cf4-5d26-4294-b1f2-6c06adc9d0d8
host: example.com
```
``` json
{
  "level": 200,
  "tilt": 2
}
```

**Response header:**
``` http
HTTP/1.1 200 OK
Content-Type: application/json
```

**Response body:**
``` json
{
  "data": {
    "id": 2,
    "target_state": {
      "level": 200,
      "tilt": 2
    }
  },
  "status": "success"
}
```


## PUT /api/loads/< id >/ctrl

**Request header:**
``` http
GET /api/loads/6/ctrl HTTP/1.1
Authorization: Bearer 60650cf4-5d26-4294-b1f2-6c06adc9d0d8
host: example.com
```

**Response header:**
``` http
HTTP/1.1 200 OK
Content-Type: application/json
```

**Response body:**
``` json

```
