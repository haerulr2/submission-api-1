# Development Guide

This guide provides detailed information for developers who want to contribute to or extend the Bookshelf API project.

## 🏗️ Architecture Overview

The project follows a simple modular architecture:

```
src/
├── server.js      # Main server configuration
├── routes.js      # Route definitions
├── handler.js     # Business logic and request handlers
└── books.js       # Data layer (in-memory storage)
```

### Architecture Principles

1. **Separation of Concerns**: Each file has a specific responsibility
2. **Modularity**: Easy to extend and maintain
3. **Simplicity**: Minimal dependencies and straightforward code
4. **Testability**: Functions are pure and easily testable

## 🛠️ Development Setup

### Prerequisites

- Node.js (v14 or higher)
- npm or yarn
- Git

### Local Development

1. **Clone and install:**
   ```bash
   git clone <repository-url>
   cd bookshelf-api
   npm install
   ```

2. **Start development server:**
   ```bash
   npm run start-dev
   ```

3. **Run linting:**
   ```bash
   npm run lint
   ```

### Environment Variables

Currently, the project uses hardcoded values. For production, consider adding:

```bash
# .env
PORT=9000
HOST=localhost
NODE_ENV=development
```

## 📁 Project Structure

### Core Files

#### `src/server.js`
- Main server configuration
- CORS setup
- Error handling
- Route registration

#### `src/routes.js`
- Route definitions
- HTTP method mapping
- CORS configuration per route

#### `src/handler.js`
- Request handlers
- Business logic
- Validation
- Response formatting

#### `src/books.js`
- Data storage (in-memory array)
- Can be extended to use database

### Configuration Files

#### `package.json`
- Dependencies and scripts
- Project metadata
- NPM scripts

#### `.eslintrc.js`
- Code style rules
- Linting configuration
- Best practices enforcement

## 🔧 Code Style Guide

### JavaScript/Node.js Conventions

1. **Indentation**: 2 spaces
2. **Quotes**: Single quotes for strings
3. **Semicolons**: Always required
4. **Line endings**: Unix (LF)
5. **Trailing spaces**: Not allowed
6. **Object spacing**: Spaces inside curly braces

### Function Naming

- Use descriptive names
- Prefix event handlers with `handle`
- Use camelCase for variables and functions
- Use PascalCase for classes

### Code Organization

```javascript
// ANCHOR: Imports
const { nanoid } = require('nanoid');

// ANCHOR: Constants
const BOOK_FIELDS = ['name', 'year', 'author'];

// ANCHOR: Helper Functions
const validateBook = (book) => {
  // validation logic
};

// ANCHOR: Main Functions
const addBookHandler = (request, h) => {
  // handler logic
};
```

## 🧪 Testing Strategy

### Manual Testing

1. **API Testing Tools:**
   - Postman
   - Insomnia
   - Thunder Client (VS Code)

2. **cURL Examples:**
   ```bash
   # Test all endpoints
   curl -X POST http://localhost:9000/books -H "Content-Type: application/json" -d '{"name":"Test Book"}'
   curl http://localhost:9000/books
   curl http://localhost:9000/books/book-id
   curl -X PUT http://localhost:9000/books/book-id -H "Content-Type: application/json" -d '{"name":"Updated Book"}'
   curl -X DELETE http://localhost:9000/books/book-id
   ```

### Automated Testing (Future Enhancement)

Consider adding:
- Unit tests with Jest
- Integration tests
- API tests with Supertest
- Load testing with Artillery

## 🔄 Data Flow

### Request Flow

1. **Client Request** → `server.js`
2. **Route Matching** → `routes.js`
3. **Handler Execution** → `handler.js`
4. **Data Operations** → `books.js`
5. **Response** → Client

### Data Validation Flow

1. **Input Validation** → Check required fields
2. **Business Logic** → Apply business rules
3. **Data Persistence** → Store/retrieve data
4. **Response Formatting** → Format response

## 🚀 Adding New Features

### Adding a New Endpoint

1. **Define the route in `routes.js`:**
   ```javascript
   {
     method: 'GET',
     path: '/books/search',
     handler: searchBooksHandler,
     options: {
       cors: { origin: ['*'] }
     }
   }
   ```

2. **Create handler in `handler.js`:**
   ```javascript
   const searchBooksHandler = (request, h) => {
     // Implementation
   };
   ```

