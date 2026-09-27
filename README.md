# Marquee Fix

Coding agents seem to like continuously scrolling text or logo marquees. I don't mind that in general, but I've noticed these marquees are often a little glitchy and develop a blank tail or visibly jump back to the start. Have a skill that should fix that.

## What it does

The skill adds a little Javascript that measures one complete row and the visible marquee width, then repeats the row until **each of two identical halves** covers the viewport. The track scrolls across one half and resets onto matching content. It also keeps the speed steady when content changes, updates the copies on resize, and makes the row manually scrollable for people who prefer reduced motion.

## Caveats

The skill was developed for pages using vanilla HTML, CSS, and JavaScript. It may need adaptation or fail on pages managed by frontend frameworks such as React. It has been tested with Codex only so far, but should work with any agent or harness that supports the Agent Skills format. Feedback about any problems or your own test results is very welcome!

## Install

### Option 1: skills.sh installer

```sh
npx skills add JustMeToby/marquee-fix
```

### Option 2: Manual install

Download the [repository](https://github.com/JustMeToby/marquee-fix) and copy the entire `marquee-fix` folder into your agent's skills directory. User-level directories often look like `~/.<agent>/skills/`; for example:
- Codex: `~/.codex/skills/marquee-fix/`
- Claude Code: `~/.claude/skills/marquee-fix/`
- Shared agent directory, where supported: `~/.agents/skills/marquee-fix/`

Check your agent's documentation if it uses a different skills directory.

## Use

Ask your agent, for example:

> Use the marquee-fix skill to repair the infinite marquee on my page. Keep its current design and test the loop at mobile, desktop, and high-resolution widths.

The [skill instructions](marquee-fix/SKILL.md) include the coverage formula, implementation guidance, and two sizing examples.

## License

MIT licensed. You are free to use, modify, and redistribute the skill, including commercially, under the [MIT license terms](https://opensource.org/license/mit).
