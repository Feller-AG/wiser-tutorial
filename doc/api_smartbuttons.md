# Configure smartbuttons via the RESTful API

## Overview

As the name already says, some buttons in your **Wiser-by-Feller** environment are smart.
But don't worry, they are not smart at all, you still have to press the (smart-)button yourself.

A smartbutton can de married with a [job](./api_jobs.md).
That means, by pressing the smartbutton a configured [job](./api_jobs.md) will be executed.

**Do not forget to include the [authentication token](./authentication.md) in all your requests!**

> 🐮 I have not get married yet, probably a smart decision?

## Types of smartbuttons

They are two kind of smartbuttons:

- Smartbuttons from type: `scene`
  - Example button-frontset (2x scene)

    ![Scene-Button-2](./images/wiser_button_symbol_scene_2.png)

- Smartbuttons from type: `groupctrl`
  - Example button-frontset (1x plus/minus)

    ![Group-Control-Button-Plus-Minus](./images/wiser_button_symbol_groupcontrol_up_down.png)

## Configure smartbuttons

The configuration of a smartbutton consists of the following steps:

1) Activated the programming mode (*program*)
    - Choose between `scene` or `groupctrl` smartbuttons
    - Configure the blink-time. The default is 60 seconds
    - At this point the smartbuttons do not blinking yet

2) Run the notify (*notify*)
    - Now the available smartbuttons will start blinking
      - `scene`-smartbuttons (will blinking `purple`)
      - `groupctrl`-smartbuttons (will blinking `yellow`)
    - As soon as one of the blinking smartbutton is pressed, all smartbuttons stop blinking and the notify request comes back with a response

3) The Marriage
    - At this point you can configure a [job](./api_jobs.md). Now the marriage of the smartbutton within a [job](./api_jobs.md) can take place.

## Activated the programming mode

### POST /api/smartbuttons/program

Activated the smartbutton programming-mode.

Possible attributes:

Key  | Description
--- | ---
on | `true` to prepare programming mode or `false` to abort it (default: `false`)
timeout | time in seconds to stay in programming mode (default: `60`)
button_type | type of buttons to program. `scene` or `groupctrl` (default: `scene`)

#### Example to activate the programming-mode with a scene-smartbutton

**Request header:**

``` http
POST /api/smartbuttons/program HTTP/1.1
Content-Type: application/json
host: example.com
```

**Request body:**

``` json
{
  "on": true,
  "timeout": 60,
  "button_type": "scene"
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
    "on": true,
    "button_type": "scene",
    "timeout": 60,
    "owner": "user"
  },
  "status": "success"
}
```

## Run the notify

### GET /api/smartbuttons/notify

Start blinking the smartbuttons and wait until one is pressed.
This is a long lasting REST-API call. It blocks and wait until a smartbutton is pressed or the timeout is reached.

#### Example to notify the pressed smartbutton

**Request header:**

``` http
GET /api/smartbuttons/notify HTTP/1.1
host: example.com
```

Wait until until a smartbutton is pressed.

**Response body:**

``` json
{
  "data": {
    "button": 50
  },
  "status": "success"
}
```

## The marriage

Finally we will get married!

### PATCH /api/smartbuttons/ < id >

#### Example to marriage/link the smartbutton with a job

The request-body contains the unique [job](./api_jobs.md)-id.

**Request header:**

``` http
PATCH /api/smartbuttons/50 HTTP/1.1
Content-Type: application/json
host: example.com
```

**Request body:**

``` json
{
  "job": 20
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
    "id": 50,
    "input_channel": 0,
    "device_addr": 48879,
    "device": "000BEEF",
    "input_type": 2,
    "job": 20,
  },
  "status": "success"
}
```

Just married, press the smartbutton and the job is executed.

> 🐮 This will be an everlasting love ❤️