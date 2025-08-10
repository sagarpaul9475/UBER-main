# User Registration Endpoint Documentation

## POST `/user/register`

### Description

Registers a new user in the system. This endpoint expects user details in the request body and returns an authentication token upon successful registration.

### Request Body

The request body must be a JSON object with the following structure:

```json
{
  "fullname": {
    "firstname": "string (min 3 chars, required)",
    "lastname": "string (optional, min 3 chars if provided)"
  },
  "email": "string (valid email, required)",
  "password": "string (min 6 chars, required)"
}
```

#### Example

```json
{
  "fullname": {
    "firstname": "John",
    "lastname": "Doe"
  },
  "email": "john.doe@example.com",
  "password": "securePassword123"
}
```

### Responses

- **201 Created**
  - **Description:** User registered successfully.
  - **Body:**
    ```json
    {
      "token": "jwt_token_string",
      "user": { /* user object */ }
    }
    ```

- **400 Bad Request**
  - **Description:** Validation failed (e.g., missing fields, invalid email, short password).
  - **Body:**
    ```json
    {
      "errors": [
        {
          "msg": "Error message",
          "param": "field",
          "location": "body"
        }
      ]
    }
    ```

- **500 Internal Server Error**
  - **Description:** Unexpected server error.

### Notes

- All required fields must be provided as specified.
- The `firstname`, `email`, and `password` fields are mandatory.
- The `lastname` field is optional but must be at least 3 characters if provided.
- The endpoint returns a JWT token for authentication upon successful registration.
