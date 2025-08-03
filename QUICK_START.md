# Quick Start Guide

Get the Bookshelf API up and running in minutes!

## ⚡ Quick Setup

### 1. Install Dependencies
```bash
npm install
```

### 2. Start the Server
```bash
# Development mode (recommended)
npm run start-dev

# OR Production mode
npm start
```

### 3. Test the API
The server will be running at `http://localhost:9000`

## 🧪 Quick Test

### Add a Book
```bash
curl -X POST http://localhost:9000/books \
  -H "Content-Type: application/json" \
  -d '{
    "name": "The Hobbit",
    "year": 1937,
    "author": "J.R.R. Tolkien",
    "summary": "A hobbit's journey",
    "publisher": "Allen & Unwin",
    "pageCount": 310,
    "readPage": 0,
    "reading": false
  }'
```

### Get All Books
```bash
curl http://localhost:9000/books
```

## 📋 Available Commands

| Command | Description |
|---------|-------------|
| `npm start` | Start production server |
| `npm run start-dev` | Start development server (auto-restart) |
| `npm run lint` | Run code linting |

## 🔧 Configuration

### Default Settings
- **Port**: 9000
- **Host**: localhost
- **CORS**: Enabled for all origins

### Environment Variables (Optional)
Create a `.env` file:
```bash
PORT=9000
HOST=localhost
NODE_ENV=development
```

## 📚 API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/books` | Add a new book |
| GET | `/books` | Get all books |
| GET | `/books/{id}` | Get book by ID |
| PUT | `/books/{id}` | Update book |
| DELETE | `/books/{id}` | Delete book |

## 🛠️ Development Tools

### Recommended Tools
- **Postman**: API testing
- **Insomnia**: Alternative to Postman
- **Thunder Client**: VS Code extension
- **cURL**: Command line testing

### VS Code Extensions
- **Thunder Client**: API testing
- **ESLint**: Code linting
- **Prettier**: Code formatting

## 🚨 Troubleshooting

### Common Issues

**Port 9000 already in use:**
```bash
# Find the process
lsof -i :9000

# Kill the process
kill -9 <PID>
```

**Server won't start:**
- Check Node.js version (v14+)
- Verify all dependencies installed
- Check for syntax errors

**CORS errors:**
- Verify server is running
- Check client origin
- Ensure CORS is configured

## 📖 Next Steps

1. **Read the full documentation**: [README.md](README.md)
2. **Explore API details**: [API_DOCUMENTATION.md](API_DOCUMENTATION.md)
3. **Learn development**: [DEVELOPMENT.md](DEVELOPMENT.md)

## 🆘 Need Help?

- Check the [README.md](README.md) for detailed information
- Review [API_DOCUMENTATION.md](API_DOCUMENTATION.md) for endpoint details
- See [DEVELOPMENT.md](DEVELOPMENT.md) for development guidelines

---

**Happy coding! 🚀** 