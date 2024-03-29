# Wiser-by-Feller RESTFul API Overview

> 🐮 Hi, my name is **Lapi**, I'm a happy swiss-cow! I am glad that you find the long way here! I will take you on my back and guide you through this wonderful documentation.

The Wiser-by-Feller RESTFul API enables you to manage all your **Wiser-by-Feller** system devices.

Per example, it's possible to turn on or off the lights in your house over the RESTFul API. You can get the state of the lights and do other crazy IoThings.

> 🐮 Wow sounds great, I would like to turn off the bell on my neck!

Information:

- All information about **Wiser-by-Feller** can be found here: https://wiser.feller.ch
- RestAPI information (OpenAPI): https://feller-ag.github.io/wiser-api

## Control your Wiser-by-Feller system over the RESTFul API

![Wiser Installation](./doc/images/wiser_api_home.png)

> 🐮 Looks like my cowshed!

## Get started

Learn about getting started with the RESTFul API and how to use it.

### 1) HTTP Guidelines

Follow the simple [HTTP Guidelines](./doc/http_guidelines.md).

> 🐮 I like simple guidelines!

### 2) Authentication

Every request to the Wiser-µGateway must include an [authentication](./doc/authentication.md) token.

> 🐮 The burn mark on my back!

### 3) Access to data

- If you want to turn **on** or **off** some lights, read more about [loads](./doc/api_loads.md).
- Get informed about [loads](./doc/api_loads.md) state changes using [WebSocket](./doc/websocket.md).
- How about a new [job](./doc/api_jobs.md)?
- Lets use a [smartbutton](./doc/api_smartbuttons.md) and get it married with a [job](./doc/api_jobs.md).
- Use [scripting](./doc/api_scripts.md) to invoke actions on 3rd party devices.

> 🐮 Please no more loads, you are heavy enough!

## Tools

- RESTFul API examples using [cURL](./doc/tool_curl.md)
- [WebSocket](./doc/websocket.md) examples with [wsdump](./doc/tool_wsdump.md)

> 🐮 The dairy machine, GPS-Receiver, ...

## FAQ

- What do you mean? Read [here](./doc/faq.md)!

## The End

``` bash
 _________
< Finally >
 ---------
        \   ^__^
         \  (**)\_______
            (__)\       )\/\
             U  ||----w |
                ||     ||
```

---
Made with ❤️ & 🐮 (...and some couples of 🍺) in Switzerland, Feller AG, 2021
