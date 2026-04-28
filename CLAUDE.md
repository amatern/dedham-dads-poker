# CLAUDE.md

This file is read automatically by Claude Code at the start of every session in this repo. It carries the persistent project context so we don't have to re-explain on each session.

## What this project is

This is a fork of [Tehes/poker](https://github.com/Tehes/poker), a static-site Texas Hold 'Em practice table. We are **re-skinning it** for Dedham Dads — a group of dads in Dedham, MA who play occasional poker nights together.

The original app is functional and well-built. We are not improving the code, adding features, or refactoring. We are changing how it looks so it feels like a Dedham Dads artifact instead of a generic poker app.

## What this project is NOT

- **Not** a feature project. Don't add new game modes, AI improvements, multiplayer, persistence, accounts, or anything that wasn't already in the upstream repo.
- **Not** a code refactor. Don't restructure JavaScript, change build tooling, or "improve" the architecture.
- **Not** a fork that diverges aggressively from upstream. We want to be able to pull future bug fixes or improvements from `Tehes/poker` cleanly. That means our changes should be confined to styling, copy, and assets — not core game logic.

## Hard rules

- **Do not touch `/js/`** unless absolutely required for a styling fix. The bots and game logic live there. If you find yourself wanting to edit a `.js` file, stop and ask first.
- **Do not add new features.** If you have an idea, mention it but don't build it.
- **Do not change responsive breakpoints** unless something is actually broken on a real device.
- **Preserve all upstream functionality.** Cards still play, bots still bot, hands still resolve correctly.
- **Use CSS variables consistently.** The original codebase uses CSS custom properties; the re-skin should too. Define palette in `:root` and reference variables everywhere.
- **No new dependencies.** No new fonts beyond what's in the existing `<link>` tags or what we explicitly add to match the cheat sheet. No new JS libraries.

## Who Dedham Dads are

Context to inform design judgment, not to recite back to the user:

Dedham Dads are a friendship group with a public face. Core group of dads in Dedham, MA who share stories, hang out at favorite pubs, take Town Meeting seriously, and occasionally sponsor each other's kids' fundraisers and 5Ks. They host "Thirsty Third Thursday" to welcome new dads. The group is **pub-based and in-person, not digital-first** — the website (and this poker app) are public faces, not where the group's life actually happens.

This means the re-skin should feel **convivial and grown-up**, not slick or corporate. Think "wood-paneled pub at a friend's poker night," not "online casino" or "professional poker training tool." Warmth over flash. Type over decoration.

## Where this deploys

- **Live homepage:** https://dedhamdads.org/ (separate repo, not this one)
- **Cheat sheet (already deployed):** https://dedhamdads.org/poker/ — Texas Hold 'Em rules and house rules for poker night, with a "felt table" aesthetic (green felt background, cream/gold/crimson palette, ornate serif fonts)
- **This app deploys to:** https://dedhamdads.org/poker/play/ — the practice table

The cheat sheet (`/poker/`) and the practice table (`/poker/play/`) should feel like **the same room** — both are poker night artifacts, both should share a visual identity. The homepage at `/` is intentionally a different room (Pub Warmth, civic, front-door).

## Visual system — match the cheat sheet

The cheat sheet establishes the aesthetic for `/poker/*`. Match it. Specifically:

### Palette (CSS variables — port these to this project)

```css
--felt: #0d4d2c;
--felt-dark: #073d20;
--felt-light: #145d36;
--cream: #f4ead5;
--cream-soft: #ebe0c7;
--gold: #d4a843;
--gold-bright: #f0c659;
--crimson: #8b1a1a;
--crimson-deep: #5c0e0e;
--ink: #1a1208;
--paper: #f5ecd4;
```

- **Felt greens** = backgrounds, table surfaces, primary brand color for this section
- **Cream/paper** = text on dark, surfaces on light
- **Gold** = accents, highlights, important UI ("your turn," call-to-action buttons)
- **Crimson** = secondary accent, danger/fold actions, the maroon thread that ties /poker/* back to the rest of the Dedham Dads identity (homepage uses #8B2635 maroon — the cheat sheet's #8b1a1a crimson is the same family)
- **Ink** = body text on cream backgrounds

### Typography (match cheat sheet)

The cheat sheet uses these Google Fonts:
- **Playfair Display** — display headings, dramatic serif
- **IM Fell English** — body text, vintage book-print feel
- **Special Elite** — accent typewriter font for tags/labels
- **UnifrakturCook** — used sparingly for the most ornate moments (avoid going overboard)

Pair them the way the cheat sheet does: Playfair for big moments, IM Fell English for body, Special Elite for small labels/tags.

### Visual register

- **Felt table backgrounds** — radial gradient greens, subtle dot texture (see cheat sheet's `body::before` for reference)
- **Vignette** — soft darkening at edges, focuses attention on the action
- **Ornate but not garish** — Victorian poker-room, not Vegas-strip
- **Restrained gold** — gold for emphasis only, not everywhere; one or two gold elements per screen
- **Cards should feel like real cards** — cream/paper backgrounds for cards, sharp suit colors

## Coordination references

- The cheat sheet HTML lives in the user's local at `C:\Users\amate\OneDrive\DedhamDadsPoker\index.html` (loose file, not in this repo). View it for design reference when in doubt about palette/type/feel.
- The cheat sheet is also live at https://dedhamdads.org/poker/ — view it in browser to see the target aesthetic.

## Working environment

- User: Andreas Matern (GitHub: amatern)
- OS: Windows, working in PowerShell
- Local repo path: `C:\Users\amate\OneDrive\<this-repo-name>`
- Deploys via: manual upload to pawnhoster cPanel (no CI/CD)
- User is comfortable with Git basics; appreciates step-by-step guidance for complex workflows

## Commit conventions

Use conventional commits: `feat:`, `fix:`, `style:`, `refactor:`, `docs:`, `chore:`. Most commits in this re-skin will be `style:` since that's the whole job. Example: `style: port felt-table palette to CSS variables`.

## When in doubt

- Ask before changing anything in `/js/`
- Ask before adding new dependencies or fonts
- Ask before diverging from the cheat sheet's established aesthetic
- Default toward less change, not more
