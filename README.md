# To-do List API [![Build Status](https://travis-ci.org/tsoliangwu0130/todo-list-api.svg?branch=master)](https://travis-ci.org/tsoliangwu0130/todo-list-api) [![MIT licensed](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)

A [Node.js](https://nodejs.org/en/) to-do list RESTful API with security and authentication supported.

## Prerequisite

### MongoDB

You'll need to run [MongoDB](https://www.mongodb.com/) on your machine in order to support CRUD operations for this API. Simply install MongoDB with [Homebrew](https://brew.sh/):

```
$ brew install mongodb
```

Then run MongoDB with [mongod](https://docs.mongodb.com/manual/reference/program/mongod/#bin.mongod) process:

```
$ mongod --dbpath ~/data/db
```

### Configuration

You'll also need to create a `config.json` file to setup the environment and place it under `server/config/`. The following is a simple example of `config.json`:

```json
{
  "test": {
    "PORT": 3000,
    "MONGODB_URI": "mongodb://localhost:27017/TodoAppTest",
    "JWT_SECRET": "jwtsecret"
  },
  "development": {
    "PORT": 3000,
    "MONGODB_URI": "mongodb://localhost:27017/TodoApp",
    "JWT_SECRET": "jwtsecret"
  }
}
```

## Usage

To install app dependencies, simply run:

```
$ npm install
```

Start the app at [localhost:3000](http://localhost:3000):

```
$ npm start
```

## Docker Compose

You can also run this app in [Docker](https://www.docker.com/) containers with [Docker Compose](https://docs.docker.com/compose/). To do so, just ensure you have `docker` and `docker-compose` installed and have the `config.json` file prepared, then simply run:

```
$ docker-compose up
```

## Resources

### todos

The following sections are all supported operations for todos resource.

#### GET /todos

Retrieve all todos for the same user with `x-auth` token.

```
GET /todos HTTP/1.1
x-auth: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJfaWQiOiI1OTY5MWM4MDJkODIxYmExNTU3YjczZTciLCJhY2Nlc3MiOiJhdXRoIiwiaWF0IjoxNTAwMDYwODAwfQ.af2PQl2HMduHU3FeXFMjxTShO97l1QYAclvweh5lBsc
```

```
HTTP/1.1 200 OK
Connection: keep-alive
Content-Length: 327
Content-Type: application/json; charset=utf-8
Date: Fri, 14 Jul 2017 19:58:44 GMT
ETag: W/"147-iRd3m2buVy9hAeukGKbirv8+2qE"
X-Powered-By: Express

{
    "todos": [
        {
            "_id": "596921872d821ba1557b73ea",
            "text": "Something to do from Postman",
            "_creator": "59691c802d821ba1557b73e7",
            "__v": 0,
            "completedAt": null,
            "completed": false
        },
        {
            "_id": "596922362d821ba1557b73eb",
            "text": "Another thing to do from Postman",
            "_creator": "59691c802d821ba1557b73e7",
            "__v": 0,
            "completedAt": null,
            "completed": false
        }
    ]
}
```

#### GET /todos/:id

Retrieve one specific todo with todo's unique ID and `x-auth` token.

```
GET /todos/596921872d821ba1557b73ea HTTP/1.1
x-auth: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJfaWQiOiI1OTY5MWM4MDJkODIxYmExNTU3YjczZTciLCJhY2Nlc3MiOiJhdXRoIiwiaWF0IjoxNTAwMDYwODAwfQ.af2PQl2HMduHU3FeXFMjxTShO97l1QYAclvweh5lBsc
```

```
HTTP/1.1 200 OK
Connection: keep-alive
Content-Length: 164
Content-Type: application/json; charset=utf-8
Date: Fri, 14 Jul 2017 20:01:44 GMT
ETag: W/"a4-DaODaXXlg9LzU2j5ykmjVxLzdQs"
X-Powered-By: Express

"todo": {
    "_id": "596921872d821ba1557b73ea",
    "text": "Something to do from Postman",
    "_creator": "59691c802d821ba1557b73e7",
    "__v": 0,
    "completedAt": null,
    "completed": false
}
```

#### POST /todos

Create a new todo with `x-auth` token.

```
POST /todos HTTP/1.1
Content-Type: application/json
x-auth: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJfaWQiOiI1OTY5MWM4MDJkODIxYmExNTU3YjczZTciLCJhY2Nlc3MiOiJhdXRoIiwiaWF0IjoxNTAwMDYwODAwfQ.af2PQl2HMduHU3FeXFMjxTShO97l1QYAclvweh5lBsc

{
  "text": "Something to do from Postman"
}
```

```
HTTP/1.1 200 OK
Connection: keep-alive
Content-Length: 155
Content-Type: application/json; charset=utf-8
Date: Fri, 14 Jul 2017 19:54:47 GMT
ETag: W/"9b-/Cw9g9LnPK/vccqDh4CDbsKF6/g"
X-Powered-By: Express

{
    "__v": 0,
    "text": "Something to do from Postman",
    "_creator": "59691c802d821ba1557b73e7",
    "_id": "596921872d821ba1557b73ea",
    "completedAt": null,
    "completed": false
}
```

#### PATCH /todos/:id

Update an existed todo with `x-auth` token.

```
PATCH /todos/596921872d821ba1557b73ea HTTP/1.1
Content-Type: application/json
x-auth: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJfaWQiOiI1OTY5MWM4MDJkODIxYmExNTU3YjczZTciLCJhY2Nlc3MiOiJhdXRoIiwiaWF0IjoxNTAwMDYwODAwfQ.af2PQl2HMduHU3FeXFMjxTShO97l1QYAclvweh5lBsc

{
  "text": "Update something to do from Postman"
}
```

```
HTTP/1.1 200 OK
Connection: keep-alive
Content-Length: 171
Content-Type: application/json; charset=utf-8
Date: Fri, 14 Jul 2017 20:05:01 GMT
ETag: W/"ab-BNMBZIQUdHOHuFYjlMapv2Aln0g"
X-Powered-By: Express

{
    "todo": {
        "_id": "596921872d821ba1557b73ea",
        "text": "Update something to do from Postman",
        "_creator": "59691c802d821ba1557b73e7",
        "__v": 0,
        "completedAt": null,
        "completed": false
    }
}
```

#### DELETE /todos/:id

Delete an existed todo with `x-auth` token.

```
DELETE /todos/596921872d821ba1557b73ea HTTP/1.1
x-auth: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJfaWQiOiI1OTY5MWM4MDJkODIxYmExNTU3YjczZTciLCJhY2Nlc3MiOiJhdXRoIiwiaWF0IjoxNTAwMDYwODAwfQ.af2PQl2HMduHU3FeXFMjxTShO97l1QYAclvweh5lBsc
```

```
HTTP/1.1 200 OK
Connection: keep-alive
Content-Length: 171
Content-Type: application/json; charset=utf-8
Date: Fri, 14 Jul 2017 20:09:11 GMT
ETag: W/"ab-BNMBZIQUdHOHuFYjlMapv2Aln0g"
X-Powered-By: Express

{
    "todo": {
        "_id": "596921872d821ba1557b73ea",
        "text": "Update something to do from Postman",
        "_creator": "59691c802d821ba1557b73e7",
        "__v": 0,
        "completedAt": null,
        "completed": false
    }
}
```

### users

The following sections are all supported operations for users resource.

#### GET /users/me

Retrieve user information with `x-auth` token.

```
GET /users/me HTTP/1.1
x-auth: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJfaWQiOiI1OTY5MWM4MDJkODIxYmExNTU3YjczZTciLCJhY2Nlc3MiOiJhdXRoIiwiaWF0IjoxNTAwMDYxNDI2fQ.P7FAUrarx_DWHmNs68weR4Y27_5afuoeDztVRY_GDAg
```

```
HTTP/1.1 200 OK
Connection: keep-alive
Content-Length: 69
Content-Type: application/json; charset=utf-8
Date: Fri, 14 Jul 2017 19:46:50 GMT
ETag: W/"45-dUoPLW+UATlB6Fe/8Qblx7oi9CY"
X-Powered-By: Express

{
    "_id": "59691c802d821ba1557b73e7",
    "email": "tsoliangwu0130@gmail.com"
}
```

#### POST /users

Create a new user and login.

```
POST /users HTTP/1.1
Content-Type: application/json

{
  "email": "tsoliangwu0130@gmail.com",
  "password": "password!"
}
```

```
HTTP/1.1 200 OK
Connection: keep-alive
Content-Length: 69
Content-Type: application/json; charset=utf-8
Date: Fri, 14 Jul 2017 19:33:20 GMT
ETag: W/"45-dUoPLW+UATlB6Fe/8Qblx7oi9CY"
X-Powered-By: Express
x-auth: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJfaWQiOiI1OTY5MWM4MDJkODIxYmExNTU3YjczZTciLCJhY2Nlc3MiOiJhdXRoIiwiaWF0IjoxNTAwMDYwODAwfQ.af2PQl2HMduHU3FeXFMjxTShO97l1QYAclvweh5lBsc

{
    "_id": "59691c802d821ba1557b73e7",
    "email": "tsoliangwu0130@gmail.com"
}
```

#### POST /users/login

Login an existed user with email and password.

```
POST /users/login HTTP/1.1
Content-Type: application/json

{
  "email": "tsoliangwu0130@gmail.com",
  "password": "password!"
}
```

```
HTTP/1.1 200 OK
Connection: keep-alive
Content-Length: 69
Content-Type: application/json; charset=utf-8
Date: Fri, 14 Jul 2017 19:43:46 GMT
ETag: W/"45-dUoPLW+UATlB6Fe/8Qblx7oi9CY"
X-Powered-By: Express
x-auth: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJfaWQiOiI1OTY5MWM4MDJkODIxYmExNTU3YjczZTciLCJhY2Nlc3MiOiJhdXRoIiwiaWF0IjoxNTAwMDYxNDI2fQ.P7FAUrarx_DWHmNs68weR4Y27_5afuoeDztVRY_GDAg

{
    "_id": "59691c802d821ba1557b73e7",
    "email": "tsoliangwu0130@gmail.com"
}
```

#### DELETE /users/me/token

Log out the current user with `x-auth` token.

```
DELETE /users/me/token HTTP/1.1
x-auth: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJfaWQiOiI1OTY5MWM4MDJkODIxYmExNTU3YjczZTciLCJhY2Nlc3MiOiJhdXRoIiwiaWF0IjoxNTAwMDYxNDI2fQ.P7FAUrarx_DWHmNs68weR4Y27_5afuoeDztVRY_GDAg
```

```
HTTP/1.1 200 OK
Connection: keep-alive
Content-Length: 0
Date: Fri, 14 Jul 2017 19:50:57 GMT
X-Powered-By: Express
```
