# wiser-api

More information can be found on https://wiser.feller.ch/


## Control your wiser system over the local API
![Wiser Installation](doc/images/wiser_api_home.png)


### Manage your loads via the RESTful API

#### GET /loads

The loads services provides access to all loads (lights & blinds) of your installation.

**Example Request:**
```
GET api/loads HTTP/1.1
```

**Example Response:**
```
HTTP/1.1 200 OK
Content-Type: application/json
```
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


#### GET /loads/state
**Example Request:**
```
GET /api/loads/state
```

**Example Response:**
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

#### PUT /loads/< id >/target_state
**Example Request:**
```
GET api/loads/6/target_state
```

**Example Response:**
``` json

```


#### PUT /loads/< id >/ctrl
**Example Request:**
```
GET /api/loads/6/ctrl
```

**Example Response:**
``` json

```
