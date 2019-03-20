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

The token arrives in the result as: `authentication_token`

<aside class="notice">
You must replace <code>kitten@email.com</code> with the registered company email.
</aside>

<aside class="notice">
You must replace <code>kittenpassword</code> with the password associated with <code>kitten@email.com</code> email.
</aside>

# Kittens

## Get All Kittens

```shell
curl "http://example.com/api/kittens"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let kittens = api.kittens.get();
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

This endpoint retrieves all kittens.

### HTTP Request

`GET http://example.com/api/kittens`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>
