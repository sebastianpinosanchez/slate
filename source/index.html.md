---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - javascript

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>
  - <h2><a href='https://raw.githubusercontent.com/sebastianpinosanchez/slate/master/source/Turboboy%20API.postman_collection.json'>Postman Collection</a></h2>

includes:
  #- errors

search: true
---

# Introduction

Welcome to the documentation of the TurboBoy API!, you can use this API to manage services (create, get and update).

We have several examples of each API route in **shell** and **javascript**, which help to understand the documentation.

This example API documentation page was created with [Slate](https://github.com/lord/slate).

1. **Production Host:** _turboboy.co_
2. **Development host:** _dev2.turboboy.co_

# Authentication

> To get the authorization token, execute the following code:

```shell
curl -X GET \
  'https://turboboy.co/api/v1/sign_in?email=kitten@email.com&password=kittenpassword'
```

```javascript
var request = require("request");

var options = { method: 'GET',
  url: 'https://turboboy.co/api/v1/sign_in',
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
Host: turboboy.co`

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

The cities for the city_name field are:

["Medellín","Bello","Caldas","Envigado","Guarne","Itagüí","La Estrella","Marinilla","Rionegro","Sabaneta","San Antonio de Prado","Copacabana","Girardota","Barbosa","El alto de las palmas","El Retiro","La Ceja","La Union"]

<aside class="success">
Remember add <code>authentication_token</code> to the header of all requests
</aside>

> Validating an address

```shell
curl -X GET \
  'https://turboboy.co/api/v1/validate-address?address=Centro%20Comercial%20Oviedo&city_name=medellin' \
  -H 'meowmeowmeow'
```

```javascript
var request = require("request");

var options = { method: 'GET',
  url: 'https://turboboy.co/api/v1/validate-address',
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

This endpoint allows validating if a direction is well formed and returns the coordinates of the point

### HTTP Request

`GET /api/v1/validate-address?address=Centro Comercial Oviedo&amp; city_name=medellin HTTP/1.1
Host: turboboy.co
authentication_token: meowmeowmeow`

### Query Parameters

Parameter | Type    | Mandatory | Default       | Description
--------- | ------- | --------- | -----------   | -----------
address   | String  | true      | doesn't apply | Address provided by the user
city_name | String  | true      | doesn't apply | Name of the corresponding city of the address

## Calculate service fee


> Calculating services fee

```shell
curl -X GET \
  'https://turboboy.co/api/v1/calc-fee?total_distance=9&has_procedures=true&return_origin=true' \
  -H 'authentication_token: meowmeowmeow
```

```javascript
var request = require("request");

var options = { method: 'GET',
  url: 'https://turboboy.co/api/v1/calc-fee',
  qs: 
   { total_distance: '9',
     has_procedures: 'true',
     return_origin: 'true' },
  headers: 
   { 
     authentication_token: 'meowmeowmeow' } };

request(options, function (error, response, body) {
  if (error) throw new Error(error);

  console.log(body);
});

```

> The successful JSON has the following structure:

```json
{
  "response": {
    "fee": 24950
  }
}
```

> The failed JSON result has the following structure:

```json
{
  "error_messages": [
    "Distancia debe ser mayor a 0."
  ]
}
```

This endpoint calculates the fee given the characteristics of a Service

### HTTP Request

`GET /api/v1/calc-fee?total_distance=9&amp; has_procedures=true&amp; return_origin=true HTTP/1.1
Host: turboboy.co
authentication_token: meowmeowmeow`


### Query Parameters

Parameter | Type    | Mandatory | Default       | Description
--------- | ------- | --------- | -----------   | -----------
total_distance   | String  | true      | doesn't apply | Number of kilometers the service has
has_procedures | Boolean  | false      | false | If the service has procedure
return_origin | Boolean  | false      | false | If the service must return to the origin

## Calculate service distance

> Calculating services distance

```shell
curl -X GET \
  'https://turboboy.co/api/v1/calc-distance?start_point=40.6655101,%20-73.8918&end_point=40.6905615,-73.9976592' \
  -H 'authentication_token: meowmeowmeow
```

```javascript
var request = require("request");

var options = { method: 'GET',
  url: 'https://turboboy.co/api/v1/calc-distance',
  qs: 
   { start_point: '40.6655101,%20-73.8918',
     end_point: '40.6905615,-73.9976592' },
  headers: 
   { 
     authentication_token: 'meowmeowmeow' } };

request(options, function (error, response, body) {
  if (error) throw new Error(error);

  console.log(body);
});
```

> The successful JSON has the following structure:

```json
{
  "response": 11
}
```

> The failed JSON result has the following structure:

```json
{
  "error_messages": [
    "Deben existir 2 puntos para calcular la distancia"
  ]
}
```

This endpoint calculates the distance that must be covered for a service with points A and B

### HTTP Request

`GET /api/v1/calc-distance?start_point=40.6655101, -73.8918&amp; end_point=40.6905615,-73.9976592 HTTP/1.1
Host: turboboy.co
authentication_token: meowmeowmeow`

### Query Parameters

Parameter | Type    | Mandatory | Default       | Description
--------- | ------- | --------- | -----------   | -----------
start_point   | String  | true      | doesn't apply | String with structure: latitude, longitude
end_point | String  | true      | doesn't apply  | String with structure: latitude, longitude

## Validate service

> Validating service

```shell
curl -X GET \
  https://turboboy.co/api/v1/validate-service \
  -H 'Content-Type: application/json' \
  -H 'authentication_token: meowmeowmeow \
  -d '{
	"origin":{
		"city_name":"medellin",
		"address":"Cra 43A ##6 Sur-15",
		"contact":"Sebastian",
		"comments":"Nothing"
	},
	"destinations":[{
		"city_name":"medellin",
		"address":"Cra. 48 ##10 45"
	}]
}'
```

```javascript
var request = require("request");

var options = { method: 'GET',
  url: 'https://turboboy.co/api/v1/validate-service',
  headers: 
   { 'Content-Type': 'application/json',
     authentication_token: 'meowmeowmeow' },
  body: 
   { origin: 
      { city_name: 'medellin',
        address: 'Cra 43A ##6 Sur-15',
        contact: 'Sebastian',
        comments: 'Nothing' },
     destinations: [ { city_name: 'medellin', address: 'Cra. 48 ##10 45' } ] },
  json: true };

request(options, function (error, response, body) {
  if (error) throw new Error(error);

  console.log(body);
});

```

> The successful JSON has the following structure with: (uuid corresponds to the service cached on the server)

```json
{
  "uuid": "904390f736af063b605b"
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

This endpoint point calculates if a service is well formed

### HTTP Request

`GET /api/v1/validate-service HTTP/1.1
Host: turboboy.co:3000
authentication_token: meowmeowmeow
Content-Type: application/json
{
	"origin":{
		"city_name":"medellin",
		"address":"Cra 43A ##6 Sur-15",
		"contact":"Sebastian",
		"comments":"Nothing"
	},
	"destinations":[{
		"city_name":"medellin",
		"address":"Cra. 48 ##10 45"
	}]
}`

### Query Parameters

Parameter | Type    | Mandatory | Default       | Description
--------- | ------- | --------- | -----------   | -----------
origin   | JSON  | true      | doesn't apply | Information about the point of origin of the service
destinations | Array  | true      | doesn't apply  | Information of the intermediate and final points for a service
origin.city_name   | String  | true      | doesn't apply | City ​​of origin of the service
origin.address   | String  | true      | doesn't apply | Address provided by the user
origin.contact   | String  | true      | doesn't apply | Name of the person responsible for the service
origin.comments   | String  | false      | doesn't apply | Service comments
destinations[n].city_name   | String  | false      | doesn't apply | City ​​of final or intermediate point of the service
destinations[n].address   | String  | false      | doesn't apply | Address provided by the user

## Create service

> Creating service

```shell
curl -X POST \
  'https://turboboy.co/api/v1/create-service?uuid=b4428ac5111fbde9e8b5' \
  -H 'authentication_token: meowmeowmeow \
```

```javascript
var request = require("request");

var options = { method: 'POST',
  url: 'https://turboboy.co/api/v1/create-service',
  qs: { uuid: 'b4428ac5111fbde9e8b5' },
  headers: 
   { 
     authentication_token: 'meowmeowmeow' } };

request(options, function (error, response, body) {
  if (error) throw new Error(error);

  console.log(body);
});


```

> The successful JSON has the following structure with: (uuid corresponds to the service cached on the server)

```json
{
  "success_messages": [
    "Servicio creado"
  ],
  "uuid": 1
}
```


> The failed JSON result has the following structure:

```json
{
    "error_messages": [
        "Servicio expiró"
    ],
    "uuid": null
}
```

This endpoint point calculates if a service is well formed

### HTTP Request

`POST /api/v1/create-service?uuid=b4428ac5111fbde9e8b5 HTTP/1.1
Host: turboboy.co
authentication_token: meowmeowmeow`

### Query Parameters

Parameter | Type    | Mandatory | Default       | Description
--------- | ------- | --------- | -----------   | -----------
uuid   | String  | true      | doesn't apply | Unique identification provided by the validate_service endpoint

## Get service status

> Getting service status

```shell
curl -X GET \
  'https://turboboy.co/api/v1/service-status?uuid=1' \
  -H 'authentication_token: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VyX2lkIjoxLCJleHAiOjE1ODgxOTMwNTIsImlzcyI6Imlzc3Vlcl9uYW1lIiwiYXVkIjoiY2xpZW50In0.MyncNrNrVQahs7cA00WEWA1Y3D3DuartT3WmyLgWHwI'
```

```javascript
var request = require("request");

var options = { method: 'GET',
  url: 'https://turboboy.co/api/v1/service-status',
  qs: { uuid: '1' },
  headers: 
   {
     authentication_token: 'eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VyX2lkIjoxLCJleHAiOjE1ODgxOTMwNTIsImlzcyI6Imlzc3Vlcl9uYW1lIiwiYXVkIjoiY2xpZW50In0.MyncNrNrVQahs7cA00WEWA1Y3D3DuartT3WmyLgWHwI' } };

request(options, function (error, response, body) {
  if (error) throw new Error(error);

  console.log(body);
});

```

> The successful JSON has the following structure

```json
{
    "status": "Creado"
}
{
    "status": "Asignado a mensajero"
}
{
    "status": "Paquete recogido por el mensajero"
}
{
    "status": "Paquete entregado"
}
{
    "status": "Cancelado por el usuario"
}
{
    "status": "Cancelado por el mensajero"
}
{
    "status": "Servicio Expiró"
}
```


> The failed JSON result has the following structure:

```json
{
    "error_messages": [
        "Servicio no existe"
    ]
}
```

This endpoint provides the status of a service

### HTTP Request

`GET /api/v1/service-status?uuid=1 HTTP/1.1
Host: turboboy.co
authentication_token: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VyX2lkIjoxLCJleHAiOjE1ODgxOTMwNTIsImlzcyI6Imlzc3Vlcl9uYW1lIiwiYXVkIjoiY2xpZW50In0.MyncNrNrVQahs7cA00WEWA1Y3D3DuartT3WmyLgWHwI`

### Query Parameters

Parameter | Type    | Mandatory | Default       | Description
--------- | ------- | --------- | -----------   | -----------
uuid   | String  | true      | doesn't apply | uuid provided in the creation of the service

