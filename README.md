# research-wiki-motion

A small agent skill for motion work in the `research-wiki` vault UI.

It is not a general animation-library skill. It captures the project's motion
contract for semantic graph demos and Reels/Capture Mode:

- motion must explain graph relationships
- screen-level scan/glitch decoration is banned
- node/link/camera/HUD motion has explicit budgets
- candidate directions should be scored before deep implementation
- Playwright visual verification is part of the definition of done

## Install

```bash
npx skills add https://github.com/moonweave/research-wiki-motion-skill -g
```

Or copy directly into Codex:

```bash
mkdir -p ~/.codex/skills/research-wiki-motion
cp SKILL.md ~/.codex/skills/research-wiki-motion/SKILL.md
```

## Use

Ask for motion work in the research-wiki graph UI, Reels/Capture Mode, semantic
graph animation, or Instagram demo motion. The skill should guide the agent to
use restrained, meaning-bound motion and verify it with browser screenshots.

## License

MIT
