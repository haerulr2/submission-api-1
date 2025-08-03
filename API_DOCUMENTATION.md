# API Documentation

Detailed documentation for the Bookshelf API endpoints, request/response formats, and examples.

## Base URL

```
http://localhost:9000
```

## Authentication

Currently, this API does not require authentication. All endpoints are publicly accessible.

## Content-Type

All requests should use:
```
Content-Type: application/json
```

## Endpoints

### 1. Add Book

Creates a new book in the collection.

**Endpoint:** `POST /books`

**Request Body:**
```json
{
  "name": "The Great Gatsby",
  "year": 1925,
  "author": "F. Scott Fitzgerald",
  "summary": "A story of the fabulously wealthy Jay Gatsby and his love for the beautiful Daisy Buchanan.",
  "publisher": "Scribner",
  "pageCount": 180,
  "readPage": 0,
  "reading": false
}
```

**Required Fields:**
- `name` (string): Book title

**Optional Fields:**
- `year` (number): Publication year
- `author` (string): Author name
- `summary` (string): Book summary
- `publisher` (string): Publisher name
- `pageCount` (number): Total number of pages
- `readPage` (number): Number of pages read
- `reading` (boolean): Reading status

**Success Response (201):**
```json
{
  "status": "success",
  "message": "Buku berhasil ditambahkan",
  "data": {
    "bookId": "unique-book-id"
  }
}
```

**Error Response (400):**
```json
{
  "status": "fail",
  "message": "Gagal menambahkan buku. Mohon isi nama buku"
}
```

**Validation Rules:**
- `name` is required
- `readPage` cannot be greater than `pageCount`

---

### 2. Get All Books

Retrieves all books with optional filtering.

**Endpoint:** `GET /books`

**Query Parameters:**
- `name` (optional): Filter by book name (case-insensitive)
- `reading` (optional): Filter by reading status (0 or 1)
- `finished` (optional): Filter by finished status (0 or 1)

**Examples:**
```
GET /books
GET /books?name=gatsby
GET /books?reading=1
GET /books?finished=0
GET /books?name=gatsby&reading=1&finished=0
```

**Success Response (200):**
```json
{
  "status": "success",
  "data": {
    "books": [
      {
        "id": "book-id-1",
        "name": "The Great Gatsby",
        "year": 1925,
        "author": "F. Scott Fitzgerald",
        "summary": "A story of the fabulously wealthy Jay Gatsby...",
        "publisher": "Scribner",
        "pageCount": 180,
        "readPage": 0,
        "finished": false,
        "reading": false,
        "insertedAt": "2023-01-01T00:00:00.000Z",
        "updatedAt": "2023-01-01T00:00:00.000Z"
      }
    ]
  }
}
```

---

### 3. Get Book by ID

Retrieves a specific book by its ID.

**Endpoint:** `GET /books/{id}`

**Path Parameters:**
- `id` (string): Book ID

**Example:**
```
GET /books/book-id-1
```

**Success Response (200):**
```json
{
  "status": "success",
  "data": {
    "book": {
      "id": "book-id-1",
      "name": "The Great Gatsby",
      "year": 1925,
      "author": "F. Scott Fitzgerald",
      "summary": "A story of the fabulously wealthy Jay Gatsby...",
      "publisher": "Scribner",
      "pageCount": 180,
      "readPage": 0,
      "finished": false,
      "reading": false,
      "insertedAt": "2023-01-01T00:00:00.000Z",
      "updatedAt": "2023-01-01T00:00:00.000Z"
    }
  }
}
```

**Error Response (404):**
```json
{
  "status": "fail",
  "message": "Buku tidak ditemukan"
}
```

---

### 4. Update Book

Updates an existing book by ID.

**Endpoint:** `PUT /books/{id}`

**Path Parameters:**
- `id` (string): Book ID

**Request Body:** Same as Add Book

**Example:**
```json
PUT /books/book-id-1
{
  "name": "The Great Gatsby (Updated)",
  "year": 1925,
  "author": "F. Scott Fitzgerald",
  "summary": "Updated summary...",
  "publisher": "Scribner",
  "pageCount": 180,
  "readPage": 90,
  "reading": true
}
```

