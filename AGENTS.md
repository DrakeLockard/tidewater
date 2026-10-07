# Base44 dev environment notes

- Pure client-side Vite + WebGPU game; no backend, database, or secrets.
- `docker-compose.base44.yml` runs a single `web` service (node:22, source bind-mounted, `node_modules` in a named volume, `npm ci` on start) and calls Vite with CLI flags `--host 0.0.0.0 --port 5173 --strictPort`. These flags override the `127.0.0.1:5188` set in `vite.config.js`, so that file stays unchanged. Host port 3000 maps to 5173.
- Vite 8 needs Node >= 20.19; use node:22.
- Headless/GPU-less browsers fail with "No WebGPU adapter found" after the title screen renders. That's expected. Gameplay needs a real WebGPU browser with a GPU.
- Tests: `docker compose -f docker-compose.base44.yml exec web npm test` (Node, uses the `webgpu` dev dependency).
- No sandbox-specific code overrides; `BASE44_PREVIEW_MODE` is passed through but unused.
