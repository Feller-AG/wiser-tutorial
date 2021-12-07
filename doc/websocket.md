# Manage your loads via WebSocket

> 🐮 Strange thing, who need this?

## Overview

It's possible to get inform about a [load](./api_loads.md) state change over a WebSocket connection.

Connecting per WebSocket to this entrypoint ``ws://<HOST-OR-IP-ADDRESS>/api`` let you feel the state-changes of your  **Wiser-by-Feller** system devices.

All messages are formatted as JSON. The interface also allow to send some `commands`, you can see it in our examples as a `request`.

**Add the [authentication token](./authentication.md) in the HTTP-Header when you initiate the connection!**

Here an example using the simple command-line tool [wsdump](./tool_wsdump.md).

## Load state changes

As soon as the state of a load change you will get informed.
Press a button of your switch and you will be notified which load has changed his state.
It's important to know that just changes are transmitted!

The attributes of the response is the same as we know from the RESTful-API [/api/loads/state](./api_loads.md).

### Example `onoff` type

**Response:**

``` json
{"load": {"id": 1, "state": {"bri": 10000}}}
```

### Example `dim` type

**Response:**

``` json
{"load": {"id": 2, "state": {"bri": 0}}}
```

### Example `motor` type

**Response:**

``` json
{"load": {"id": 3, "state": {"moving": "stop", "tilt": 0, "level": 8160}}}
```

## Get all load states

Get the current state of all loads.

**Request:**

``` json
{"command": "dump_loads"}
```

**Response:**

``` json
{"load": {"id": 1, "state": {"bri": 10000}}}
{"load": {"id": 2, "state": {"bri": 0}}}
{"load": {"id": 3, "state": {"moving": "stop", "tilt": 0, "level": 8160}}}
```
