# TODO App - REST API Documentation
RESTful API Designed in Node.js for a very simple TODO application.

## Index
* [Requirements](#requirements)
* [Installation](#installation)
* [Schema](#schema)
* [Authentication](#authentication)
* [Root End-Point](#root-end-point)
* [Core Resources](#core-resources)
* [Documentation](#documentation)
* [Request & Response Examples](#request--response-examples)

## Requirements

- [node & npm](http://nodejs.org)
- [MongoDB](https://www.mongodb.com/): Make sure you have your own local or remote MongoDB database URI configured in `credentials/mongo.js`
- [PostMan](https://www.getpostman.com/)

## Installation

1. Clone the repository: `git clone git@github.com:toslimarif/todo-api.git`
2. Install the application: `npm install`
3. Place your own MongoDB URI in `credentials/mongo.js`
3. Start the server: `npm start`
4. Open PostMan and make a `GET` request to `http://localhost:3000/api/info/`

## Schema

1. All API access is over HTTP, and accessed from `http://localhost:3000/api/v1`.
2. All data is sent and received as JSON.
3. Blank fields are included as `null` instead of being omitted.
4. All timestamps return in ISO 8601 format: `YYYY-MM-DDTHH:MM:SSZ`

## Authentication
There are no authentication implemented yet. So, all the end-points are open.

## Root End-Point
`http://localhost:3000/api/v1`

## Core Resources
### Todo
`Todo` object represents snapshot of a specific Todo with a unique Id. You can retrieve it to see details about the Todo.

#### Schema
```javascript
{
    title: {
        type: String,
        required: true
    },
    description: {
        type: String,
        required: true,
        default: 'N/A'
    },
    isCompleted: {
        type: Boolean,
        required: true,
        default: false
    },
}
```
#### End-Points
| Method | End-Point | Description |
| --- | --- | --- |
| `GET` | `/todo` | List all *todos* |
| `POST` | `/todo` | Create a new *todo* |
| `GET` | `/todo/:id` | Fetch a specific *todo* |
| `PUT` | `/todo/:id` | Edit existing *todo* |
| `PATCH` | `/todo/:id` | Mark an existing *todo* as complete |
| `DELETE` | `/todo/:id` | Delete existing *todo* |

## Documentation
https://documenter.getpostman.com/view/8474302/SVfGyBSu

## Request & Response Examples

### API Resources
  - [GET /todo](#get-todo)
  - [GET /todo/:todoId](#get-todotodoId)
  - [POST /todo](#post-todo)
  - [PUT /todo/:todoId](#put-todotodoId)
  - [PATCH /todo/:todoId](#patch-todotodoId)
  - [DELETE /todo/:todoId](#delete-todotodoId)

### GET /todo
To get the list of all *todos*
#### Resourse Url
`http://localhost:3000/api/v1/todo`
#### Request Params
`N/A`
#### Request Body
`N/A`
#### Response
```javascript
{
  "status": "Success",
  "message": "Todos Fetched Successfully!",
  "todos": [
    {
      "description": "This task is about starting to do some really interesting stuff!",
      "isCompleted": true,
      "_id": "676b25d58e87e30e2f544625",
      "title": "New test tasks",
      "__v": 0
    },
    {
      "description": "Desc 2",
      "isCompleted": false,
      "_id": "6769d78ce9c1293a2bfa7006",
      "title": "Task 2",
      "onDate": "2024-12-23T21:35:08.703Z",
      "__v": 0
    }
  ],
  "todoCount": 2
}
```

### GET /todo/:todoId
To get a specific *todo*
#### Resourse Url
`http://localhost:3000/api/v1/todo/{{TODO_ID}}`
#### Request Params
`{{TODO_ID}}`
#### Request Body
`N/A`
#### Response
```javascript
{
    "status": "Success",
    "message": "Todo Fetched Successfully!",
    "todo": {
        "description": "Write documentation for Todo API",
        "isCompleted": false,
        "_id": "5d56e2bbc2a36326a0a57c19",
        "title": "Write Documentation",
        "__v": 0
    }
}
```

### POST /todo
To create a new *todo*
#### Resourse Url
`http://localhost:3000/api/v1/todo`
#### Request Params
`N/A`
#### Request Body
```javascript
{
    "title": "Write Test-Cases",
    "description": "Write Test-Cases for Todo API",
}
```
#### Response
```javascript
{
    "status": "Success",
    "message": "Todo Created SuccessFully!",
    "todo": {
        "description": "Write Test-Cases for Todo API",
        "isCompleted": false,
        "_id": "5d56e320c2a36326a0a57c1a",
        "title": "Write Test-Cases",
        "__v": 0,
        "todoId": "5d56e320c2a36326a0a57c1a"
    }
}
```

### PUT /todo/:todoId
To edit an existing *todo*
#### Resourse Url
`http://localhost:3000/api/v1/todo/{{TODO_ID}}`
#### Request Params
`{{TODO_ID}}`
#### Request Body
```javascript
{
    "title": "UPDATED: Write Documentation",
    "description": "UPDATED: Write documentation for Todo API"
}
```
#### Response
```javascript
{
    "status": "Success",
    "message": "Todo Updated Successfully!",
    "todo": {
        "description": "UPDATED: Write documentation for Todo API",
        "isCompleted": true,
        "_id": "5d56e2bbc2a36326a0a57c19",
        "title": "UPDATED: Write Documentation",
        "__v": 0
    }
}
```
### PATCH /todo/:todoId
To mark a *todo* as Complete
#### Resourse Url
`http://localhost:3000/api/v1/todo/{{TODO_ID}}`
#### Request Params
`{{TODO_ID}}`
#### Request Body
`N/A`
#### Response
```javascript
{
    "status": "Success",
    "message": "Todo Marked as Completed!",
    "todo": {
        "description": "Write documentation for Todo API",
        "isCompleted": true,
        "_id": "5d56e2bbc2a36326a0a57c19",
        "title": "Write Documentation",
        "__v": 0
    }
}
```

### DELETE /todo/:todoId
To delete an existing *todo*
#### Resourse Url
`http://localhost:3000/api/v1/todo/{{TODO_ID}}`
#### Request Params
`{{TODO_ID}}`
#### Request Body
`N/A`
#### Response
```javascript
{
    "status": "Success",
    "message": "Todo Deleted Successfully!"
}
```
