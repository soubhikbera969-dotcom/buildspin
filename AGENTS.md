# Buildspin — Base44 Dev Notes

## What this is
A single-page static PWA. No backend, no build step, no dependencies. Just `index.html` (inline CSS + JS), `manifest.json`, `sw.js`, and two icon PNGs.

## How it runs here
Served by `nginx:alpine` via `docker-compose.base44.yml` on host port 3000. The repo root is bind-mounted read-only into the nginx html directory.

## Gotcha
The repo root directory can have `700` permissions after import, which makes nginx's non-root worker return 403. Fix with `chmod 755 .` before starting (or after restarting).

## Verify
- `curl -s -o /dev/null -w "%{http_code}" http://localhost:3000/` → 200
- All assets (manifest.json, sw.js, icon-*.png) should return 200
