---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - javascript

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the documentation of the TurboBoy API!, you can use this api to manage services (create, get and update).

We have several examples of each API route in **shell** and **javascript**, which help to understand the documentation.

This example API documentation page was created with [Slate](https://github.com/lord/slate).

# Authentication

> To get the authorization token, execute the following code:

```shell
curl -X GET \
  'http://192.168.1.36:3000/api/v1/sign_in?email=kitten@email.com&password=kittenpassword'
```

```javascript
var request = require("request");

var options = { method: 'GET',
  url: 'http://192.168.1.36:3000/api/v1/sign_in',
  qs: { email: 'prueba@akt.com', password: 'prueba' },

request(options, function (error, response, body) {
  if (error) throw new Error(error);

  console.log(body);
});
```

> The successful JSON has the following structure:

```json
{
    "authentication_token": "meowmeowmeow",
    "success_messages": [
        "Usuario logeado"
    ]
}
```

> The failed JSON result has the following structure:

```json
{
    "error_messages": [
        ...
    ]
}
```

### HTTP Request

`GET /api/v1/sign_in?email=kitten@email.com&amp; password=kittenpassword HTTP/1.1
Host: 192.168.1.36:3000`

Before making any request to the API it is necessary to obtain the authorization 
token with the registered credentials in the turboboy system for the company.

The token arrives in the result as: `authentication_token` in this case the value is  `meowmeowmeow`

<aside class="notice">
You must replace <code>kitten@email.com</code> with the registered company email.
</aside>

<aside class="notice">
You must replace <code>kittenpassword</code> with the password associated with <code>kitten@email.com</code> email.
</aside>

# Services

## Validate an address

<aside class="success">
Remember add <code>authentication_token</code> to the header of all requests
</aside>

> Validating an address

```shell
curl -X GET \
  'http://192.168.1.36:3000/api/v1/validate-address?address=Centro%20Comercial%20Oviedo&city_name=medellin' \
  -H 'meowmeowmeow'
```

```javascript
var request = require("request");

var options = { method: 'GET',
  url: 'http://192.168.1.36:3000/api/v1/validate-address',
  qs: 
   { address: 'Centro%20Comercial%20Oviedo',
     city_name: 'medellin' },
  headers: 
   { 
     authentication_token: 'meowmeowmeow'
    } };

request(options, function (error, response, body) {
  if (error) throw new Error(error);

  console.log(body);
});
```

> The successful JSON has the following structure:

```json
{
  "response": {
    "success": true,
    "lat": "6.1987967",
    "lng": "-75.57362405"
  }
}
```

> The failed JSON result has the following structure:

```json
{
    "error_messages": [
        "Nombre ciudad es requerido",
        "Dirección es requerida"
    ]
}
```

this final point allows validating if a direction is well formed and returns the coordinates of the point

### HTTP Request

`GET /api/v1/validate-address?address=Centro Comercial Oviedo&amp; city_name=medellin HTTP/1.1
Host: 192.168.1.36:3000
authentication_token: meowmeowmeow`

### Query Parameters

Parameter | Type | Description
--------- | ------- | -----------
address | String | Address provided by the Google Maps API and its predictive field
city_name | String | Name of the corresponding city of the address
