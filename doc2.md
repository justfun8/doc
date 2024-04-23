
# API documentation

This repository contains the documentation for [petstore](https://petstore.swagger.io)’s API.

#### Contents

- [Overview](#1-overview)
- [Authentication](#2-authentication)
- [Resources](#3-resources)
  - [Pets](#31-pets)

## 1. Overview

You can directly use the foundation URL to access petstore API：
`https://petstore.swagger.io/v2`


## 2. Authentication
Open api, no account password token required.
## 3. Resources

The API is RESTful and arranged around resources. All requests must be made using `https`
### 3.1. Pets

#### Getting the pet’s details by petID
Returns details of the pet.

```
GET https://petstore.swagger.io/v2/pet/{petID}
```

Example request:

```
curl -X 'GET' \
  'https://petstore.swagger.io/v2/pet/1' \
  -H 'accept: application/json'
```

Example response:

```
HTTP/1.1 200 OK
 access-control-allow-headers: Content-Type,api_key,Authorization 
 access-control-allow-methods: GET,POST,DELETE,PUT 
 access-control-allow-origin: * 
 content-type: application/json 
 server: Jetty(9.2.9.v20150224) 

{
  "id": 1,
  "category": {
    "id": 1,
    "name": "string"
  },
  "name": "doggie",
  "photoUrls": [
    "string"
  ],
  "tags": [
    {
      "id": 1,
      "name": "string"
    }
  ],
  "status": "available"
}
```
responses the model of pet, these are the keys of the pet model.

| Field      | Type   | Description                                     |
| -----------|--------|-------------------------------------------------|
| id         | string | A unique identifier for the pet.               |
| category   | Object | The pet’s username.                  |
| name       | string | The pet’s name on Medium.                      |
| photoUrls  | string | The URL to the pet’s photo       |
| tags   | Array | The pet’s tags         |
| status   | string | The URL to the pet’s status         |


Possible errors:

| Error code           | Description                                     |
| ---------------------|-------------------------------------------------|
| 400 Bad Request      | 	Invalid ID supplied                                                         |
| 404 Not Found        | Pet not found |


#### Creating a post

Upload a pet image
```
POST https://petstore.swagger.io/v2/pet/{{petId}}/uploadImage
```

Where petId is the  id of the pet.

Example request:

```
curl -X 'POST' \
  'https://petstore.swagger.io/v2/pet/1/uploadImage' \
  -H 'accept: application/json' \
  -H 'Content-Type: multipart/form-data' \
  -F 'file=@screenshoot 2024-03-15 090733.png;type=image/png'
```

With the following fields:

| Parameter       | Type         | Required?  | Description                                     |
| -------------   |--------------|------------|-------------------------------------------------|
| petId           | int64       | required   | ID of pet that needs to be updated  |
| additionalMetadata            | string  | optional   | Additional data to pass to server       |
| file    | file       | optional   | file to upload |

Example server response:

```
HTTP/1.1 201 OK
Content-Type: application/json; charset=utf-8

{
  "code": 200,
  "type": "unknown",
  "message": "additionalMetadata: null\nFile uploaded to ./screenshoot 2024-03-15 090733.png, 66773 bytes"
}
```

responses the model of ApiResponse, these are the keys of the ApiResponse model.

| Field         | Type         | Description                                     |
| --------------|--------------|-------------------------------------------------|
| code            | string       | http code              |
| type         | string       |                                 |
| message      | string       | The url and size of the image                |

Responses code:

|  code           | Description                                                                                                          |
| ---------------------|----------------------------------------------------------------------------------------------------------------------|
| 415  	Unsupported Media Type     |  need upload correct file                                                      |
