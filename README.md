# Happy Bird

## OVERVIEW

Happy Bird is a small browser-based Flappy Bird clone implemented in plain JavaScript, HTML and CSS. It includes a Progressive Web App (PWA) manifest and a service worker so it can be installed and run offline on supported devices.

Key features:
- Lightweight, single-page game using a `<canvas>`.
- Modular game code inside `scripts/game/`.
- PWA support via `manifest.json` and a root `service-worker.js`.

## ARCHITECTURE

The app is organized as a simple static web project:

- `index.html` — single page entry that loads the game and the PWA manifest.
- `styles/` — CSS for layout and visual presentation.
- `images/` — app icons and in-game assets.
- `scripts/` — main boot script and game modules. Key files:
  - `scripts/main.js` — initializes the game and registers the service worker.
  - `scripts/game/` — contains game logic modules (bird, pipes, renderer, state, audio, etc.).
- `service-worker.js` — root-level service worker that caches the app shell and assets.
- `manifest.json` — PWA metadata (icons, start_url, display mode).

Design notes:
- The game loop, rendering, and state are split into small modules under `scripts/game/` for clarity and testability.
- The service worker uses a simple cache-first strategy for app shell assets and falls back to network for others.

## USAGE

Prerequisites: a static HTTP server is required for service worker and PWA features to work correctly (file:// will not register a service worker).

Running locally:

1. From the project root run a quick static server, for example with Python 3:

```bash
python -m http.server 8000
```

2. Open `http://localhost:8000` in a modern browser.

Notes about PWA and installation:
- The app manifest is linked from `index.html`. The service worker is registered from `scripts/main.js` as `/service-worker.js` so the worker's scope covers the whole site.
- To test PWA install behavior, open DevTools → Application → Manifest, and simulate install or use the browser prompt.
- If you change the service worker, increment the cache name inside `service-worker.js` to force clients to update.

Debugging tips:
- Use the browser's DevTools Network tab with Service Worker and Cache storage panes visible to inspect cached entries.
- If the page doesn't update after edits, try unregistering the service worker and clearing the site data, or increment the cache version constant.

## FILE STRUCTURE

Top-level overview:

```
index.html
manifest.json
service-worker.js
images/
  icon.png
  happybird.png
  iconsmall.png
scripts/
  main.js
  game/
    audio.js
    bird.js
    collision.js
    pipes.js
    renderer.js
    state.js
styles/
  style.css
```

## CONTRIBUTING

- Fork the repository, create a feature branch, and open a pull request.
- Keep changes focused and include small, testable commits.
- Follow existing code style (ES modules, short functions, no global mutations where possible).

## LICENSE

This project is provided under the MIT License.

MIT License

Copyright (c) 2026

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
