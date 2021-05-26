# Wiser-by-Feller RESTFul API Overview

The Wiser-by-Feller RESTFul API enables you to manage your system devices.
So that you can build your own apps on any platform.

More information can be found on https://wiser.feller.ch

## Control your Wiser-by-Feller system over the RESTFul API

![Wiser Installation](doc/images/wiser_api_home.png)


# Get started

## HTTP Guidelines

- [JSend](https://github.com/omniti-labs/jsend) - Simple JSON responses.
- A successful request is indicated by HTTP status code: `200 OK`
- Supported HTTP versions are: `HTTP/1.0, HTTP/1.1`
- HTTP methods (Verbs): `GET, PUT, DELETE, POST, PATCH`


## Authentication

Every request to the Wiser-uGateway must include an authentication token.

Read [here](./authentication.md) how you get an authentication token.


## Access to data

 - If you want to turn **on** or **off** some lights, read more about [loads](./loads.md)
 - [TODO]


## Tools

 - cUrl
 - Postman
 - Python
 - ...