3. **Export the handler:**
   ```javascript
   module.exports = {
     // ... existing exports
     searchBooksHandler
   };
   ```

### Adding New Validation

1. **Create validation function:**
   ```javascript
   const validateSearchParams = (params) => {
     // validation logic
   };
   ```

2. **Use in handler:**
   ```javascript
   const searchBooksHandler = (request, h) => {
     const validation = validateSearchParams(request.query);
     if (!validation.isValid) {
       return h.response({
         status: 'fail',
         message: validation.message
       }).code(400);
     }
     // ... rest of handler
   };
   ```

## 🔍 Debugging

### Logging

The project uses console.log for debugging. For production, consider:

```javascript
// Add structured logging
const logger = {
  info: (message, data) => console.log(`[INFO] ${message}`, data),
  error: (message, error) => console.error(`[ERROR] ${message}`, error),
  debug: (message, data) => console.log(`[DEBUG] ${message}`, data)
};
```

### Common Issues

1. **Port already in use:**
   ```bash
   # Find process using port 9000
   lsof -i :9000
   # Kill process
   kill -9 <PID>
   ```

2. **CORS issues:**
   - Check CORS configuration in `server.js`
   - Verify origin settings

3. **Validation errors:**
   - Check request body format
   - Verify required fields
   - Check data types

## 📊 Performance Considerations

### Current Implementation

- **In-memory storage**: Fast but not persistent
- **Simple validation**: Lightweight
- **No caching**: Each request processed fresh

### Optimization Opportunities

1. **Database Integration:**
   ```javascript
   // Replace books array with database
   const { Pool } = require('pg');
   const pool = new Pool({
     connectionString: process.env.DATABASE_URL
   });
   ```

2. **Caching:**
   ```javascript
   // Add Redis caching
   const redis = require('redis');
   const client = redis.createClient();
   ```

3. **Rate Limiting:**
   ```javascript
   // Add rate limiting middleware
   const rateLimit = require('express-rate-limit');
   ```

## 🔒 Security Considerations

### Current Security

- **CORS**: Configured for development
- **Input Validation**: Basic validation implemented
- **No Authentication**: Public API

### Security Enhancements

1. **Input Sanitization:**
   ```javascript
   const sanitizeInput = (input) => {
     // Sanitize user input
   };
   ```

2. **Authentication:**
   ```javascript
   // Add JWT authentication
   const jwt = require('jsonwebtoken');
   ```

3. **Rate Limiting:**
   ```javascript
   // Implement rate limiting
   const rateLimit = require('express-rate-limit');
   ```

## 🚀 Deployment

### Production Considerations

1. **Environment Variables:**
   ```bash
   PORT=9000
   HOST=0.0.0.0
   NODE_ENV=production
   ```

2. **Process Management:**
   ```bash
   # Use PM2 for production
   npm install -g pm2
   pm2 start src/server.js --name "bookshelf-api"
   ```

3. **Reverse Proxy:**
   ```nginx
   # Nginx configuration
   server {
       listen 80;
       server_name api.example.com;
       
       location / {
           proxy_pass http://localhost:9000;
       }
   }
   ```

## 📝 Contributing Guidelines

### Before Contributing

1. **Fork the repository**
2. **Create a feature branch**
3. **Follow the code style**
4. **Add tests if applicable**
5. **Update documentation**

### Pull Request Process

1. **Update README.md** if needed
2. **Update API_DOCUMENTATION.md** if adding endpoints
3. **Test thoroughly**
4. **Submit PR with clear description**

### Code Review Checklist

- [ ] Code follows style guide
- [ ] Functions are properly documented
- [ ] Error handling is implemented
- [ ] No console.log in production code
- [ ] All tests pass
- [ ] Documentation is updated

## 🆘 Troubleshooting

### Common Issues

1. **Server won't start:**
   - Check if port 9000 is available
   - Verify Node.js version
   - Check for syntax errors

2. **CORS errors:**
   - Verify CORS configuration
   - Check client origin

3. **Validation errors:**
   - Check request format
   - Verify required fields

### Getting Help

1. Check existing issues
2. Create detailed bug report
3. Include error messages and steps to reproduce
4. Provide environment information

---

**Happy coding! 🚀** 