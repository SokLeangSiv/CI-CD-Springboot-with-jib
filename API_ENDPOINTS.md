# Testing Bro - API Endpoints

Base URL: `http://localhost:8080`

## Health & System Endpoints

### 1. Health Check
**GET** `/api/health`

Returns the health status of the application.

**Response:**
```json
{
  "status": "UP",
  "timestamp": "2026-02-21T10:30:00",
  "service": "testing-bro",
  "version": "1.0.0"
}
```

### 2. Ping
**GET** `/api/ping`

Simple ping endpoint.

**Response:**
```
pong
```

---

## Test Endpoints (For Testing Various HTTP Methods)

### 3. Hello
**GET** `/api/test/hello?name=John`

**Query Parameters:**
- `name` (optional, default: "World")

**Response:**
```json
{
  "message": "Hello, John!"
}
```

### 4. Echo
**GET** `/api/test/echo/{message}`

**Path Parameters:**
- `message` - Any string to echo back

**Example:** `GET /api/test/echo/HelloWorld`

**Response:**
```json
{
  "echo": "HelloWorld"
}
```

### 5. Create Test Data
**POST** `/api/test/create`

**Request Body:**
```json
{
  "key1": "value1",
  "key2": "value2"
}
```

**Response:**
```json
{
  "id": "550e8400-e29b-41d4-a716-446655440000",
  "data": {
    "key1": "value1",
    "key2": "value2"
  },
  "status": "created"
}
```

### 6. Update Test Data
**PUT** `/api/test/update/{id}`

**Path Parameters:**
- `id` - ID of the item to update

**Request Body:**
```json
{
  "key1": "updated_value"
}
```

**Response:**
```json
{
  "id": "123",
  "data": {
    "key1": "updated_value"
  },
  "status": "updated"
}
```

### 7. Delete Test Data
**DELETE** `/api/test/delete/{id}`

**Path Parameters:**
- `id` - ID of the item to delete

**Response:**
```json
{
  "id": "123",
  "status": "deleted"
}
```

### 8. Get Headers
**GET** `/api/test/headers`

Returns all request headers.

**Response:**
```json
{
  "user-agent": "PostmanRuntime/7.26.8",
  "accept": "*/*",
  "host": "localhost:8080"
}
```

### 9. Query Parameters Test
**GET** `/api/test/query?search=test&limit=20&offset=10`

**Query Parameters:**
- `search` (optional)
- `limit` (optional, default: 10)
- `offset` (optional, default: 0)

**Response:**
```json
{
  "search": "test",
  "limit": 20,
  "offset": 10
}
```

---

## User Management Endpoints (CRUD with Database)

### 10. Get All Users
**GET** `/api/users`

**Response:**
```json
[
  {
    "id": 1,
    "name": "John Doe",
    "email": "john@example.com",
    "createdAt": "2026-02-21T10:00:00"
  }
]
```

### 11. Get User by ID
**GET** `/api/users/{id}`

**Path Parameters:**
- `id` - User ID

**Response:**
```json
{
  "id": 1,
  "name": "John Doe",
  "email": "john@example.com",
  "createdAt": "2026-02-21T10:00:00"
}
```

### 12. Create User
**POST** `/api/users`

**Request Body:**
```json
{
  "name": "Jane Smith",
  "email": "jane@example.com"
}
```

**Response:**
```json
{
  "id": 2,
  "name": "Jane Smith",
  "email": "jane@example.com",
  "createdAt": "2026-02-21T10:30:00"
}
```

### 13. Update User
**PUT** `/api/users/{id}`

**Path Parameters:**
- `id` - User ID

**Request Body:**
```json
{
  "name": "Jane Updated",
  "email": "jane.updated@example.com"
}
```

**Response:**
```json
{
  "id": 2,
  "name": "Jane Updated",
  "email": "jane.updated@example.com",
  "createdAt": "2026-02-21T10:30:00"
}
```

### 14. Delete User
**DELETE** `/api/users/{id}`

**Path Parameters:**
- `id` - User ID

**Response:**
```json
{
  "message": "User deleted successfully",
  "id": "2"
}
```

---

## How to Run

1. Make sure PostgreSQL database is running
2. Set environment variables in `.env` file:
   ```
   DB_URL=jdbc:postgresql://your-host/your-database
   DB_USERNAME=your-username
   DB_PASSWORD=your-password
   ```

3. Run the application:
   ```bash
   ./mvnw spring-boot:run
   ```

4. Application will start on `http://localhost:8080`

## Testing with cURL

```bash
# Health check
curl http://localhost:8080/api/health

# Ping
curl http://localhost:8080/api/ping

# Create a user
curl -X POST http://localhost:8080/api/users \
  -H "Content-Type: application/json" \
  -d '{"name":"John Doe","email":"john@example.com"}'

# Get all users
curl http://localhost:8080/api/users

# Test echo
curl http://localhost:8080/api/test/echo/hello

# Test with query params
curl "http://localhost:8080/api/test/hello?name=Developer"
```

## Testing with Postman

Import these endpoints into Postman or use the examples above to test each endpoint.
