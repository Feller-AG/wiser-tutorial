# Access the Wiser-by-Feller WebSocket using wsdump

## Overview

Here an example how to interact with the Wiser-by-Feller WebSocket-Interface using `wsdump`.

## Install wsdump

For using [wsdump](https://websocket-client.readthedocs.io/en/latest/getting_started.html) you have to install the Python-Package [websocket-client](https://websocket-client.readthedocs.io).

It's recommended to install Python-Packages in a [Python-Virtual-Environment](https://docs.python.org/3.8/library/venv.html).

**Install Python-Package:**

``` bash
lapi@cowshed$ export PYVENV="ws-example-venv"

lapi@cowshed$ cd /tmp

# All-in-one
lapi@cowshed$ python3 -m venv ${PYVENV} && source ${PYVENV}/bin/activate && pip3 install websocket-client

# Check if the tool exists
(ws-example-venv) lapi@cowshed$ which wsdump 
/tmp/ws-example-venv/bin/wsdump
```

## Get the authentication code

See [authentication](./authentication.md) for more information. You can use [cURL](./tool_curl.md) to get an authentication token.

## Setup some variables

Change the IP-Address according your Gateway IP-Address.

**Set IP-Address and authentication token:**

``` bash
export GATEWAY_IP_ADDRESS="192.168.1.123"
export GATEWAY_TOKEN="60650cf4-5d26-4294-b1f2-6c06adc9d0d8"
```

## Interaction over WebSocket using wsdump

``` bash
(ws-example-venv) lapi@cowshed$ wsdump --headers="Authorization: Bearer ${GATEWAY_TOKEN}" ws://${GATEWAY_IP_ADDRESS}/api
Press Ctrl+C to quit

< {"load": {"id": 1, "state": {"bri": 10000}}}

> {"command": "dump_loads"}
< {"load": {"id": 1, "state": {"bri": 10000}}}
< {"load": {"id": 2, "state": {"bri": 0}}}
< {"load": {"id": 3, "state": {"moving": "stop", "tilt": 0, "level": 8160}}}

# Press Ctrl+C to quit
[Ctrl+C]

# Exit the Python-Virtual-Environment
(ws-example-venv) lapi@cowshed$ deactivate
lapi@cowshed$
```
