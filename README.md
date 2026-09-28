# TS Todo

**English** | [Русский](README.ru.md)

A to-do list built with vanilla TypeScript and Vite: classes, interfaces and singletons instead of a UI framework, with items kept in `localStorage`.

> 🎓 **Training project** · September 2025. A to-do list written while learning TypeScript classes and interfaces; no backend, all data lives in the browser.

**Live demo:** https://barbarafromtonshaevo.github.io/ts-todo/

<p>
  <img src="./screenshots/desktop.webp" alt="To-do list with five items, two of them checked, on desktop" width="68%">
  <img src="./screenshots/mobile.webp" alt="The same to-do list on mobile" width="24%">
</p>

## Features

- Add an item through the form (up to 40 characters, empty input is ignored).
- Mark an item as done: its text gets crossed out.
- Remove a single item or clear the whole list.
- The list survives page reloads.

## Tech stack

| Area | Tools |
| --- | --- |
| Language | TypeScript 5 (`strict`), vanilla DOM APIs |
| Build | Vite 7 |
| Styles | Plain CSS |
| Hosting | GitHub Pages (`gh-pages` package) |

## Architecture

```
form / buttons ──► main.ts ──► FullList (state + localStorage) ──► ListTemplate ──► <ul id="listItems">
```

1. [src/main.ts](src/main.ts) wires up the form and the Clear button, loads the saved list on `DOMContentLoaded` and renders it.
2. [src/model/FullList.ts](src/model/FullList.ts) holds the array of items and writes it to `localStorage` (key `myList`) after every change.
3. [src/model/ListItem.ts](src/model/ListItem.ts) is a single item with private fields behind getters and setters.
4. [src/templates/ListTemplate.ts](src/templates/ListTemplate.ts) rebuilds the `<ul>` from the list and attaches the checkbox and delete handlers to each row.

### Key decisions

- **Singletons for the model and the view.** `FullList.instance` and `ListTemplate.instance` have private constructors, so the whole app shares one state and one renderer.
- **Each class implements an interface** (`List`, `Item`, `DOMList`), so the contract is described separately from the implementation.

## Project structure

```
src/
├── css/style.css            # app styles
├── model/
│   ├── FullList.ts          # list state + localStorage persistence (singleton)
│   └── ListItem.ts          # a single to-do item
├── templates/
│   └── ListTemplate.ts      # renders the list to the DOM (singleton)
└── main.ts                  # entry point, event listeners
```

## Getting started

Requires Node.js 20.19+ (Vite 7).

```bash
npm install
npm run dev          # http://localhost:5173/ts-todo/
```

Other scripts:

```bash
npm run build        # type-check with tsc, then build into dist/
npm run preview      # serve the production build locally
npm run deploy       # build and publish dist/ to the gh-pages branch
```

## Deployment

Deployed on GitHub Pages from the `gh-pages` branch. There is no CI: `npm run deploy` builds locally and pushes `dist/` with the `gh-pages` package. Vite's `base` is set to `/ts-todo` in [vite.config.js](vite.config.js).

## Known limitations

- Long words in an item break at any letter (`word-break: break-all`), which is visible on mobile.
- Saved data mirrors the private field names (`_id`, `_item`, `_checked`), so renaming a field in `ListItem` breaks lists already stored in `localStorage`.
- Clear removes everything without confirmation, and items cannot be edited.

## What I'd improve

- **Explicit serialization.** A `toJSON()` / `fromJSON()` pair in `ListItem` would decouple the storage format from the class internals.
- **Softer text wrapping.** `overflow-wrap: anywhere` breaks only words that do not fit.
- **Unit tests** with Vitest for `FullList`: adding, removing, clearing and loading from `localStorage`.
- **Deploy via GitHub Actions** instead of publishing from a local machine.
