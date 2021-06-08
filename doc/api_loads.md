# Manage your loads via the RESTful API

## Overview

The loads services provides access to all loads (e.g. lights, blinds) of your installation.

**Do not forget to include the [authentication token](./authentication.md) in all your requests!**

To modify the state of a load, there are two possibilities:

- Using the API `target_state`
  - Use `target_state` to set the desired end-state of a load using a value e.g. `bri` (brightness)
- Using the API `ctrl`
  - Use `ctrl` to invoke (simulate) a button-event, e.g. `click`, `press`, `release`

> 🐮 Help! I need somebody [Help](./faq_loads.md) !

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

## GET /api/loads/state

Get all loads (lights & blinds) state of your installation.

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
        "bri": 10000
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
    }
  ],
  "status": "success"
}
```

## PUT /api/loads/< id >/target_state

Possible `target_state` values per load-type:

Type | Attribute(s)
--- | ---
onoff | `bri`
dim | `bri`
motor | `level`,  `tilt`

### Example `onoff` type (using target_state)

Let's set the load state of an `onoff` type.

To turn **on** or **off** a load set the attribute `bri` (brightness) to the following values:

- Turn **off** set the `bri` attribute to `0`
- Turn **on** set  the `bri` attribute to `10000`

**Request header:**

``` http
PUT /api/loads/1/target_state HTTP/1.1
Authorization: Bearer 60650cf4-5d26-4294-b1f2-6c06adc9d0d8
Content-Type: application/json
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
    "id": 1,
    "target_state": {
      "bri": 0
    }
  },
  "status": "success"
}
```

### Example `dim` type (using target_state)

Let's set the load state of a `dim` type.

On a dimmable light you can set the target brightness between 0% and 100% (0 - 10000).

- Turn `off` set the `bri` attribute to `0`
- To dim  set the `bri` attribute between 1 and 10000 (e.g. set `bri` to 5000, means 50% of brightness)

**Request header:**

``` http
PUT /api/loads/2/target_state HTTP/1.1
Authorization: Bearer 60650cf4-5d26-4294-b1f2-6c06adc9d0d8
Content-Type: application/json
host: example.com
```

**Request body:**

``` json
{
  "bri": 5000
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
      "bri": 5000
    }
  },
  "status": "success"
}
```

### Example `motor` type (using target_state)

Let's set the load state of a `motor` type.

On a motor e.g. shutter/blind you can set the target level between 0% and 100% (0 - 10000) and a tilt value.

#### Shutter position (target level)

- To set the shutter in open position set the `level` attribute to `0`
- To set the shutter in close position set the `level` attribute to `10000`
- To control the shutter set the `level` attribute between 1 and 10000 (e.g. set `level` to 5000, means set the shutter/blind to position 50%)

#### Slats of a shutter (number of tilt)

- Tilt in number of `tilt` commands. Finally it's the motor running time, because we don't know the slat position in degrees

**Request header:**

``` http
PUT /api/loads/3/target_state HTTP/1.1
Authorization: Bearer 60650cf4-5d26-4294-b1f2-6c06adc9d0d8
Content-Type: application/json
host: example.com
```

**Request body:**

``` json
{
  "level": 5000,
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
    "id": 3,
    "target_state": {
      "level": 5000,
      "tilt": 2
    }
  },
  "status": "success"
}
```

## PUT /api/loads/< id >/ctrl

Possible button events:

Event | Description
--- | ---
click | if the button was pressed shorter than 500ms
press | if the button was pressed 500ms or longer
release | must follow after a pressed event

Possible button types:

``` INI
button "on" for buttons like:
+-----+
|  I  |
+-----+

button "off" for buttons like:
+-----+
|  0  |
+-----+

button "up" for buttons like:
+-----+  +-----+
|  +  |  |  ^  |
+-----+  +-----+

button "down" for buttons like:
+-----+  +-----+
|  -  |  |  v  |
+-----+  +-----+

button "toggle" for buttons like:
+-----+
| I/0 |
+-----+
```

### Example `onoff` type (using ctrl)

Let's control the load of an `onoff` type.

To turn **on** or **off** using `button` and `event` attributes:

- Turn **on** set the `button` attribute to `on` and `event` attribute to `click`
- Turn **off** set the `button` attribute to `off` and `event` attribute to `click`

**Request header:**

``` http
PUT /api/loads/1/ctrl HTTP/1.1
Authorization: Bearer 60650cf4-5d26-4294-b1f2-6c06adc9d0d8
Content-Type: application/json
host: example.com
```

**Request body:**

``` json
{
  "button": "on",
  "event": "click"
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
  "status": "success",
  "data": {
      "id": 1,
      "ctrl": {
          "button": "on",
          "event": "click"
      }
  }
}
```