**Success Response (200):**
```json
{
  "status": "success",
  "message": "Buku berhasil diperbarui"
}
```

**Error Response (404):**
```json
{
  "status": "fail",
  "message": "Gagal memperbarui buku. Id tidak ditemukan"
}
```

**Error Response (400):**
```json
{
  "status": "fail",
  "message": "Gagal memperbarui buku. Mohon isi nama buku"
}
```

---

### 5. Delete Book

Deletes a book by ID.

**Endpoint:** `DELETE /books/{id}`

**Path Parameters:**
- `id` (string): Book ID

**Example:**
```
DELETE /books/book-id-1
```

**Success Response (200):**
```json
{
  "status": "success",
  "message": "Buku berhasil dihapus"
}
```

**Error Response (404):**
```json
{
  "status": "fail",
  "message": "Buku gagal dihapus. Id tidak ditemukan"
}
```

## Data Models

### Book Object

```json
{
  "id": "string (16 characters)",
  "name": "string (required)",
  "year": "number (optional)",
  "author": "string (optional)",
  "summary": "string (optional)",
  "publisher": "string (optional)",
  "pageCount": "number (optional)",
  "readPage": "number (optional)",
  "finished": "boolean (auto-calculated)",
  "reading": "boolean (optional)",
  "insertedAt": "string (ISO 8601)",
  "updatedAt": "string (ISO 8601)"
}
```

### Response Format

All API responses follow this structure:

```json
{
  "status": "success|fail",
  "message": "string",
  "data": {
    // Response data (optional)
  }
}
```

## Status Codes

| Code | Description |
|------|-------------|
| 200  | OK - Request successful |
| 201  | Created - Resource created successfully |
| 400  | Bad Request - Validation error |
| 404  | Not Found - Resource not found |
| 500  | Internal Server Error - Server error |

## Error Messages

| Message | Description | Status Code |
|---------|-------------|-------------|
| `"Gagal menambahkan buku. Mohon isi nama buku"` | Missing book name | 400 |
| `"Gagal menambahkan buku. readPage tidak boleh lebih besar dari pageCount"` | Invalid read page count | 400 |
| `"Buku tidak ditemukan"` | Book not found | 404 |
| `"Gagal memperbarui buku. Id tidak ditemukan"` | Book ID not found for update | 404 |
| `"Gagal memperbarui buku. Mohon isi nama buku"` | Missing book name in update | 400 |
| `"Buku gagal dihapus. Id tidak ditemukan"` | Book ID not found for deletion | 404 |

## Examples

### Complete Workflow

1. **Add a book:**
   ```bash
   curl -X POST http://localhost:9000/books \
     -H "Content-Type: application/json" \
     -d '{
       "name": "To Kill a Mockingbird",
       "year": 1960,
       "author": "Harper Lee",
       "summary": "A story of racial injustice",
       "publisher": "J. B. Lippincott & Co.",
       "pageCount": 281,
       "readPage": 0,
       "reading": false
     }'
   ```

2. **Get all books:**
   ```bash
   curl http://localhost:9000/books
   ```

3. **Filter books by name:**
   ```bash
   curl "http://localhost:9000/books?name=mockingbird"
   ```

4. **Update a book:**
   ```bash
   curl -X PUT http://localhost:9000/books/book-id \
     -H "Content-Type: application/json" \
     -d '{
       "name": "To Kill a Mockingbird",
       "year": 1960,
       "author": "Harper Lee",
       "summary": "A story of racial injustice",
       "publisher": "J. B. Lippincott & Co.",
       "pageCount": 281,
       "readPage": 140,
       "reading": true
     }'
   ```

5. **Delete a book:**
   ```bash
   curl -X DELETE http://localhost:9000/books/book-id
   ```

## Testing

You can test the API using:

- **Postman**: Import the collection
- **cURL**: Use the examples above
- **Insomnia**: Create requests manually
- **Thunder Client**: VS Code extension

## Rate Limiting

Currently, there are no rate limits implemented. Consider implementing rate limiting for production use.

## CORS

The API supports CORS with the following configuration:
- Origin: `*` (all origins allowed)
- Methods: All HTTP methods
- Headers: All headers 