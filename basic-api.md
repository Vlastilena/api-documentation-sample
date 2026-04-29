# Basic REST API Documentation Sample

## Overview

This is a simple REST API example demonstrating basic CRUD operations and core REST concepts.

It is intended as a foundational API documentation sample for technical writing practice.

---

## Base URL

https://api.example.com/v1

---

## Authentication

All requests require Bearer token authentication.

Authorization: Bearer <access_token>

---

## GET /users

Returns a list of users.

### Response (200 OK)

```json
[
  {
    "id": 1,
    "name": "Firstname Lastname",
    "email": "Firstname@example.com"
  }
]
```

---

### Errors

- 401 Unauthorized – missing or invalid authentication token  
- 500 Internal Server Error – unexpected server failure  

---

## POST /users

Creates a new user.

### Request Body

{
  "name": "Firstname Lastname",
  "email": "Firstname@example.com"
}

---

### Response (201 Created)

{
  "id": 1,
  "name": "Firstname Lastname",
  "email": "Firstname@example.com"
}

---

### Errors

- 400 Bad Request – invalid input data  
- 409 Conflict – user already exists  
