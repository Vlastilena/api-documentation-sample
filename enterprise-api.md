# Enterprise Headless CMS API Documentation Sample

## Overview

This is an enterprise-style REST API documentation sample inspired by headless CMS and composable content platforms.

It demonstrates advanced API design concepts used in scalable enterprise systems.

Key features include:
- Content modeling
- Versioning and publishing workflow
- Role-based access control (RBAC)
- Standardized response structure
- RESTful architecture patterns

---

## Base URL

https://api.example.com/v1

---

## Authentication

All requests require Bearer token authentication.

Authorization: Bearer <access_token>  
Content-Type: application/json  
Accept: application/json  

---

## Content Model

A content item represents a structured entity in the CMS.

Fields:
- id – unique identifier
- title – content title
- body – main content
- status – draft | published
- version – content version

---

## GET /content-items

Returns a list of content items.

### Query Parameters

- status (string) – filter by draft or published  
- page (int) – page number  
- limit (int) – items per page  

---

### Response (200 OK)

```json
{
  "data": [
    {
      "id": "101",
      "title": "Welcome Page",
      "status": "published",
      "version": 3
    }
  ],
  "meta": {
    "page": 1,
    "limit": 20,
    "total": 42
  }
}
```

---

### Errors

- 401 Unauthorized – invalid or missing token  
- 403 Forbidden – insufficient permissions  
- 500 Internal Server Error – unexpected server failure  

---

## POST /content-items

Creates a new content item in draft state.

### Request Body

```json
{
  "title": "New Article",
  "body": "Content goes here",
  "status": "draft"
}
```

---

### Response (201 Created)

```json
{
  "id": "102",
  "title": "New Article",
  "status": "draft",
  "version": 1
}
```

---

## POST /content-items/{id}/publish

Publishes a content item and creates a new immutable version.

### Behavior
- Changes status to published
- Increments version
- Makes content available via delivery API

---

### Response (200 OK)

```json
{
  "id": "102",
  "status": "published",
  "version": 2
}
```

---

## Roles & Permissions

- Author → create and edit drafts  
- Editor → review and approve content  
- Publisher → publish content  

Access to endpoints depends on assigned role.

---

## Error Model

All errors follow a consistent structure:

```json
{
  "error": {
    "code": "FORBIDDEN",
    "message": "You do not have permission to perform this action"
  }
}
```
