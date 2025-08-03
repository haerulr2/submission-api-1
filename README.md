# Bookshelf API

A RESTful API for managing books built with Node.js and Hapi framework.

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Usage](#usage)
- [API Endpoints](#api-endpoints)
- [Data Structure](#data-structure)
- [Error Handling](#error-handling)
- [Development](#development)
- [Contributing](#contributing)

## 🎯 Overview

Bookshelf API is a simple and efficient REST API for managing a personal book collection. Built with the Hapi framework, it provides CRUD operations for books with features like filtering, validation, and proper error handling.

## ✨ Features

- **CRUD Operations**: Create, Read, Update, and Delete books
- **Filtering**: Filter books by name, reading status, and finished status
- **Validation**: Comprehensive input validation
- **CORS Support**: Cross-origin resource sharing enabled
- **Error Handling**: Proper HTTP status codes and error messages
- **In-Memory Storage**: Simple in-memory data storage (can be extended to database)

## 🔧 Prerequisites

Before running this project, make sure you have:

- **Node.js** (version 14 or higher)
- **npm** (comes with Node.js)

## 🚀 Installation

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd bookshelf-api
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Start the server**
   ```bash
   # Production mode
   npm start
   
   # Development mode (with auto-restart)
   npm run start-dev
   ```

The server will start on `http://localhost:9000`

## 📖 Usage

### Starting the Server

```bash
# Development mode (recommended for development)
npm run start-dev

# Production mode
npm start
```

### Testing the API

You can test the API using tools like:
- **Postman**
- **cURL**
- **Insomnia**
- **Thunder Client** (VS Code extension)

## 🔌 API Endpoints

### 1. Add Book
- **Method**: `POST`
- **URL**: `/books`
- **Body**:
  ```json
  {
    "name": "Book Title",
    "year": 2023,
    "author": "Author Name",
    "summary": "Book summary",
    "publisher": "Publisher Name",
    "pageCount": 300,
    "readPage": 150,
    "reading": false
  }
  ```

### 2. Get All Books
- **Method**: `GET`
- **URL**: `/books`
- **Query Parameters**:
  - `name` (optional): Filter by book name
  - `reading` (optional): Filter by reading status (0 or 1)
  - `finished` (optional): Filter by finished status (0 or 1)

### 3. Get Book by ID
- **Method**: `GET`
- **URL**: `/books/{id}`

### 4. Update Book
- **Method**: `PUT`
- **URL**: `/books/{id}`
- **Body**: Same as Add Book

### 5. Delete Book
- **Method**: `DELETE`
- **URL**: `/books/{id}`

## 📊 Data Structure

### Book Object
```json
{
  "id": "unique-id",
  "name": "Book Title",
  "year": 2023,
  "author": "Author Name",
  "summary": "Book summary",
  "publisher": "Publisher Name",
  "pageCount": 300,
  "readPage": 150,
  "finished": false,
  "reading": false,
  "insertedAt": "2023-01-01T00:00:00.000Z",
  "updatedAt": "2023-01-01T00:00:00.000Z"
}
```

### Response Format
```json
{
  "status": "success|fail",
  "message": "Response message",
  "data": {
    // Response data
  }
}
```

## ⚠️ Error Handling

The API returns appropriate HTTP status codes:

- **200**: Success
- **201**: Created
- **400**: Bad Request (validation errors)
- **404**: Not Found
- **500**: Internal Server Error

### Common Error Messages

- `"Gagal menambahkan buku. Mohon isi nama buku"` - Missing book name
- `"Gagal menambahkan buku. readPage tidak boleh lebih besar dari pageCount"` - Invalid read page count
- `"Buku tidak ditemukan"` - Book not found

## 🛠️ Development

### Project Structure
```
bookshelf-api/
├── src/
│   ├── server.js      # Main server file
│   ├── routes.js      # Route definitions
│   ├── handler.js     # Request handlers
│   └── books.js       # Data storage
├── package.json
├── .eslintrc.js       # ESLint configuration
└── README.md
```

### Available Scripts

```bash
# Start the server
npm start

# Start in development mode (with auto-restart)
npm run start-dev

# Run linting
npm run lint
```

### Code Style

This project uses ESLint with the following rules:
- 2-space indentation
- Single quotes
- Semicolons required
- Unix line endings
- No trailing spaces
- Object curly spacing
- Arrow spacing
- No unused variables

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📝 License

This project is licensed under the ISC License.

## 🆘 Support

If you encounter any issues or have questions:

1. Check the [Issues](link-to-issues) page
2. Create a new issue with detailed information
3. Include error messages and steps to reproduce

---

**Happy coding! 📚✨** 