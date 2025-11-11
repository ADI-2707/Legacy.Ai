# Frontend - Legacy.Ai

A React-based frontend for an AI-powered code review application.

## Features

- **Code Editor**: Interactive code editor with syntax highlighting powered by Prism.js
- **Code Review**: Submit code snippets to the backend AI service for intelligent reviews
- **Markdown Display**: Reviews are rendered as formatted markdown with code highlighting
- **Syntax Highlighting**: Support for JavaScript syntax highlighting and multiple themes
- **Real-time Editing**: Live code updates with automatic syntax highlighting

## Tech Stack

- **React** 19.1.1 - UI framework
- **Vite** 7.1.7 - Build tool and dev server
- **Axios** 1.12.2 - HTTP client for API requests
- **React Markdown** 10.1.0 - Markdown rendering
- **Prism.js** 1.30.0 - Syntax highlighting
- **React Simple Code Editor** 0.14.1 - Code editing component

## Getting Started

### Installation

```bash
npm install
```

### Development

```bash
npm run dev
```

Starts the development server at `http://localhost:5173`

### Build

```bash
npm run build
```

Creates an optimized production build in the `dist` folder.

### Lint

```bash
npm lint
```

Checks code quality with ESLint.

## Project Structure

```
src/
├── App.jsx          # Main application component
├── App.css          # Application styles
├── main.jsx         # Entry point
└── index.css        # Global styles
```

## How It Works

1. User writes or pastes code in the editor
2. Click the review button to send code to the backend
3. Backend AI service analyzes the code
4. Review results are displayed as formatted markdown with syntax highlighting

## API Integration

The frontend connects to the backend API at `http://localhost:3000/ai/get-review` to send code for review.

## Notes

- Ensure the backend server is running before using the code review feature
- The application uses a dark GitHub theme for code syntax highlighting

## Connect with me
- **LinkedIn:** https://www.linkedin.com/in/devadi
- **GitHub:** https://github.com/ADI-2707
