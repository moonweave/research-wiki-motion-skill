---
name: research-wiki-motion
description: |
  Use when designing, implementing, or reviewing motion for the research-wiki
  graph UI, especially Reels/Capture Mode, semantic graph animations, canvas
  node/link motion, Instagram demo shots, or visual polish that must stay
  meaningful and restrained. Pair with anneal when comparing multiple motion
  directions before implementation.
---

# Research Wiki Motion

Use this skill for motion work in the `research-wiki` vault UI, especially:

- Reels/Capture Mode (`?capture=1`)
- semantic graph animation in `apps/vault-ui/frontend/src/components/GraphView.tsx`
- HUD/caption motion in `apps/vault-ui/frontend/src/styles.css`
- short-form video demos where motion must attract attention without making the
  research tool feel gimmicky

## Core Rule

Motion must explain the graph. It must not decorate the screen.

Allowed motion attaches to one of these semantic surfaces:

- `node`: current concept spotlight, selected paper focus, degree/cluster emphasis
- `link`: manual link flow, similar-edge ignition, neighborhood bloom
- `camera`: restrained zoom-to-fit, macro-to-micro focus, no aggressive pans
- `HUD`: subtle metric/caption pulse, progress state, no full-screen effects

If a motion cannot answer "what research relationship does this reveal?", do not
add it.

## Hard Bans

Do not add:

- full-screen scan/sweep overlays
- glitch effects
- random decorative particles
- background flashes
- bokeh/orb decoration
- global node blinking
- fast camera whip/pan/zoom
- animations that affect normal graph mode when `captureMode` is false
- unverified "looks good" claims without screenshots

## Direction Choice

When choosing among two or more motion concepts, use `anneal`-style scoring
before implementing deeply.

Draft 2-3 candidates and score each on the same fixture, normally:

| Question | Scale |
| --- | --- |
| First-2-second hook: is visible change obvious in a silent vertical clip? | 0/1/2 |
| Research value: does the viewer understand what the product helps them do? | 0/1/2 |
| Semantic attachment: is motion bound to nodes, links, graph scope, or query flow? | 0/1/2 |
| Restraint: does the graph remain readable without screen-level decoration? | 0/1/2 |
| Capture stability: do HUD/caption/graph avoid overlap at mobile and 9:16 sizes? | 0/1/2 |
| Runtime health: console, page errors, failed requests, and bad responses are empty | pass/fail |

Pick by the score. Use taste only to break a near tie.

## Preferred Patterns

Use these before inventing new effects:

- **Concept Spotlight**: one or two soft rings from the current concept node.
- **Link Bloom**: particles along links touching the current node during local expansion.
- **Similar Edge Ignite**: brighter particles only on `kind === "similar"` edges.
- **Core Collapse**: fade/filter low-degree satellites, keep backbone readable.
- **Macro-to-Micro Focus**: restrained zoom/focus from global cluster map to one concept.
- **Workflow Narrative**: search/select concept -> local neighborhood -> similar links.

Keep durations slow enough for a phone recording: no critical phase under 2.5s.

## Implementation Guardrails

Before editing functions/classes, follow the repo's GitNexus impact rule.

For `GraphView.tsx`:

- Prefer canvas-local helpers such as `drawCaptureSpotlight()` and
  `captureLinkParticleCount()`.
- Keep motion behind `captureMode` or a capture-step condition.
- Preserve existing drag-end pinning behavior: only user drag should set `fx/fy`.
- Do not auto-pin nodes just to make a shot stable.
- Avoid adding animation dependencies unless DOM/SVG timeline work clearly needs one.

For `styles.css`:

- Keep capture layout fullscreen and quiet.
- HUD/caption may pulse subtly.
- Never reintroduce `.capture-graph::before` screen sweeps or `captureSweep`.
- Ensure hidden controls also have `pointer-events: none` in capture mode.

For `App.tsx`:

- Keep `?capture=1` shareable and reproducible.
- Provide an exit path (`Exit` and/or `Esc`) if capture mode is user-entered.
- Do not make capture mode the default app experience.

## Verification Checklist

Run the smallest applicable set, then broaden if the change is shared:

```bash
cd apps/vault-ui/frontend
npm run test:graph-physics
npm run build
npm run test:smoke
```

For runtime visual checks, start the app and capture at least:

- normal graph mode: controls visible, capture styles absent
- `?capture=1`, 9:16 viewport: global/local/similar/final stages
- mobile-width viewport if adding controls or HUD changes

The browser check must record:

- `consoleErrors: []`
- `pageErrors: []`
- `failedRequests: []`
- `badResponses: []`
- canvas is nonblank
- no text/HUD/caption overlap
- no full-screen scan/sweep animation

If the change touches backend static serving or repo-wide code, also run:

```bash
uv run pytest
npx gitnexus detect-changes
git diff --check
```

## Review Stance

Findings first. Treat visual success as evidence-backed, not assumed.

Report:

- screenshots or paths to captured PNGs
- exact commands run
- whether ordinary graph mode still behaves normally
- remaining visual risk, especially if final judgment needs human review
