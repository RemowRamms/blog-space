# React Blog - Backend API

[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

Express.js backend API for the React Blog application. Provides RESTful endpoints for user authentication, blog post management, and image uploads with MongoDB persistence.

---

## Table of Contents

1. [Features](#features)
2. [Prerequisites](#prerequisites)
3. [Installation](#installation)
4. [Environment Setup](#environment-setup)
5. [Available Scripts](#available-scripts)
6. [API Routes](#api-routes)
7. [Database](#database)
8. [Authentication](#authentication)
9. [Project Structure](#project-structure)
10. [Testing](#testing)
11. [Linting & Formatting](#linting--formatting)
12. [Contributing](#contributing)
13. [License](#license)

---

## Features

- ⚡️ **Express.js** for fast, lightweight API server
- 🗄️ **MongoDB** with Mongoose ODM for data persistence
- 🔐 **JWT Authentication** with bcrypt password hashing
- 📝 **Blog Post Management** (CRUD operations)
- 🖼️ **Image Upload** support
- 👤 **User Management** with role-based access
- 🧪 **Jest** unit tests with MongoDB Memory Server
- 🔄 **Nodemon** for auto-reload during development
- 🧹 **ESLint + Prettier** for code quality
- 📋 **CORS** enabled for frontend integration

---

## Prerequisites

- Node.js >= 18
- npm >= 9.x
- MongoDB (local or cloud instance, e.g., MongoDB Atlas)

Verify Node.js and npm:

```bash
node -v
npm -v
```

---

## Installation

From the project root, navigate to the backend directory:

```bash
cd backend
```

Install dependencies:

```bash
npm install
```

---

## Environment Setup

Create a `.env` file in the `backend/` directory with the following variables:

```ini
MONGODB_URI=mongodb://localhost:27017/react-blog
JWT_SECRET=your-secret-key-here
PORT=5000
NODE_ENV=development
```

**Environment Variables:**

- **MONGODB_URI**: MongoDB connection string (local or Atlas)
- **JWT_SECRET**: Secret key for signing JWT tokens (use a strong, random string in production)
- **PORT**: Server port (default: 5000)
- **NODE_ENV**: Environment mode (`development` or `production`)

---

## Available Scripts

From the `backend/` directory:

```bash
npm run dev
```

Starts the development server with Nodemon auto-reload on [http://localhost:5000](http://localhost:5000).

```bash
npm start
```

Starts the production server.

```bash
npm run lint
```

Runs ESLint on `src/` and reports issues.

```bash
npm test
```

Runs Jest tests with MongoDB Memory Server for isolated test environments.

---

## API Routes

### Users (`/api/users`)

- **POST** `/api/users/register` - Register a new user
  - Body: `{ email, password, name }`
  - Returns: User object with JWT token

- **POST** `/api/users/login` - Authenticate user
  - Body: `{ email, password }`
  - Returns: User object with JWT token

- **GET** `/api/users/:id` - Get user by ID (requires auth)
  - Returns: User object

- **PUT** `/api/users/:id` - Update user profile (requires auth)
  - Body: `{ name, email, ... }`
  - Returns: Updated user object

### Posts (`/api/posts`)

- **GET** `/api/posts` - Get all posts
  - Query: `?limit=10&page=1`
  - Returns: Array of posts with pagination

- **GET** `/api/posts/:id` - Get post by ID
  - Returns: Post object with author details

- **POST** `/api/posts` - Create new post (requires auth)
  - Body: `{ title, content, tags }`
  - Returns: Created post object

- **PUT** `/api/posts/:id` - Update post (requires auth, author only)
  - Body: `{ title, content, tags }`
  - Returns: Updated post object

- **DELETE** `/api/posts/:id` - Delete post (requires auth, author only)
  - Returns: Success message

### Images (`/api/images`)

- **POST** `/api/images/upload` - Upload image (requires auth)
  - Body: FormData with `file` field
  - Returns: Image URL and metadata

- **GET** `/api/images/:id` - Get image by ID
  - Returns: Image metadata

- **DELETE** `/api/images/:id` - Delete image (requires auth, uploader only)
  - Returns: Success message

---

## Database

### MongoDB Setup

**Local MongoDB:**

```bash
# macOS with Homebrew
brew services start mongodb-community

# Windows (if installed)
mongod

# Linux
sudo systemctl start mongod
```

**MongoDB Atlas (Cloud):**

1. Create account at [mongodb.com/cloud/atlas](https://mongodb.com/cloud/atlas)
2. Create a cluster and database
3. Get connection string: `mongodb+srv://username:password@cluster.mongodb.net/dbname`
4. Add to `.env` as `MONGODB_URI`

### Models

- **User**: Email, password hash, name, created_at
- **Post**: Title, content, author (ref), tags, created_at, updated_at
- **Image**: URL, uploader (ref), filename, created_at

---

## Authentication

JWT-based authentication is implemented via `middleware/jwt.js`:

1. User registers/logs in → receives JWT token
2. Client includes token in `Authorization: Bearer <token>` header
3. Middleware verifies token and attaches user to request
4. Protected routes check for valid token

**Token Expiry**: Configure in JWT middleware (default: 7 days)

---

## Project Structure

```
backend/
├── src/
│   ├── __tests__/              # Jest unit tests
│   │   ├── users.test.js
│   │   ├── posts.test.js
│   │   └── images.test.js
│   ├── db/
│   │   └── init.js             # MongoDB connection & initialization
│   ├── middleware/
│   │   └── jwt.js              # JWT authentication middleware
│   ├── routes/
│   │   ├── users.js            # User endpoints
│   │   ├── posts.js            # Post endpoints
│   │   └── images.js           # Image endpoints
│   ├── services/
│   │   ├── users.js            # User business logic
│   │   ├── posts.js            # Post business logic
│   │   └── images.js           # Image business logic
│   ├── test/
│   │   ├── globalSetup.js      # Jest setup
│   │   ├── globalTeardown.js   # Jest teardown
│   │   └── setupFileAfterEnv.js # Test environment config
│   ├── app.js                  # Express app configuration
│   ├── example.js              # Example/seed data
│   └── index.js                # Server entry point
├── .env                        # Environment variables (not in git)
├── .eslintrc.json              # ESLint config
├── .prettierrc.json            # Prettier config
├── jest.config.json            # Jest config
├── nodemon.json                # Nodemon config
├── package.json
├── package-lock.json
└── README.md
```

---

## Testing

Run tests with Jest:

```bash
npm test
```

Tests use MongoDB Memory Server for isolated, fast test execution without requiring a live database.

**Test Files:**

- `__tests__/users.test.js` - User registration, login, profile
- `__tests__/posts.test.js` - Post CRUD operations
- `__tests__/images.test.js` - Image upload and management

---

## Linting & Formatting

```bash
npm run lint
```

Runs ESLint on the `src/` directory. Configuration is in `.eslintrc.json`.

Format code with Prettier:

```bash
npx prettier --write src/
```

---

## Contributing

- Fork the repository
- Create a feature branch
- Commit your changes
- Push to your branch
- Open a Pull Request

---

## License

This project is licensed under the MIT License. See the [LICENSE](../LICENSE) file for details.
