# Lineage Proof — reproducibility, measured

A single-file pitch deck for **Lineage Proof**, the meter for agent reproducibility:
replay an agent's input, measure how often it reproduces, and attribute the
divergence to the layer that caused it (skill version · KB chunk · API · model).

Built as a self-contained `index.html` — **React 18 + Framer Motion** loaded via ESM
import-maps and in-browser Babel, so it runs with no build step.

## View it

Live on GitHub Pages → https://chanman22git.github.io/lineage-proof/

## Run locally

Serve over HTTP (ESM import-maps don't load reliably from `file://`):

```bash
python3 -m http.server 8011
# then open http://localhost:8011/
```

## Presenter controls

| Key | Action |
| --- | --- |
| `←` `→` / `Space` | Navigate slides |
| `T` | Rehearsal timer (target 3:00) |
| `P` | Presenter notes |
| dots (right edge) | Jump to any slide |

Respects `prefers-reduced-motion`. Requires network access for the CDN-hosted
libraries (React, Framer Motion via esm.sh) and Google Fonts.
