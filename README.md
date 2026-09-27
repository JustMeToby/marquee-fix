# Marquee Fix

A Codex skill for repairing continuously scrolling text or logo marquees that develop a blank tail or visibly jump back to the start. It applies to HTML/CSS and vanilla JavaScript marquees, especially when a short row is shown on a wide screen.

## What it does

The skill measures one complete row and the visible marquee width, then repeats the row until **each of two identical halves** covers the viewport. The track scrolls across one half and resets onto matching content. It also keeps the speed steady when content changes, updates the copies on resize, and makes the row manually scrollable for people who prefer reduced motion.

The [three-name example](marquee-fix/references/minimal-example.html) is a standalone HTML file you can open in a browser. It needs no build step or dependencies.

## Install

Publish the contents of this directory as the root of a GitHub repository. Then ask Codex:

> Use $skill-installer to install `https://github.com/OWNER/REPO/tree/main/`

Replace `OWNER/REPO` with your repository and `main` if its default branch has another name. If you commit the `for-github` directory inside a larger repository instead, use `.../tree/main/for-github/marquee-fix` as the URL path.

For a manual install, copy the entire `marquee-fix` folder into `$CODEX_HOME/skills/` (by default `~/.codex/skills/`). Keep its `SKILL.md`, `agents/`, and `references/` together. The skill is available to Codex on the next turn.

## Use

Ask Codex, for example:

> Use $marquee-fix to repair the infinite marquee on my page. Keep its current design and test the loop at mobile, desktop, and 5120px widths.

The [skill instructions](marquee-fix/SKILL.md) include the coverage formula, implementation guidance, and two sizing examples.
