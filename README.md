# Lineage Proof: reproducibility, measured

A single-file pitch deck for "the meter for agent reproducibility": replay an agent's input, measure how often it reproduces, and attribute any divergence to the layer that caused it.

**Live:** https://chanman22git.github.io/lineage-proof/

> **This is the earlier version of the idea that became [Invara](https://github.com/Chanman22git/Invara)** ([live](https://chanman22git.github.io/Invara/)).
> Lineage Proof proposed *replaying* agent inputs to measure reproducibility. Invara reworked the concept to read reproducibility straight from traces that agents already emit, scored per intent, without re-running the agent. Invara also adds an interactive dashboard mockup. This repo is kept as the record of the first iteration.

## Executive summary

- **What it is:** a 9-slide, roughly three-minute pitch deck for **Lineage Proof**, a proposed tool that gives AI-agent teams a number they have never had: their agents' **reproducibility rate**.
- **Who it's for:** engineering and AI-platform leaders who guide agents with skills and knowledge bases and currently accept inconsistent output as "the model is just non-deterministic".
- **Status:** archived concept. It is a pitch artefact, not a working product, and it was superseded by [Invara](https://github.com/Chanman22git/Invara).
- **Core idea:** *replay → diff → attribute.* Run the same input twice, compare the two traces, and flag which layer drifted (skill version, KB chunk, API response, or model randomness).
- **Technical highlights:** one self-contained `index.html` using React 18 and Framer Motion, loaded through an ES module import map and in-browser Babel, so there is no build step. It includes presenter tooling (rehearsal timer, speaker notes, slide dots) and respects `prefers-reduced-motion`.

## The pitch, slide by slide

| # | Slide | Point it makes |
|---|---|---|
| 0 | Cold open | *Lineage Proof: the meter for agent reproducibility.* It is framed as pillar one of an AI trustworthiness initiative, built on EvalLib, Phoenix and OpenTelemetry. |
| 1 | The unmeasured failure mode | Nobody can state their agents' reproducibility rate. Shrugging it off as non-determinism is a normalised failure mode. |
| 2 | Where this sits | Of the trustworthiness pillars (reliability, validity, safety, security, accountability, explainability, privacy, fairness), reproducibility is the precondition. Without it, the others can't be measured on an agent. |
| 3 | The wedge | Sell the **meter**, not the diagnosis: "You don't know your reproducibility rate. Here's the instrument that produces it." |
| 4 | How it works | Five steps: **Replay** (capture two lineages via Phoenix), **Diff**, **Attribute** the drifting layer, **Aggregate** a consistency % across a test suite, and **Alert** when it drops below a threshold. |
| 5 | Why drift is actionable | In a skill- and KB-guided setup, the divergence that remains is mostly controllable infrastructure drift, which can be attributed and fixed. |
| 6 | Honest scope | Owns reliability and accountability via lineage. Does **not** claim correctness or security: a reproducibly wrong agent scores 100%. |
| 7 | The demo | A gauge set up to show a reproducibility number measured live on stage. |
| 8 | Close | "We establish the reproducibility floor that makes every other trustworthiness measurement possible." |

The on-screen visuals are illustrative. The gauge's arc stops at a fixed visual position, and its readout shows a placeholder (`▮▮.▮%`) rather than a claimed figure. The attribution bar chart is labelled "illustrative shape".

## Features

- **Scroll-snapping slides** with Framer Motion entrance animations (staggered reveals, SVG path drawing for the hero "fork" and the mechanism diagram).
- **Presenter controls:**

  | Key | Action |
  | --- | --- |
  | `→` / `PageDown` / `Space` | Next slide |
  | `←` / `PageUp` | Previous slide |
  | `Home` / `End` | First / last slide |
  | `T` | Rehearsal timer. Turns to a warning at 2:45 and to over-time at 3:00. |
  | `P` | Presenter notes panel |
  | Dots (right edge), `‹` `›` buttons | Jump to any slide, or step through the slides |

- **Per-slide timing budget** (`META` in `index.html`) that adds up to about 3 minutes 14 seconds, with speaker notes for each slide (`NOTES`).
- **Reduced motion:** with `prefers-reduced-motion`, paths render fully drawn, the gauge settles instantly, and looping pulses stop.

## How it's built

```
index.html
 ├── <script type="importmap">  → react, react-dom/client, framer-motion (esm.sh)
 ├── @babel/standalone (jsDelivr) → transpiles the inline JSX in the browser
 ├── <style>                     → the whole deck's CSS (design tokens, layout, slides)
 └── <script type="text/babel">  → App, Slide, HeroFork, Pillars, AttribFig, Gauge,
                                   AttribBars, Dots, Timer + META / NOTES data
```

## Tech stack

- React 18.3.1 and ReactDOM (from esm.sh)
- Framer Motion 11.11.0 (from esm.sh)
- Babel standalone 7.25.6 (from jsDelivr), for in-browser JSX
- Google Fonts
- GitHub Pages

## Project structure

```
lineage-proof/
├── index.html   # The entire deck: markup, CSS, JSX, slide data and speaker notes
└── README.md
```

## Running locally

Serve the folder over HTTP, because ES module import maps don't load reliably from `file://`:

```bash
git clone https://github.com/Chanman22git/lineage-proof.git
cd lineage-proof
python3 -m http.server 8011
# open http://localhost:8011/
```

An internet connection is required, because React, Framer Motion, Babel and the fonts load from CDNs.

## Deployment

GitHub Pages is configured in **"Deploy from a branch"** mode: branch `main`, folder `/` (root). The repo has no GitHub Actions workflow. Pushing to `main` republishes the deck.

## Known limitations

- **Superseded.** Active work on this idea continues in [Invara](https://github.com/Chanman22git/Invara).
- **Concept only.** There is no replay, diff or attribution engine in this repo. The live-demo slide is a staged gauge.
- **Runtime CDN dependencies.** In-browser Babel and CDN imports suit a pitch deck, not production use.

## Author

**Chandru** ("BuiltByInstincts"), Product & Data Builder, Bengaluru. I build products at the intersection of AI, data, and human behaviour.

- Portfolio: https://chanman22git.github.io/builtbyinstincts/
- LinkedIn: https://linkedin.com/in/chandrasekarv22
