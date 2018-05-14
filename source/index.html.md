---
title: Events Manager API Doc

language_tabs: # must be one of https://git.io/vQNgJ
  - javascript

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Events Manager API! 

Events Manager is a platform that helps manage creation and development of events such as conferences, ceremonies, weddings, formal parties, concerts, or conventions and as well provide centers to host these events. Suppose a user has an event coming up, He/She can post it on Events Manager and get a center.

This API provides you with all the endpoints you need to create your own version of the Events Manager application


To view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

This Events Manager API documentation page was created with [Slate](https://github.com/lord/slate).

# Development
### The API was built using
- Node - [Node](https://nodejs.org/en/)
- ExpressJs - [Express](https://expressjs.com/)
- PostgreSql - [PostgreSql](https://www.postgresql.org/)
- Sequelize orm - [Sequelize orm](http://docs.sequelizejs.com/manual/installation/getting-started)

# Authentication

Authentication has been put in place for secured routes. Most of the routes in this endpoints are secured and a user will need to provide an authourization token to access them. The token is only provided when a user creates an account or signs in to use the application. Read on to know how the token is used for requests:

<!-- > To authorize, use this code:

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
```

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
```

> Make sure to replace `meowmeowmeow` with your API key.

Kittn uses API keys to allow access to the API. You can register a new Kittn API key at our [developer portal](http://example.com/developers).

Kittn expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: meowmeowmeow`

<aside class="notice">
You must replace <code>meowmeowmeow</code> with your personal API key.
</aside> -->

# Installation
- Install  `node` and `postgres` 
- Clone the repository: 
```
> $ git clone https://github.com/Abudu-Samuel/Events-Manager
```
- Change directory into events-manager directory
```
> $ cd events-manager
```
- Install dependencies 
```
> $ npm install
```
- Once installation is done, create a `.env` file and fill it with the neccessary environment variables.
- Create a database to be used with the application
- Migrate database by running
```sh
> $ sequelize db:migrate
```
- Start app
```sh
> $ npm start:dev
```
- Consume endpoints using postman [Postman](https://www.getpostman.com/)

# Endpoints
### User Endpoints
Summary | Endpoint | Description | Request Method
--------- | ------- | ----------- | -----------
SignUp | api/v1/users | This creates a new user | POST
SignIn | api/v1/users/login | This logs an existing user in to the application. This is true for both admin and normal users | POST
### Admin Endpoints
Summary | Endpoint | Description | Request Method
--------- | ------- | ----------- | -----------
Add Center | api/v1/centers | This allows an admin to create a center to the database. | POST
Edit Center | api/v1/centers/center/centerid | This allows an admin to edit a center | PUT
### Center Endpoints
Summary | Endpoint | Description | Request Method
--------- | ------- | ----------- | -----------
Newly added centers | api/v1/centers/latest | This gets the three latest centers added to the database. | GET
Get Centers | api/v1/centers/ | This gets all centers in the database | GET
Get A Center | api/v1/centers/center/centerid | This gets a single center in the database | GET
### Event Endpoints
Summary | Endpoint | Description | Request Method
--------- | ------- | ----------- | -----------
Add Event | api/v1/events/ | This allows a user to add an event to the database. | POST
Newly added events | api/v1/events/latest | This gets the three latest events added to the database| GET
Get User Event(s) | api/v1/events/user/events | This gets event created by a specific user | GET
Edit Event | api/v1/events/event/eventid | This allows a user to edit an event | PUT
Get An Event | api/v1/events/event/eventid | This gets a single event in the database | GET
Get Events | api/v1/events | This gets all events in the database | GET
Delete Event | api/v1/events/event/eventid | This allows a user to delete event(s) he/she created | DELETE
Slated Event(s) | api/vi/events/center/eventid | This gets event(s) slated for a single center | GET

# User Endpoints Examples
## User Signup

```javascript

```

> Request Body

```json

  {
    "firstname": "testing",
    "lastname": "example",
    "email": "testing@example.com",
    "username": "testexamp",
    "password": "password"
  }

```

> Response Body

```json

  {
    "responseData": {
      "message": "Account Created",
      "id": 2,
      "username": "testexamp",
      "email": "testing@example.com",
      "firstname": "testing",
      "lastname": "example",
    }
  }

```
### Request
- Endpoint: `Post ('/users')`
- Body: `Application/json`


### Query Parameters
Parameter | Required | Validation
--------- | --------- | ---------
Firstname | true | Must be a string and must not be less than three characters.
Lastname | true | Must be a string and must not be less than three characters.
Username | true | Must be a string and must not be less than three characters.
Email | true | Must be a valid email
Password | true | Must not be less than 5 characters long
### Response
- Status: 201: created
- Body: `Application/json`

### Error status codes
- 400 - Bad Request
- 409 - Conflict
- 500 - Internal server error

## User Signin

```javascript

```

> Request Body

```json

  {
    "username": "testexamp",
    "password": "password"
  }

```

> Response Body

```json

  {
      "message": "Sign in Successful!",
      "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6NCwiZW1haWwiOiJleGFtcGxlQGV4YW1wbGUuY29tIiwibWVtYmVyc2hpcCI6ImJyb256ZSIsInJvbGUiOiJ1c2VyIiwiaWF0IjoxNTE2ODgwMzIyLCJleHAiOjE1MTY5NjY3MjJ9.XqZL8Cv3t4x53mnQ-9GfGayUFxMGS2hfdjbjbjeIFEw"
  }

```
### Request
- Endpoint: `Post ('/users/login')`
- Body: `Application/json`


### Query Parameters
Parameter | Required | Validation
--------- | --------- | ---------
Username | true | Must be a string and must not be less than three characters.
Password | true | Must not be less than 5 characters long
### Response
- Status: 200: Ok
- Body: `Application/json`

### Error status codes
- 400 - Bad Request
- 401 - Unauthorized
- 500 - Internal server error

# Admin Endpoints Examples
## Add center

```javascript

```

> Request Header

```json

  {
    "authorization": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6NCwiZW1haWwiOiJleGFtcGxlQGV4YW1wbGUuY29tIiwibWVtYmVyc2hpcCI6ImJyb256ZSIsInJvbGUiOiJ1c2VyIiwiaWF0IjoxNTE2ODgwMzIyLCJleHAiOjE1MTY5NjY3MjJ9.XqZL8Cv3t4x53mnQ-9GfGayUFxMGS2hfdjbjbjeIFEw"
  }

```

> Request Body

```json

  {
      "name": "Grand Hall",
      "capacity": 300,
      "location": "Ikeja",
      "price": 500000.000,
      "state": "Lagos",
      "description": "Awesome Event Center",
      "image": "http://image.com",
      "isAvailable": true
  }

```

> Response Body

```json

  {
      "message": "Center created Successfully",
      "id": 1,
      "name": "Grand Hall",
      "capacity": 300,
      "location": "Ikeja",
      "price": 500000.000,
      "state": "Lagos",
      "description": "Awesome Event Center",
      "image": "http://image.com",
      "isAvailable": true
  }

```

### Request
- Endpoint: `Post ('/centers')`
- Body: `Application/json`


### Query Parameters
Parameter | Required | Validation
--------- | --------- | ---------
Name | true | Must be a string
Capacity | true | Must be a number
Location | true | Must be a string
Price | true | Must be a number
State | true | Must be a string
Description | true | Must be a string
Image | true | Must be a string
isAvailable | true | Must be a boolean
### Response
- Status: 201: created
- Body: `Application/json`

### Error status codes
- 400 - Bad Request
- 401 - Unauthorized

## Edit center

```javascript

```

> Request Header

```json

  {
    "authorization": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6NCwiZW1haWwiOiJleGFtcGxlQGV4YW1wbGUuY29tIiwibWVtYmVyc2hpcCI6ImJyb256ZSIsInJvbGUiOiJ1c2VyIiwiaWF0IjoxNTE2ODgwMzIyLCJleHAiOjE1MTY5NjY3MjJ9.XqZL8Cv3t4x53mnQ-9GfGayUFxMGS2hfdjbjbjeIFEw"
  }

```

> Request Body

```json

  {
      "name": "Grand Hall Updated",
      "capacity": 300,
      "location": "Ikeja",
      "price": 500000.000,
      "state": "Lagos",
      "description": "Awesome Event Center",
      "image": "http://image.com",
      "isAvailable": true
  }

```

> Response Body

```json

  {
      "message": "Center modification is Successfully",
      "id": 1,
      "name": "Grand Hall Updated",
      "capacity": 300,
      "location": "Ikeja",
      "price": 500000.000,
      "state": "Lagos",
      "description": "Awesome Event Center",
      "image": "http://image.com",
      "isAvailable": true
  }

```

### Request
- Endpoint: `Post ('/centers/center/centerid')`
- Body: `Application/json`


### Query Parameters
Parameter | Required | Validation
--------- | --------- | ---------
Name | true | Must be a string
Capacity | true | Must be a number
Location | true | Must be a string
Price | true | Must be a number
State | true | Must be a string
Description | true | Must be a string
Image | true | Must be a string
isAvailable | true | Must be a boolean
### Response
- Status: 201: created
- Body: `Application/json`

### Error status codes
- 400 - Bad Request
- 401 - Unauthorized

# Center Endpoints Examples
## Get latest centers

```javascript

```

> Response Body

```json

  {
      "message": "Centers Found",
      "foundCenters": [
        {
          "id": 1,
          "name": "Grand Hall",
          "capacity": 300,
          "location": "Ikeja",
          "price": 500000.000,
          "state": "Lagos",
          "description": "Awesome Event Center",
          "image": "http://image.com",
          "isAvailable": true
        },
        {
           "id": 2,
            "name": "Ovation Hall",
            "capacity": 300,
            "location": "Ipaja",
            "price": 500000.000,
            "state": "Lagos",
            "description": "Awesome Event Center",
            "image": "http://image.com",
            "isAvailable": true
        },
        {
           "id": 3,
            "name": "Lively Hall",
            "capacity": 300,
            "location": "Agege",
            "price": 500000.000,
            "state": "Lagos",
            "description": "Awesome Event Center",
            "image": "http://image.com",
            "isAvailable": true
        }
      ]
     
  }

```

### Request
- Endpoint: `Get ('/centers/latest')`
- Body: `Application/json`

### Response
- Status: 200: ok
- Body: `Application/json`

### Error status codes
- 500 - Internal server error


## Get a center

```javascript

```

> Request Header

```json

  {
    "authorization": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6NCwiZW1haWwiOiJleGFtcGxlQGV4YW1wbGUuY29tIiwibWVtYmVyc2hpcCI6ImJyb256ZSIsInJvbGUiOiJ1c2VyIiwiaWF0IjoxNTE2ODgwMzIyLCJleHAiOjE1MTY5NjY3MjJ9.XqZL8Cv3t4x53mnQ-9GfGayUFxMGS2hfdjbjbjeIFEw"
  }

```

> Response Body

```json

  {
      "message": "Center found",
      "center": {
      "id": 1,
      "name": "Grand Hall Updated",
      "capacity": 300,
      "location": "Ikeja",
      "price": 500000.000,
      "state": "Lagos",
      "description": "Awesome Event Center",
      "image": "http://image.com",
      "isAvailable": true
      }
  }

```

### Request
- Endpoint: `Get ('/centers/center/centerid')`
- Body: `Application/json`

### Response
- Status: 200: Ok
- Body: `Application/json`

### Error status codes
- 500 - Internal server error

# Event Endpoints Examples
## Add event

```javascript

```

> Request Header

```json

  {
    "authorization": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6NCwiZW1haWwiOiJleGFtcGxlQGV4YW1wbGUuY29tIiwibWVtYmVyc2hpcCI6ImJyb256ZSIsInJvbGUiOiJ1c2VyIiwiaWF0IjoxNTE2ODgwMzIyLCJleHAiOjE1MTY5NjY3MjJ9.XqZL8Cv3t4x53mnQ-9GfGayUFxMGS2hfdjbjbjeIFEw"
  }

```

> Request Body

```json

  {
      "userId": 1,
      "centerId": 1,
      "title": "Youth Elevation Event",
      "date": "2018-12-05",
      "type": "Educational",
      "description": "Awesome Event For youths",
      "image": "http://image.com"
  }

```

> Response Body

```json

  {
      "message": "Event Created",
      "createdEvent": 
        {
          "id": 1,
          "userId": 1,
          "centerId": 1,
          "title": "Youth Elevation Event",
          "date": "2018-12-05",
          "type": "Educational",
          "description": "Awesome Event For youths",
          "image": "http://image.com"
        }
  }

```

### Request
- Endpoint: `Post ('/events')`
- Body: `Application/json`

### Query Parameters
Parameter | Required | Validation
--------- | --------- | ---------
Title | true | Must be a string
Date | true | Must be a string
Type | true | Must be a string
Description | true | Must be a string
Image | true | Must be a string

### Response
- Status: 201: created
- Body: `Application/json`

### Error status codes
- 400 - Bad request
- 500 - Internal server error


## Edit an event

```javascript

```

> Request Header

```json

  {
    "authorization": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6NCwiZW1haWwiOiJleGFtcGxlQGV4YW1wbGUuY29tIiwibWVtYmVyc2hpcCI6ImJyb256ZSIsInJvbGUiOiJ1c2VyIiwiaWF0IjoxNTE2ODgwMzIyLCJleHAiOjE1MTY5NjY3MjJ9.XqZL8Cv3t4x53mnQ-9GfGayUFxMGS2hfdjbjbjeIFEw"
  }

```

> Request Body

```json

  {
      "userId": 1,
      "centerId": 1,
      "title": "Youth Elevation Event updated",
      "date": "2018-12-05",
      "type": "Educational",
      "description": "Awesome Event For youths",
      "image": "http://image.com"
  }

```

> Response Body

```json

  {
      "message": "Event modification is successful",
      "updatedEvent": {
      "id": 1,
      "userId": 1,
      "centerId": 1,
      "title": "Youth Elevation Event updated",
      "date": "2018-12-05",
      "type": "Educational",
      "description": "Awesome Event For youths",
      "image": "http://image.com"
      }
  }

```

### Request
- Endpoint: `Put ('/events/event/eventid')`
- Body: `Application/json`

### Query Parameters
Parameter | Required | Validation
--------- | --------- | ---------
Title | true | Must be a string
Date | true | Must be a string
Type | true | Must be a string
Description | true | Must be a string
Image | true | Must be a string

### Response
- Status: 200: Ok
- Body: `Application/json`

### Error status codes
- 400 - Bad request
- 422 - Unauthorized
- 500 - Internal server error

## Delete an event

```javascript

```

> Request Header

```json

  {
    "authorization": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6NCwiZW1haWwiOiJleGFtcGxlQGV4YW1wbGUuY29tIiwibWVtYmVyc2hpcCI6ImJyb256ZSIsInJvbGUiOiJ1c2VyIiwiaWF0IjoxNTE2ODgwMzIyLCJleHAiOjE1MTY5NjY3MjJ9.XqZL8Cv3t4x53mnQ-9GfGayUFxMGS2hfdjbjbjeIFEw"
  }

```

> Response Body

```json

  {
      "message": "Event deleted",
  }

```

### Request
- Endpoint: `Delete ('/events/event/eventid')`
- Body: `Application/json`

### Response
- Status: 200: Ok
- Body: `Application/json`

### Error status codes
- 422 - Unauthorized
- 500 - Internal server error

## Get an event

```javascript

```

> Request Header

```json

  {
    "authorization": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6NCwiZW1haWwiOiJleGFtcGxlQGV4YW1wbGUuY29tIiwibWVtYmVyc2hpcCI6ImJyb256ZSIsInJvbGUiOiJ1c2VyIiwiaWF0IjoxNTE2ODgwMzIyLCJleHAiOjE1MTY5NjY3MjJ9.XqZL8Cv3t4x53mnQ-9GfGayUFxMGS2hfdjbjbjeIFEw"
  }


```

> Response Body

```json

  {
      "message": "Event Found",
      "Event": {
      "id": 1,
      "userId": 1,
      "centerId": 1,
      "title": "Youth Elevation Event updated",
      "date": "2018-12-05",
      "type": "Educational",
      "description": "Awesome Event For youths",
      "image": "http://image.com"
      }
  }

```

### Request
- Endpoint: `Get ('/events/event/eventid')`
- Body: `Application/json`

### Response
- Status: 200: Ok
- Body: `Application/json`

### Error status codes
- 500 - Internal server error

## Get all events
```javascript

```

> Request Header

```json

  {
    "authorization": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6NCwiZW1haWwiOiJleGFtcGxlQGV4YW1wbGUuY29tIiwibWVtYmVyc2hpcCI6ImJyb256ZSIsInJvbGUiOiJ1c2VyIiwiaWF0IjoxNTE2ODgwMzIyLCJleHAiOjE1MTY5NjY3MjJ9.XqZL8Cv3t4x53mnQ-9GfGayUFxMGS2hfdjbjbjeIFEw"
  }

```

> Response Body

```json

  {
      "message": "Events Found",
      "Event": [
      {
        "id": 1,
        "userId": 1,
        "centerId": 1,
        "title": "Youth Elevation Event updated",
        "date": "2018-12-05",
        "type": "Educational",
        "description": "Awesome Event For youths",
        "image": "http://image.com"
      },
      {
        "id": 2,
        "userId": 1,
        "centerId": 1,
        "title": "Coming of the kings",
        "date": "2018-12-05",
        "type": "Educational",
        "description": "Awesome Event For youths",
        "image": "http://image.com"
      },
      {
        "id": 3,
        "userId": 1,
        "centerId": 1,
        "title": "Make it right",
        "date": "2018-12-05",
        "type": "Educational",
        "description": "Awesome Event For youths",
        "image": "http://image.com"
      },
      {
        "id": 4,
        "userId": 1,
        "centerId": 1,
        "title": "You and me conference",
        "date": "2018-12-05",
        "type": "Educational",
        "description": "Awesome Event For youths",
        "image": "http://image.com"
      }
      ]
  }

```

### Request
- Endpoint: `Get ('/events/')`
- Body: `Application/json`

### Response
- Status: 200: Ok
- Body: `Application/json`

### Error status codes
- 500 - Internal server error

## Get three latest events

```javascript

```

> Request Header

```json

  {
    "authorization": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6NCwiZW1haWwiOiJleGFtcGxlQGV4YW1wbGUuY29tIiwibWVtYmVyc2hpcCI6ImJyb256ZSIsInJvbGUiOiJ1c2VyIiwiaWF0IjoxNTE2ODgwMzIyLCJleHAiOjE1MTY5NjY3MjJ9.XqZL8Cv3t4x53mnQ-9GfGayUFxMGS2hfdjbjbjeIFEw"
  }

```

> Response Body

```json

  {
      "message": "Events Found",
      "Event": [
      {
        "id": 4,
        "userId": 1,
        "centerId": 1,
        "title": "You and me conference",
        "date": "2018-12-05",
        "type": "Educational",
        "description": "Awesome Event For youths",
        "image": "http://image.com"
      },
      {
        "id": 3,
        "userId": 1,
        "centerId": 1,
        "title": "Make it right",
        "date": "2018-12-05",
        "type": "Educational",
        "description": "Awesome Event For youths",
        "image": "http://image.com"
      },
      {
        "id": 2,
        "userId": 1,
        "centerId": 1,
        "title": "Coming of the kings",
        "date": "2018-12-05",
        "type": "Educational",
        "description": "Awesome Event For youths",
        "image": "http://image.com"
      }
      ]
  }

```

### Request
- Endpoint: `Get ('/events/latest')`
- Body: `Application/json`

### Response
- Status: 200: Ok
- Body: `Application/json`

### Error status codes
- 500 - Internal server error
