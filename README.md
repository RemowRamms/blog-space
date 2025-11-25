# Blog Space

[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

A modern, full-stack blog application built with React, Express.js, and MongoDB. Features a rich text editor, user authentication, dark/light themes, and a responsive design built with Tailwind CSS.

**Frontend**: React 18 + Vite + Tailwind CSS + React Query  
**Backend**: Express.js + MongoDB + JWT Authentication  
**UI Components**: Radix UI + Lucide Icons + Framer Motion

---

## Table of Contents

1. [Features](#features)  
2. [Prerequisites](#prerequisites)  
3. [Installation](#installation)  
4. [Available Scripts](#available-scripts)  
5. [Project Structure](#project-structure)  
6. [Configuration](#configuration)  
7. [Styling & Theming](#styling--theming)  
8. [Storybook](#storybook)  
9. [Linting & Formatting](#linting--formatting)  
10. [Testing](#testing)  
11. [Commit Hooks](#commit-hooks)  
13. [Contributing](#contributing)  
14. [License](#license)

---

## Features

### Frontend
- ⚡️ **Vite** for lightning-fast development and builds
- 📝 **Rich Text Editor** with Quill.js for creating and editing posts
- 🎨 **Tailwind CSS** for modern, responsive styling
- 🌙 **Dark/Light Themes** with smooth transitions via next-themes
- 🔍 **Client-side Routing** with React Router DOM
- 🧩 **Modern UI Components** with Radix UI primitives
- 🎯 **Form Handling** with React Hook Form + Zod validation
- 🚀 **State Management** with React Query for server state
- 📱 **Responsive Design** optimized for all screen sizes
- 🎭 **Animations** with Framer Motion
- 🔔 **Toast Notifications** with Sonner

### Backend
- ⚡️ **Express.js** for fast, reliable API server
- 🗄️ **MongoDB** with Mongoose ODM for data persistence
- 🔐 **JWT Authentication** with secure password hashing
- 📝 **Blog Post CRUD** operations with author permissions
- 🖼️ **Image Upload** support for blog posts
- 👤 **User Management** with registration and login
- 🧪 **Testing** with Jest and MongoDB Memory Server
- 🔄 **Auto-reload** with Nodemon during development

### Development Tools
- 📖 **Storybook** for component development and documentation
- 🧪 **Testing** with Vitest (unit) and Playwright (e2e)
- 🧹 **Code Quality** with ESLint, Prettier, and lint-staged
- 🪝 **Git Hooks** with Husky for pre-commit checks
- 📝 **Conventional Commits** with Commitlint  

---

## Prerequisites

- Node.js >= 18  
- npm >= 9.x or Yarn >= 1.x  

Verify you have them installed:

```bash
node -v
npm -v
# or
yarn -v
```

---

## Installation

Clone the repository:

```bash
git clone https://github.com/RemowRamms/blog-space.git
cd blog-space
```

Install frontend dependencies:

```bash
npm install
```

Install backend dependencies:

```bash
cd backend
npm install
cd ..
```

Initialize Git hooks:

```bash
npm run prepare
```

---

## Available Scripts

### Frontend (from project root)

```bash
npm run dev
```

Starts the Vite development server on [http://localhost:5173](http://localhost:5173).

```bash
npm run build
```

Builds the frontend for production into `dist/`.

```bash
npm run preview
```

Serves the production build locally.

```bash
npm run lint
```

Runs ESLint on `src/` and auto-fixes issues.

```bash
npm run storybook
```

Launches Storybook on [http://localhost:6006](http://localhost:6006).

```bash
npm run build-storybook
```

Builds the static Storybook site.

### Backend (from backend/ directory)

```bash
npm run dev
```

Starts the Express development server with auto-reload on [http://localhost:5000](http://localhost:5000).

```bash
npm start
```

Starts the production server.

```bash
npm run lint
```

Runs ESLint on `backend/src/`.

```bash
npm test
```

Runs Jest tests for the backend API.

---

## Project Structure

```
react-blog/
├── .husky/                  # Git hooks
│   ├── commit-msg
│   └── pre-commit
├── .storybook/              # Storybook configuration
│   ├── main.js
│   └── preview.js
├── backend/                 # Backend logic (API, DB, services)
│   ├── __tests__/           # Backend tests
│   ├── db/                  # Database config or models
│   ├── middleware/          # Express middleware
│   ├── routes/              # API routes
│   ├── services/            # Business logic
│   ├── test/                # Additional backend tests
│   ├── app.js
│   ├── example.js
│   └── index.js
├── public/                  # Static assets
│   ├── pic1.jpg
│   └── vite.svg
├── src/                     # Frontend source
│   ├── api/                 # API utilities
│   ├── assets/              # Images, fonts, etc.
│   ├── components/          # Reusable UI components
│   ├── contexts/            # React context providers
│   ├── hooks/               # Custom React hooks
│   ├── lib/                 # Utility functions/libraries
│   ├── pages/               # Page components
│   ├── stories/             # Storybook stories
│   ├── App.css
│   ├── App.jsx
│   └── main.jsx
├── vitest.setup.ts         # Vitest setup
├── vitest.workspace.js     # Vitest config for workspaces
├── components.json          # Custom config (possibly for Storybook or dynamic imports)
├── index.html               # App HTML template
├── jsconfig.json            # JS/TS project config
├── package.json
├── package-lock.json
├── tsconfig.json
├── tsconfig.app.json
├── tsconfig.node.json
├── vite.config.js           # Vite config
├── .env
├── .commitlintrc.json
├── .eslintrc.json
├── .eslintignore
├── .prettierrc.json
├── .prettierignore
├── .gitignore
├── README.md
├── jest.config.json
├── nodemon.json
```


---

## Configuration

### Frontend Environment Variables

Create a `.env` file in the project root:

```ini
VITE_API_URL=http://localhost:5000/api
```

### Backend Environment Variables

Create a `.env` file in the `backend/` directory:

```ini
MONGODB_URI=mongodb://localhost:27017/blog-space
JWT_SECRET=your-super-secret-jwt-key-here
PORT=5000
NODE_ENV=development
```

**Required Backend Variables:**
- `MONGODB_URI`: MongoDB connection string (local or Atlas)
- `JWT_SECRET`: Secret key for signing JWT tokens (use a strong, random string in production)
- `PORT`: Server port (default: 5000)
- `NODE_ENV`: Environment mode (`development` or `production`)

---

## Styling & Theming

- Tailwind CSS is configured via `tailwind.config.js`
- Utility‑first styling with optional `class‑variance‑authority`
- Light/dark theme toggle powered by `next-themes`

---

## Storybook

Your component library and UI states live in Storybook:

- Run `npm run storybook` to develop in isolation
- Run `npm run build-storybook` to generate a static site for review
- Chromatic support is preconfigured via `@chromatic-com/storybook`

---

## Linting & Formatting

- ESLint configuration in `.eslintrc.js`
- Prettier configuration in `.prettierrc` + `prettier-plugin-tailwindcss`
- `lint-staged` auto‑formats and lints on git commit

---

## Testing

### Frontend Testing

**Vitest** for unit and integration tests:

```bash
npx vitest
```

**Playwright** for end-to-end browser tests:

```bash
npx playwright test
```

### Backend Testing

**Jest** for API unit tests:

```bash
cd backend
npm test
```

Backend tests use MongoDB Memory Server for isolated test environments without requiring a live database.

---

## Commit Hooks

- Husky installs Git hooks on `npm run prepare`
- Commitlint enforces Conventional Commits
- `lint-staged` runs Prettier & ESLint on staged files

---

## Quick Start

1. **Start the Backend:**
   ```bash
   cd backend
   npm run dev
   ```

2. **Start the Frontend:** (in a new terminal)
   ```bash
   npm run dev
   ```

3. **Open your browser:**
   - Frontend: [http://localhost:5173](http://localhost:5173)
   - Backend API: [http://localhost:5000](http://localhost:5000)
   - Storybook: [http://localhost:6006](http://localhost:6006) (run `npm run storybook`)

## Contributing

- Fork the repository
- Create a feature branch (`git checkout -b feature/amazing-feature`)
- Commit your changes using conventional commits (`feat:`, `fix:`, `docs:`, etc.)
- Push to your branch (`git push origin feature/amazing-feature`)
- Open a Pull Request

Please follow our code of conduct and coding standards.

---

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
