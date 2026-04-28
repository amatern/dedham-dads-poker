# PROJECT_PLAN.md — Dedham Dads Poker Re-skin

Three sessions. Don't try to do them all at once. Between sessions: commit your work, run the app, click through it, take a break.

## Goal

Re-skin the upstream Tehes/poker fork so it feels like a Dedham Dads artifact — specifically, like an extension of the cheat sheet at https://dedhamdads.org/poker/. Same room, different activity.

**Out of scope for all three sessions:** new features, refactoring, JS changes, responsive breakpoint changes, accessibility overhauls. Re-skin only.

---

## Session 1 — Foundation: palette, fonts, and the table

**Goal:** Get the core visual system in place. After this session, the table should look like Dedham Dads even if details are rough.

### Concrete deliverables

1. **Port the felt-table palette into `css/style.css` as CSS variables** in `:root`. Use the same variable names the cheat sheet uses (`--felt`, `--cream`, `--gold`, etc.) so they're consistent across `/poker/*`.

2. **Replace the existing color values throughout the stylesheet with variable references.** Don't introduce new colors — only use the variables you defined.

3. **Update font imports.** Replace existing Google Fonts `<link>` in the HTML files (`index.html`, `hole-cards.html`, `remoteTable.html`) with the cheat sheet's font set: Playfair Display, IM Fell English, Special Elite. Drop fonts the original used that we don't need.

4. **Apply font families across the app's text styles.** Headings → Playfair Display. Body/UI → IM Fell English. Small labels/tags → Special Elite.

5. **Style the table itself.** The play surface should be felt green with the radial gradient and subtle texture from the cheat sheet (see `body::before` in the cheat sheet HTML). Add the vignette via `body::after`.

### Acceptance criteria

- [ ] All colors in `css/style.css` reference CSS variables, no raw hex values left behind
- [ ] Three font families loaded, applied consistently across the app
- [ ] Table background is felt green with proper depth (gradient + texture + vignette)
- [ ] Game still plays correctly — bots still bot, hands still resolve, cards still flip
- [ ] No JS changes
- [ ] Visual feels like a relative of the cheat sheet, not the original generic skin

### Commit

`style: establish felt-table palette and typography`

---

## Session 2 — Cards, chips, and the UI furniture

**Goal:** The pieces *on* the table should match the table. After this session, every visual element of the game should feel intentional.

### Concrete deliverables

1. **Cards.** Cream/paper backgrounds (`--cream` or `--paper`). Crimson for hearts/diamonds, ink for spades/clubs. Subtle border so cards have edges. The cards in the original feel sterile; ours should feel like real cards on a felt table.

2. **Chips.** If the original has chips rendered, give them a Dedham Dads vibe — gold for high-value, crimson for mid, cream for low (or whatever color logic makes sense given how chips are currently rendered). Use the cheat sheet's chip values as reference: White 25, Red 100, Green 500, Black 1000.

3. **Buttons & controls.** All in-game buttons (Bet, Call, Raise, Fold, Check, All-in) should use the palette consistently. Suggested mapping:
   - **Primary actions (Bet, Raise, Call):** gold accent on felt-dark background
   - **Destructive (Fold):** crimson
   - **Passive (Check):** cream/muted
   - **Big move (All-in):** crimson-deep with gold border or similar emphasis

4. **Modals, dialogs, overlays.** If the game has any (welcome screen, end-of-hand summary, settings), restyle them to match. Cream paper-style backgrounds, ink text, gold accents.

5. **Player avatars / labels.** If the game shows bot names or player labels, restyle the typography to match (Special Elite for labels, Playfair for player names).

### Acceptance criteria

