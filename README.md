# TS Todo

A small to-do list app built with vanilla TypeScript and Vite, using object-oriented patterns (singletons, interfaces) instead of a UI framework. Items persist between sessions via `localStorage`.

**Live demo:** https://barbarafromtonshaevo.github.io/ts-todo/

## About

This project was built as a practical exercise in writing type-safe, framework-free front-end code with TypeScript. It focuses on core OOP concepts — classes, interfaces, getters/setters, and the singleton pattern — applied to a familiar problem (a to-do list) rather than relying on a framework's state management. No backend is required: all data lives in the browser's `localStorage`.

## Features

- Add new to-do items via a simple form
- Mark items as done/undone with a checkbox
- Remove individual items
- Clear the entire list at once
- Data persists across page reloads using `localStorage`

## Tech Stack

- [TypeScript](https://www.typescriptlang.org/)
- [Vite](https://vitejs.dev/) — dev server and build tool
- Vanilla DOM APIs (no UI framework)
- [gh-pages](https://www.npmjs.com/package/gh-pages) — deployment to GitHub Pages

## Project Structure

```
src/
├── css/
│   └── style.css        # App styles
├── model/
│   ├── FullList.ts       # Singleton managing the list state + localStorage persistence
│   └── ListItem.ts        # Data model for a single to-do item
├── templates/
│   └── ListTemplate.ts    # Renders the list state to the DOM
└── main.ts                 # App entry point, wires up event listeners
```

## Getting Started

### Prerequisites

- [Node.js](https://nodejs.org/) (with npm)

### Installation

```bash
git clone https://github.com/BarbaraFromTonshaevo/ts-todo.git
cd ts-todo
npm install
```

### Development

Start the local dev server:

```bash
npm run dev
```

### Build

Type-check and build for production:

```bash
npm run build
```

### Preview

Preview the production build locally:

```bash
npm run preview
```

### Deploy

Build and publish the `dist` folder to GitHub Pages:

```bash
npm run deploy
```

## License

No license specified.
