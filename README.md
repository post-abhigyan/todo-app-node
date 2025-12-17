# Todo App - Node.js Backend

A simple RESTful API backend for a todo application built with Node.js and Express.js.

## Features

- Create, Read, Update, and Delete (CRUD) operations for todos
- In-memory data storage
- RESTful API design
- JSON response format
- Error handling
- CORS enabled

## Prerequisites

- Node.js (v12 or higher)
- npm

## Installation

1. Clone the repository:
```bash
git clone <repository-url>
cd todo-app-node
```

2. Install dependencies:
```bash
npm install
```

3. Start the server:
```bash
npm start
```

The server will start on `http://localhost:3000` by default.

## API Endpoints

### Root Endpoint
- **GET /** - Get API information

### Todo Endpoints

#### Get All Todos
- **URL:** `/todos`
- **Method:** `GET`
- **Success Response:** 
  - **Code:** 200
  - **Content:** 
    ```json
    {
      "success": true,
      "data": [
        {
          "id": 1,
          "title": "Sample Todo",
          "description": "This is a sample todo",
          "completed": false,
          "createdAt": "2025-12-17T05:00:00.000Z"
        }
      ]
    }
    ```

#### Get Specific Todo
- **URL:** `/todos/:id`
- **Method:** `GET`
- **URL Parameters:** `id=[integer]`
- **Success Response:** 
  - **Code:** 200
  - **Content:** 
    ```json
    {
      "success": true,
      "data": {
        "id": 1,
        "title": "Sample Todo",
        "description": "This is a sample todo",
        "completed": false,
        "createdAt": "2025-12-17T05:00:00.000Z"
      }
    }
    ```
- **Error Response:**
  - **Code:** 404
  - **Content:** `{ "success": false, "error": "Todo not found" }`

#### Create Todo
- **URL:** `/todos`
- **Method:** `POST`
- **Body:**
  ```json
  {
    "title": "New Todo",
    "description": "Optional description"
  }
  ```
- **Success Response:** 
  - **Code:** 201
  - **Content:** 
    ```json
    {
      "success": true,
      "data": {
        "id": 2,
        "title": "New Todo",
        "description": "Optional description",
        "completed": false,
        "createdAt": "2025-12-17T05:00:00.000Z"
      }
    }
    ```
- **Error Response:**
  - **Code:** 400
  - **Content:** `{ "success": false, "error": "Title is required" }`

#### Update Todo
- **URL:** `/todos/:id`
- **Method:** `PUT`
- **URL Parameters:** `id=[integer]`
- **Body:**
  ```json
  {
    "title": "Updated Todo",
    "description": "Updated description",
    "completed": true
  }
  ```
  Note: All fields are optional. Only provided fields will be updated.
- **Success Response:** 
  - **Code:** 200
  - **Content:** 
    ```json
    {
      "success": true,
      "data": {
        "id": 1,
        "title": "Updated Todo",
        "description": "Updated description",
        "completed": true,
        "createdAt": "2025-12-17T05:00:00.000Z",
        "updatedAt": "2025-12-17T06:00:00.000Z"
      }
    }
    ```
- **Error Response:**
  - **Code:** 404
  - **Content:** `{ "success": false, "error": "Todo not found" }`
  - **Code:** 400
  - **Content:** `{ "success": false, "error": "Title cannot be empty" }`

#### Delete Todo
- **URL:** `/todos/:id`
- **Method:** `DELETE`
- **URL Parameters:** `id=[integer]`
- **Success Response:** 
  - **Code:** 200
  - **Content:** 
    ```json
    {
      "success": true,
      "data": {
        "id": 1,
        "title": "Deleted Todo",
        "description": "This todo was deleted",
        "completed": false,
        "createdAt": "2025-12-17T05:00:00.000Z"
      }
    }
    ```
- **Error Response:**
  - **Code:** 404
  - **Content:** `{ "success": false, "error": "Todo not found" }`

## Example Usage with cURL

### Create a todo:
```bash
curl -X POST http://localhost:3000/todos \
  -H "Content-Type: application/json" \
  -d '{"title":"Buy groceries","description":"Milk, eggs, bread"}'
```

### Get all todos:
```bash
curl http://localhost:3000/todos
```

### Get a specific todo:
```bash
curl http://localhost:3000/todos/1
```

### Update a todo:
```bash
curl -X PUT http://localhost:3000/todos/1 \
  -H "Content-Type: application/json" \
  -d '{"completed":true}'
```

### Delete a todo:
```bash
curl -X DELETE http://localhost:3000/todos/1
```

## Data Model

### Todo Object
```javascript
{
  id: Number,          // Unique identifier (auto-generated)
  title: String,       // Todo title (required)
  description: String, // Todo description (optional)
  completed: Boolean,  // Completion status (default: false)
  createdAt: String,   // ISO timestamp of creation
  updatedAt: String    // ISO timestamp of last update (optional)
}
```

## Technical Details

- **Framework:** Express.js
- **Data Storage:** In-memory (data is lost on server restart)
- **Default Port:** 3000 (configurable via PORT environment variable)
- **Response Format:** JSON

## License

ISC