- [ ] Cards feel like physical cards on a felt table
- [ ] All buttons follow a consistent visual hierarchy keyed to the action's semantic meaning
- [ ] Any modals/dialogs match the rest of the app
- [ ] Hover/active states are styled (don't leave default browser blue)
- [ ] No element looks "left behind" from the original skin
- [ ] Game still plays correctly

### Commit

`style: re-skin cards, chips, and controls`

---

## Session 3 — Polish, copy, and metadata

**Goal:** Ship-ready. After this session, deploy to https://dedhamdads.org/poker/play/.

### Concrete deliverables

1. **Page copy / branding.** Replace any "Tehes Poker" or generic strings with "Dedham Dads Poker" or similar. Update:
   - `<title>` tags in `index.html`, `hole-cards.html`, `remoteTable.html`
   - `<meta name="description">` — something like "Practice Texas Hold 'Em — Dedham Dads Poker Night"
   - Any visible "welcome" or "about" copy in the app
   - Footer if there is one

2. **Meta tags for sharing.** Update Open Graph tags so when the URL is shared in iMessage/Slack/wherever, it previews nicely:
   - `og:title` — "Dedham Dads Poker — Practice Table"
   - `og:description` — same as meta description
   - `og:url` — `https://dedhamdads.org/poker/play/`
   - `og:type` — `website`
   - `theme-color` — `#0d4d2c` (the felt green)

3. **Canonical URLs.** Update `<link rel="canonical">` in all three HTML files to `https://dedhamdads.org/poker/play/`.

4. **Manifest.** Update `manifest.json`:
   - `name` — "Dedham Dads Poker"
   - `short_name` — "DD Poker"
   - `theme_color` — `#0d4d2c`
   - `background_color` — `#073d20`
   - `start_url` — `/poker/play/`

5. **Favicon.** If time allows and a quick win is available — replace with something simple and Dedham Dads-flavored (a card suit, a chip, a pair of letters). If no quick win, leave for designer dad later. Don't burn the session on this.

6. **Footer link back to the cheat sheet.** Small link at the bottom: "Need a refresher? → Cheat Sheet" pointing to `/poker/`. This is the one *new* element being added; it justifies itself because the two pages are siblings and discovery between them matters.

7. **Final pass.** Click through the whole app one more time. Play a hand. Check mobile. Look for anything that still feels "left behind" from the original skin.

### Acceptance criteria

- [ ] No "Tehes" or generic poker references visible anywhere in the UI
- [ ] All meta tags reflect Dedham Dads identity and the `/poker/play/` URL
- [ ] Manifest is updated
- [ ] OG preview will look good when shared
- [ ] Footer links back to the cheat sheet at `/poker/`
- [ ] Mobile and desktop both look right
- [ ] Game still plays correctly

### Commit

`style: finalize copy, meta tags, and manifest for deploy`

---

## After Session 3 — Deploy

The app is static files. To deploy:

1. **Locally test once more.** Open `index.html` in a browser, play a hand. Resize for mobile.
2. **Upload to pawnhoster via cPanel.** Create a `play/` folder inside the existing `/poker/` directory on the server. Upload all the repo files (except `.git/`, `README.md`, `agents.md`, the planning files) into `/poker/play/`.
3. **Verify** at https://dedhamdads.org/poker/play/.
4. **Update the homepage** (separate repo `dedhamdads-org`) to add a link card or nav item pointing to the practice table. The current homepage's "Open the table →" card on the poker section should now route to the cheat sheet (`/poker/`) which is correct, but a new link or update may make sense to surface the practice table.
5. **Update the cheat sheet** to link out to the practice table ("Practice your game → /poker/play/"). This requires editing the cheat sheet HTML, which lives in `C:\Users\amate\OneDrive\DedhamDadsPoker\index.html` and is deployed at `dedhamdads.org/poker/`.

---

## Style notes that apply to all sessions

- **Use CSS variables.** Always.
- **Don't add features.** Re-skin only.
- **Don't touch `/js/`.** If you think you need to, ask first.
- **When in doubt, look at the cheat sheet.** It's the source of truth for what `/poker/*` should feel like.
- **Conventional commits.** Most commits will be `style:`.
