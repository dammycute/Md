# Define the content for the API Design Markdown file
api_design_content = """
# API Design Document for Greenhouse Product Store Web App

## Table of Contents
1. [Introduction](#introduction)
2. [Authentication and Authorization](#authentication-and-authorization)
3. [Endpoints](#endpoints)
   - [User Endpoints](#user-endpoints)
   - [Product Endpoints](#product-endpoints)
   - [Order Endpoints](#order-endpoints)
4. [Error Handling](#error-handling)
5. [Rate Limiting](#rate-limiting)
6. [Security](#security)
7. [Versioning](#versioning)
8. [Documentation](#documentation)

## Introduction
This document outlines the API design for the Greenhouse Product Store Web App. The API allows users to interact with the system, enabling functionalities such as user registration, product browsing, order creation, and order tracking.

## Authentication and Authorization
- **Authentication**: JSON Web Tokens (JWT) will be used for authentication. Users must include a valid token in the `Authorization` header for protected routes.
- **Authorization**: Role-based access control (RBAC) will be implemented to ensure that only users with the appropriate roles can access certain endpoints.

## Endpoints

### User Endpoints
#### Register
- **URL**: `/api/register`
- **Method**: `POST`
- **Request Body**:
  ```json
  {
    "username": "string",
    "email": "string",
    "password": "string"
  }
  ```
- **Response**:
  ```json
  {
    "message": "User registered successfully",
    "user": {
      "id": "integer",
      "username": "string",
      "email": "string"
    }
  }
  ```

#### Login
- **URL**: `/api/login`
- **Method**: `POST`
- **Request Body**:
  ```json
  {
    "email": "string",
    "password": "string"
  }
  ```
- **Response**:
  ```json
  {
    "token": "string"
  }
  ```

#### Get User Details
- **URL**: `/api/users/me`
- **Method**: `GET`
- **Headers**:
  - `Authorization`: `Bearer <token>`
- **Response**:
  ```json
  {
    "id": "integer",
    "username": "string",
    "email": "string"
  }
  ```

### Product Endpoints
#### Get All Products
- **URL**: `/api/products`
- **Method**: `GET`
- **Response**:
  ```json
  [
    {
      "id": "integer",
      "name": "string",
      "description": "string",
      "price": "number",
      "stock": "integer"
    }
  ]
  ```

#### Get Product Details
- **URL**: `/api/products/:id`
- **Method**: `GET`
- **Response**:
  ```json
  {
    "id": "integer",
    "name": "string",
    "description": "string",
    "price": "number",
    "stock": "integer"
  }
  ```

### Order Endpoints
#### Create Order
- **URL**: `/api/orders`
- **Method**: `POST`
- **Headers**:
  - `Authorization`: `Bearer <token>`
- **Request Body**:
  ```json
  {
    "items": [
      {
        "product_id": "integer",
        "quantity": "integer"
      }
    ]
  }
  ```
- **Response**:
  ```json
  {
    "order_id": "integer",
    "status": "string",
    "total_price": "number"
  }
  ```

#### Get Order Details
- **URL**: `/api/orders/:id`
- **Method**: `GET`
- **Headers**:
  - `Authorization`: `Bearer <token>`
- **Response**:
  ```json
  {
    "id": "integer",
    "user_id": "integer",
    "total_price": "number",
    "status": "string",
    "items": [
      {
        "product_id": "integer",
        "quantity": "integer",
        "price": "number"
      }
    ],
    "created_at": "string",
    "updated_at": "string"
  }
  ```

#### Update Order Status
- **URL**: `/api/orders/:id`
- **Method**: `PUT`
- **Headers**:
  - `Authorization`: `Bearer <token>`
- **Request Body**:
  ```json
  {
    "status": "string"
  }
  ```
- **Response**:
  ```json
  {
    "message": "Order status updated",
    "order": {
      "id": "integer",
      "status": "string"
    }
  }
  ```

## Error Handling
- **Error Format**:
  ```json
  {
    "error": {
      "message": "string",
      "code": "integer"
    }
  }
  ```
- **Common Errors**:
  - `400 Bad Request`: Invalid input data
  - `401 Unauthorized`: Authentication required
  - `403 Forbidden`: Access denied
  - `404 Not Found`: Resource not found
  - `500 Internal Server Error`: Server error

## Rate Limiting
- Implement rate limiting to prevent abuse of the API endpoints. For example, limit the number of requests per minute for each IP address.

## Security
- Use HTTPS for all endpoints to ensure secure data transmission.
- Validate all input data to prevent SQL injection and other attacks.
- Use JWT for secure authentication and authorization.

## Versioning
- Use URL versioning (e.g., `/api/v1/products`) to manage different versions of the API.

## Documentation
- Use tools like Swagger or Postman to create and maintain API documentation. Ensure the documentation is up-to-date and accessible to developers.
"""

# Write the content to a Markdown file
api_design_file_path = "/mnt/data/greenhouse_product_store_api_design.md"
with open(api_design_file_path, "w") as file:
    file.write(api_design_content)

api_design_file_path
