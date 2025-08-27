# API Documentation

This section contains documentation for all public APIs.

## REST API Documentation

### Authentication

All API endpoints require authentication unless otherwise specified.

#### Authentication Methods

1. **API Key Authentication**
   ```http
   Authorization: Bearer YOUR_API_KEY
   ```

2. **OAuth 2.0**
   ```http
   Authorization: Bearer YOUR_ACCESS_TOKEN
   ```

### Base URL

```
https://api.example.com/v1
```

### Response Format

All responses follow this structure:

```json
{
  "success": true,
  "data": {},
  "message": "Success message",
  "timestamp": "2024-01-01T00:00:00Z"
}
```

### Error Handling

Error responses follow this format:

```json
{
  "success": false,
  "error": {
    "code": "ERROR_CODE",
    "message": "Human readable error message",
    "details": {}
  },
  "timestamp": "2024-01-01T00:00:00Z"
}
```

### Common HTTP Status Codes

| Code | Description |
|------|-------------|
| 200  | Success |
| 201  | Created |
| 400  | Bad Request |
| 401  | Unauthorized |
| 403  | Forbidden |
| 404  | Not Found |
| 429  | Rate Limited |
| 500  | Internal Server Error |

## API Endpoints

### Users API

#### GET /users

Retrieve a list of users.

**Parameters:**
- `page` (integer, optional): Page number (default: 1)
- `limit` (integer, optional): Items per page (default: 20, max: 100)
- `search` (string, optional): Search term for filtering users

**Example Request:**
```http
GET /users?page=1&limit=10&search=john
Authorization: Bearer YOUR_API_KEY
```

**Example Response:**
```json
{
  "success": true,
  "data": {
    "users": [
      {
        "id": 1,
        "username": "john_doe",
        "email": "john@example.com",
        "created_at": "2024-01-01T00:00:00Z",
        "updated_at": "2024-01-01T00:00:00Z"
      }
    ],
    "pagination": {
      "current_page": 1,
      "per_page": 10,
      "total": 1,
      "total_pages": 1
    }
  },
  "message": "Users retrieved successfully",
  "timestamp": "2024-01-01T00:00:00Z"
}
```

#### POST /users

Create a new user.

**Request Body:**
```json
{
  "username": "string (required, 3-50 characters)",
  "email": "string (required, valid email)",
  "password": "string (required, min 8 characters)",
  "first_name": "string (optional)",
  "last_name": "string (optional)"
}
```

**Example Request:**
```http
POST /users
Content-Type: application/json
Authorization: Bearer YOUR_API_KEY

{
  "username": "jane_doe",
  "email": "jane@example.com",
  "password": "securepassword123",
  "first_name": "Jane",
  "last_name": "Doe"
}
```

**Example Response:**
```json
{
  "success": true,
  "data": {
    "user": {
      "id": 2,
      "username": "jane_doe",
      "email": "jane@example.com",
      "first_name": "Jane",
      "last_name": "Doe",
      "created_at": "2024-01-01T00:00:00Z",
      "updated_at": "2024-01-01T00:00:00Z"
    }
  },
  "message": "User created successfully",
  "timestamp": "2024-01-01T00:00:00Z"
}
```

#### GET /users/{id}

Retrieve a specific user by ID.

**Parameters:**
- `id` (integer, required): User ID

**Example Request:**
```http
GET /users/1
Authorization: Bearer YOUR_API_KEY
```

**Example Response:**
```json
{
  "success": true,
  "data": {
    "user": {
      "id": 1,
      "username": "john_doe",
      "email": "john@example.com",
      "first_name": "John",
      "last_name": "Doe",
      "created_at": "2024-01-01T00:00:00Z",
      "updated_at": "2024-01-01T00:00:00Z"
    }
  },
  "message": "User retrieved successfully",
  "timestamp": "2024-01-01T00:00:00Z"
}
```

#### PUT /users/{id}

Update a specific user.

**Parameters:**
- `id` (integer, required): User ID

