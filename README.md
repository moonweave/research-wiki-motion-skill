# research-wiki-motion

Agent skill for semantic graph motion work in the `research-wiki` vault UI.

This is not a general animation-library skill. It captures the project's motion
contract for semantic graph demos, Instagram/Reels capture shots, and
Reels/Capture Mode implementation review:

- motion must explain graph relationships
- screen-level scan/glitch decoration is banned
- node/link/camera/HUD motion has explicit budgets
- candidate directions should be scored before deep implementation
- Playwright visual verification is part of the definition of done

## What It Is For

Use this skill when working on:

- `research-wiki` graph UI motion
- Reels/Capture Mode (`?capture=1`)
- semantic graph animations on nodes, links, camera, or HUD
- Instagram demo shots that need attention-grabbing but restrained motion
- review of graph motion regressions, visual overlap, or unverified polish

Do not use it as a substitute for a full animation-library reference such as
GSAP, Framer Motion, Motion One, or Anime.js.

## Install

```bash
npx skills add https://github.com/moonweave/research-wiki-motion-skill -g -y --copy
```

The installed skill should appear as `research-wiki-motion`:

```bash
npx skills list -g
```

## Use

Example prompts:

```text
Use $research-wiki-motion to compare three capture-mode motion directions.
```

```text
Use $research-wiki-motion to review the graph animation for Reels recording.
```

The skill guides the agent toward restrained, meaning-bound motion and requires
browser screenshots or runtime checks before claiming visual success.

## Repository Layout

```text
.
├── SKILL.md              # Agent-facing skill instructions
├── agents/openai.yaml    # UI metadata for skill listings
├── LICENSE               # MIT license
└── README.md             # Public repo overview
```

## Verification

Validate the skill package:

```bash
python /Users/choemun-yeong/.codex/skills/.system/skill-creator/scripts/quick_validate.py .
```

For `research-wiki` app changes made with this skill, follow the verification
checklist inside `SKILL.md`.

## License

MIT
