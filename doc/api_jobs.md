# Configure jobs via the RESTful API

## Overview

Using a job allows you to control a group of loads.
The loads can be configured using the attribute `target_states` and/or `button_ctrl`.

Its also possible to change system-flags `flag_values` or even to run user-scripts [`scripts`](./api_scripts.md).

You can create a job with multiple-sections. That means, that it can contain `target_states` and `button_ctrl`.
See below in the examples how to run the sections separately or even all sections (whole job).

Jobs are triggered in different/multiple ways:

- internally from a timer

- in combination with a [smartbutton](./api_smartbuttons.md)

- and probably the most important, over the REST-API

**Do not forget to include the [authentication token](./authentication.md) in all your requests!**

> 🐮 My `job` is to eat a lot of fresh grass and my `target_state` is to getting full!

## Configure jobs

### POST /api/jobs

Lets configure a job that turn **on** some loads (e.g. lights) of your installation.

#### Example to configure a job using attribute target_states

The attribute `target_states` maps with the Loads-[target_state](./api_loads.md#api-loads-target-state) attributes.

**Request header:**

``` http
POST /api/jobs HTTP/1.1
Content-Type: application/json
host: example.com
```

**Request body:**

``` json
{
  "target_states": [
    {
      "load": 1,
      "bri": 10000
    },
    {
      "load": 2,
      "bri": 10000
    }
  ]
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
    "id": 20,
    "target_states": [
        {
            "load": 1,
            "bri": 10000
        },
        {
            "load": 2,
            "bri": 10000
        }
    ]
  },
  "status": "success"
}
```

#### Example to configure a job using attribute button_ctrl

The attribute `button_ctrl` maps with the Loads-[ctrl](./api_loads.md#api-loads-ctrl) attributes.

**Request header:**

``` http
POST /api/jobs HTTP/1.1
Content-Type: application/json
host: example.com
```

**Request body:**

``` json
{
  "button_ctrl": {
    "event": "click",
    "button": "on",
    "loads": [1, 2]
  }
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
    "id": 30,
    "button_ctrl": {
        "ctrl_input_channel": 16,
        "event": "click",
        "button": "on",
        "loads": [1, 2]
    }
  },
  "status": "success"
}
```

## Run jobs

Now lets run the jobs.

Be in mind that the response of the job, doesn't means that the loads (e.g. lights) reached the final target-states. It's just a *job* that has been executed.

### GET /api/jobs/ < id > /run

This will run the `target_states`-section of your job.

**Request header:**

``` http
GET /api/jobs/20/run HTTP/1.1
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
  "data": {
    "id": 20,
    "target_states": [
        {
            "load": 1,
            "bri": 10000
        },
        {
            "load": 2,
            "bri": 10000
        }
    ]
  },
  "status": "success"
}
```

### GET /api/jobs/ < id > /ctrl

This will run the `button_ctrl`-section of your job.

**Request header:**

``` http
GET /api/jobs/30/run HTTP/1.1
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
  "data": {
    "id": 30,
    "button_ctrl": {
        "ctrl_input_channel": 16,
        "event": "click",
        "button": "on",
        "loads": [1, 2]
    }
  },
  "status": "success"
}
```

### GET /api/jobs/ < id > /trigger

This will trigger the whole job (all sections).