**Request Body:**
```json
{
  "username": "string (optional, 3-50 characters)",
  "email": "string (optional, valid email)",
  "first_name": "string (optional)",
  "last_name": "string (optional)"
}
```

**Example Request:**
```http
PUT /users/1
Content-Type: application/json
Authorization: Bearer YOUR_API_KEY

{
  "first_name": "Johnny",
  "last_name": "Doe"
}
```

#### DELETE /users/{id}

Delete a specific user.

**Parameters:**
- `id` (integer, required): User ID

**Example Request:**
```http
DELETE /users/1
Authorization: Bearer YOUR_API_KEY
```

**Example Response:**
```json
{
  "success": true,
  "data": null,
  "message": "User deleted successfully",
  "timestamp": "2024-01-01T00:00:00Z"
}
```

### Posts API

#### GET /posts

Retrieve a list of posts.

**Parameters:**
- `page` (integer, optional): Page number (default: 1)
- `limit` (integer, optional): Items per page (default: 20, max: 100)
- `user_id` (integer, optional): Filter by user ID
- `category` (string, optional): Filter by category
- `published` (boolean, optional): Filter by published status

**Example Request:**
```http
GET /posts?user_id=1&published=true&page=1&limit=5
Authorization: Bearer YOUR_API_KEY
```

#### POST /posts

Create a new post.

**Request Body:**
```json
{
  "title": "string (required, max 255 characters)",
  "content": "string (required)",
  "category": "string (optional)",
  "published": "boolean (optional, default: false)",
  "tags": "array of strings (optional)"
}
```

**Example Request:**
```http
POST /posts
Content-Type: application/json
Authorization: Bearer YOUR_API_KEY

{
  "title": "My First Blog Post",
  "content": "This is the content of my first blog post...",
  "category": "technology",
  "published": true,
  "tags": ["tech", "programming", "api"]
}
```

## Rate Limiting

API requests are rate limited to prevent abuse:

- **Authenticated requests**: 1000 requests per hour
- **Unauthenticated requests**: 100 requests per hour

Rate limit information is included in response headers:

```http
X-RateLimit-Limit: 1000
X-RateLimit-Remaining: 999
X-RateLimit-Reset: 1640995200
```

## SDKs and Libraries

### JavaScript/Node.js

```javascript
npm install @example/api-client
```

```javascript
const ApiClient = require('@example/api-client');

const client = new ApiClient({
  apiKey: 'your-api-key',
  baseUrl: 'https://api.example.com/v1'
});

// Get users
const users = await client.users.list({ page: 1, limit: 10 });

// Create user
const newUser = await client.users.create({
  username: 'john_doe',
  email: 'john@example.com',
  password: 'password123'
});
```

### Python

```bash
pip install example-api-client
```

```python
from example_api import ApiClient

client = ApiClient(api_key='your-api-key')

# Get users
users = client.users.list(page=1, limit=10)

# Create user
new_user = client.users.create(
    username='john_doe',
    email='john@example.com',
    password='password123'
)
```

## Webhooks

Configure webhooks to receive real-time notifications about events.

### Webhook Events

- `user.created` - Triggered when a new user is created
- `user.updated` - Triggered when a user is updated
- `user.deleted` - Triggered when a user is deleted
- `post.created` - Triggered when a new post is created
- `post.published` - Triggered when a post is published

### Webhook Payload

```json
{
  "event": "user.created",
  "data": {
    "user": {
      "id": 1,
      "username": "john_doe",
      "email": "john@example.com"
    }
  },
  "timestamp": "2024-01-01T00:00:00Z"
}
```

### Webhook Security

All webhook payloads are signed with HMAC-SHA256. Verify the signature using the `X-Webhook-Signature` header.

```javascript
const crypto = require('crypto');

function verifyWebhookSignature(payload, signature, secret) {
  const expectedSignature = crypto
    .createHmac('sha256', secret)
    .update(payload)
    .digest('hex');
  
  return crypto.timingSafeEqual(
    Buffer.from(signature),
    Buffer.from(`sha256=${expectedSignature}`)
  );
}
```