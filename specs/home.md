# Home / Workspace page body — Figma spec

Source: fileKey `tYohAsCRA9yni6rBCKi5QJ`, node `2458:43293` ("content"), 1920 × 968, sits directly below the app header.
Reference renders: `assets/icons/home-background.png` (background only, 1920×968).

Font everywhere: **Montserrat** (weights 400 Regular, 500 Medium, 500 Medium Italic, 600 SemiBold).
Shared shadow token "Default Shadow": `box-shadow: 0 2px 7px 0 rgba(0,125,171,0.10)` (#007DAB1A).

## Color tokens used

| token | hex |
|---|---|
| text/primary | #363B4D |
| text/secondary (also icon/secondary) | #5F6475 |
| text/accent | #8D99AE |
| text/blue, icon/primary | #007FAD |
| text/on-primary | #FFFFFF |
| background/primary | #FFFFFF |
| background/secondary (progress track) | #F4F6FB |
| border/border | #CED0D4 |
| component/button-secondary, interaction/hover-black | #F2F3F7 |
| status/error | #ED4B52 |
| status/warning | #FF7C19 |
| status/success | #94CC86 |
| color/red/600 | #A4495D |
| color/red/700 | #7B3746 |
| color/purple/800 | #2B376B |
| color/blue/500 | #87CFE7 |

## Text styles (Figma styles)

| style | weight | size / line-height | letter-spacing |
|---|---|---|---|
| header/large | 500 | 32 / 40 | 0 |
| title/large | 600 | 18 / 24 | 0 |
| title/medium | 600 | 16 / 20 | 0.15px |
| title/small | 600 | 14 / 18 | 0.1px |
| body/large/regular | 500 | 16 / 20 | 0.5px |
| body/medium/regular | 500 | 14 / 18 | 0.25px |
| body/medium/semibold | 600 | 14 / 18 | 0 |
| body/medium/italic | 500 italic | 14 / 18 | 0.25px |
| body/medium/accent | 400 | 14 / 18 | 0 |
| body/small/regular | 500 | 12 / 14 | 0.4px |
| body/small/accent | 400 | 12 / 14 | 0 |

---

## 1. Page container + background

- Container (`content`): `display:flex; flex-direction:column; gap:48px; padding:40px 100px; width:1920px; height:968px; position:relative;` → content width 1720px. No max-width defined in Figma (fixed 1920 frame).
- **Background** (`2728:10242`): absolutely positioned layer behind everything, `left:50%; transform:translateX(-50%); top:0; width:1920px; overflow:hidden` (Figma frame is 1458 tall, but only the top 968 is visible).
  - Base fill (stacked, top first):
    `linear-gradient(180deg, #FFFFFF 11.621%, #F0FBFF 60.577%, #FDFDFD 81.25%), linear-gradient(90deg, #F2F3F7 0%, #F2F3F7 100%)` — i.e. effectively the white→#F0FBFF→#FDFDFD vertical gradient (the top layer is opaque, the #F2F3F7 layer is hidden beneath it).
  - Two large soft "wave" shapes (SVG, 36% fill-opacity linear gradients):
    - `home-bg-wave-back.svg` (2923.94 × 2123.5, gradient #D7ECF3 → white/0): wrapper box `position:absolute; left:-558px; bottom:-1112.51px; width:3145.967px; height:2441.509px; display:flex; align-items:center; justify-content:center` → inner img 2923.935 × 2123.5, `transform: rotate(6.51deg)`.
    - `home-bg-wave-front.svg` (2802.91 × 2001.84, gradient #87CFE7 → white/0): wrapper `left:-318px; bottom:-1266.77px; width:2959.39px; height:2227.574px` (flex-centered) → inner img 2802.907 × 2001.837, `transform: rotate(-4.76deg)`.
    - (bottom offsets are relative to the 1458px-tall background frame.)
  - Top-right diagonal hatching (two groups of thin lines, fill #BCC4E8, opacity 0.7 nested twice): `home-bg-lines-a.svg` / `home-bg-lines-b.svg` (each ~665 × 663, **5.8 MB each** — very heavy). Wrappers: A `right:-607.44px; bottom:1026.06px; 839.342×838.287`, B `right:-459.99px; bottom:732px; 839.323×838.28`, inner `transform: scaleY(-1) rotate(161.63deg)`, opacity .7. Only a faint corner of these is visible (top-right ~350×420px area).
  - Two more line groups (bottom-left, node 1190:2147) are positioned entirely outside the visible area — skip.
  - **Recommendation:** use `home-background.png` (1920×968, a flattened render of exactly this visible background) as `background: url(home-background.png) top center / 1920px 968px no-repeat, #FDFDFD` instead of rebuilding the layers. If the viewport is wider than 1920, centre it; if taller, fill below with #FDFDFD (bottom edge of PNG is ~#E9F6FB/#D9EFF7 on the right — consider `background-size: cover`).

## 2. Content header (`2588:6053`)

`display:flex; justify-content:space-between; align-items:flex-end; width:100%` (height 76).

- Left column `welcome text`: flex column, gap 16px, nowrap.
  - `Hi, John!` — Montserrat 500, 32px / 40px, ls 0, #363B4D.
  - `Here’s what’s going on today.` (curly apostrophes U+2019) — Montserrat 600, 16px / 20px, ls 0.15px, #5F6475.
- Right: icon button (interactive) 36 × 36, bg #F2F3F7, radius 4px, padding 0 4px, centered; icon `home-settings.svg` 24×24 (gear, fill #5F6475). No text.

## 3. Content cards area (`2458:43300`)

Flex column, gap 24px, width 100% (1720), fills remaining height; children: top row, bottom row.

### 3a. Top row cards (`2458:43301`)

`display:flex; gap:24px; align-items:center`. 4 cards, each ends up **412px wide** (Due Soon is fixed 412; the other three are `flex:1` = (1720 − 3·24 − 412)/3 = 412). Card height 94.

Common card (all 4 — look like clickable "button cards"):
- `background:#FFFFFF; border:1px solid #CED0D4; border-radius:8px; box-shadow:0 2px 7px 0 rgba(0,125,171,0.10); padding:16px 24px; display:flex; align-items:center; gap:24px; overflow:hidden`.
- Icon tile: 48 × 48, radius 4px, padding 4px, icon 40 × 40 (white fill) filling it.
- Text block: flex column, left aligned, nowrap:
  - Label: Montserrat 500, 16px / 20px, ls 0.5px, #5F6475.
  - Number: Montserrat 500, 32px / 40px, ls 0, #363B4D.

| # | node | tile bg | icon asset | label | number |
|---|---|---|---|---|---|
| 1 | 2532:23094 (High Priority) | #ED4B52 | `home-card-priority.svg` (warning triangle) | `High Priority Tickets` | `9` |
| 2 | 2585:14297 (Due Soon) | #FF7C19 | `home-card-due-soon.svg` (clock) | `Tickets Due Soon` | `17` |
| 3 | 2920:20454 (Closed Today) | #007FAD | `home-card-closed-today.svg` (clipboard list) | `My Tickets Closed Today` | `5` + progress |
| 4 | 2532:23133 (Mentions) | #A4495D | `home-card-mentions.svg` (chat bubble) | `Mentions` | `4` |

**Card 3 "My Tickets Closed Today" details** — text block is `flex:1` (fills to card's right padding):
- Row 1: label as above.
- Row 2 `lower text`: `display:flex; align-items:center; gap:24px; width:100%`
  - `5` — 32/40, 500, #363B4D, fixed width 19px, centered.
  - Progress group: `flex:1; display:flex; align-items:center; gap:8px`
    - Track: `flex:1; height:12px; background:#F4F6FB; border-radius:8px; overflow:hidden; position:relative` (≈187px wide at 412 card).
    - Fill: `position:absolute; left:0; top:50%; translateY(-50%); height:12px; width:48.2px; background:#94CC86` (no own radius; clipped by track's 8px radius → left end rounded, right end square). 48.2/187 ≈ **25.8%** → use **25%** (5 of 20).
    - `15 to go!` — Montserrat 500, 12px / 14px, ls 0.4px, #8D99AE, nowrap.

### 3b. Bottom row (`2458:43338`)

`display:flex; gap:24px; align-items:flex-start; flex:1`. Two cards, both **height 648px**.

---

## 4. My To-Do List card (`2881:25463`)

- `width:1284px; height:648px; background:#FFFFFF; border:1px solid #CED0D4; border-radius:8px; box-shadow:0 2px 7px 0 rgba(0,125,171,0.10); padding:16px; display:flex; flex-direction:column; gap:16px; overflow:hidden` (list content is clipped at the bottom — last card is cut off; implement as `overflow-y:auto` for a scrollable list).

### Top title bar
`display:flex; justify-content:space-between; align-items:center; padding:0 8px; width:100%` (height 36).
- Left: `title + counter` flex, gap 8px, align center:
  - `My To-Do List` — Montserrat 600, 18px / 24px, #363B4D.
  - `(10)` — Montserrat 500, 14px / 18px, ls 0.25px, #5F6475.
- Right `Filtering options`: flex, gap 16px, align center:
  - Filter = **two checkboxes** (variant "checkbox" of the Filter Dropdown component; NOT a dropdown), flex gap 16px:
    - Each: flex, gap 8px, align center; checkbox icon `home-checkbox-checked.svg` 24×24 (checked, #007FAD rounded square w/ white check, glyph 18×18 inside 24 box); label Montserrat 500, 14px / 18px, ls 0.25px, #5F6475.
    - Labels: `Tickets`, `Checklist Items`. Both checked. Interactive (toggle).
  - Sort button: 36 × 36, bg #F2F3F7, radius 4px, padding 0 4px, icon `home-sort.svg` 24×24 (#5F6475). Interactive.
  - (A hidden "Filters" dropdown variant exists in the component — button bg #F2F3F7, radius 4, height 32, width 118, padding 0 8px, `home-filter.svg` 20px + `Filters` 14/18 500 #5F6475 + `home-filter-chevron.svg` 20px; its menu is white, radius 4, Default Shadow, items padding 8px 16px with checkbox + label `Tickets` / `Checklist Items`. **Not shown in this design.**)

### Ticket list
`display:flex; flex-direction:column; gap:12px; width:1252px`.

**Ticket card (common):** `background:#FFFFFF; border:1px solid #CED0D4; border-radius:8px; padding:12px 16px; width:100%`. Cards with sub-rows are `flex-direction:column; gap:8px`. Rows look clickable (card 3 is shown in hover state).

**Top row:** `display:flex; justify-content:space-between; align-items:center; width:100%` with 4 children:
1. Number + title group: flex, gap 8px, align center:
   - Ticket number — Montserrat 500, 14px / 18px, ls 0.25px, **#007FAD**, fixed width **75px**.
   - Title — Montserrat 600, 14px / 18px, ls 0, #363B4D, fixed width **500px**.
2. Created date (nowrap, two runs + a space):
   - `Created at` — Montserrat 400, 12px / 14px, ls 0, #5F6475
   - ` ` (space, 14px)
   - `4/04/24 10:00 AM` — Montserrat 500, 12px / 14px, ls 0.4px, #363B4D
3. Status: `display:flex; gap:10px; align-items:center; padding:2px 8px; border-radius:4px;` **no background, no border**; both texts #363B4D, 12px:
   - `Status` — 400, 12 / 14, ls 0
   - `To Do` — 500, 12 / 14, ls 0.4px
4. Avatar: 20 × 20 circle (`border-radius:100px`), bg per row, initials Montserrat 600, 8px, line-height normal, ls 0.1px, #FFFFFF, centered.

**Divider** (only in cards with sub-rows): 1px line `#F2F3F7`, full width (`home-divider-todo.svg`, 1220×1 — or just `border-top:1px solid #F2F3F7`).

**Sub-row (checklist item):** `display:flex; justify-content:space-between; align-items:center; width:100%`:
- Left: flex gap 8px, align center: `home-checklist.svg` 16×16 (orange #FFA630) + text Montserrat 500, 12px / 14px, ls 0.4px, #5F6475, nowrap.
- Right (optional): 20px avatar as above.

**Rows, in order (verbatim):**

| # | number | title | card bg | top-row avatar | sub-rows |
|---|---|---|---|---|---|
| 1 | `54983` | `Login page not loading for some users` | #FFFFFF | JD #7B3746 | divider; `Check permissions and assign to IT` (no avatar) |
| 2 | `46467` | `Card declined but funds were deducted` | #FFFFFF | JD #7B3746 | — (single row, no gap) |
| 3 | `3467` | `App crashes when uploading a file` | **#F2F3F7** (hover state) | CA #2B376B | divider; `Test in beta environment` + JD #7B3746; `Send to development if issue is confirmed` + JD #7B3746 |
| 4 | `43646` | `Request to upgrade membership` | #FFFFFF | JD #7B3746 | — |
| 5 | `5678` | `Transfer ownership of account` | #FFFFFF | JD #7B3746 | — |
| 6 | `54353` | `App crashes when uploading an image` | #FFFFFF | JD #7B3746 | — |
| 7 | `76532` | `Is there a sandbox environment?` | #FFFFFF | JD #7B3746 | — |
| 8 | `54365` | `App isn’t loading` (U+2019) | #FFFFFF | JD #7B3746 | divider; `Send to development if issue is confirmed` + JD #7B3746 |
| 9 | `#543643` | `Login page not loading for some users` | #FFFFFF | JD #7B3746 | — (clipped by card bottom) |

All rows: created `Created at 4/04/24 10:00 AM`, status `Status` / `To Do`.
Single-line card height = 12+18+12+2 = 44px.

---

## 5. Recent Activity card (`2836:42420`)

(Figma title is **"Recent Activity"**, not "Yesterday's Work".)

- `width:412px; height:648px; background:#FFFFFF; border:1px solid #CED0D4; border-radius:8px; padding:16px; display:flex; flex-direction:column; gap:16px; overflow:hidden` — **no box-shadow** in Figma (unlike the To-Do card; likely an oversight — add Default Shadow if you want parity).
- Title row: `Recent Activity` — Montserrat 600, 18px / 24px, #363B4D.
- List: flex column, gap 12px.

**Activity item (common):** `width:380px; background:#FFFFFF; border:1px solid #CED0D4; border-radius:8px; padding:12px;` inner column `display:flex; flex-direction:column; gap:8px`:
1. Action line (flex, gap 6px, align center; item 5 uses gap 8px) — pieces below.
2. Divider: 1px `#CED0D4`, full width (356px) — `home-divider-activity.svg` or `border-top:1px solid #CED0D4`.
3. Ticket row: flex, gap 8px, height 18px, Montserrat 600, 14px / 18px, ls 0.1px:
   - Id `345234  ` (two trailing spaces, `white-space:pre`) — #007FAD
   - Title — #363B4D, `overflow:hidden; text-overflow:ellipsis; white-space:nowrap`
4. Timestamp: `9/19/24 4:35 PM by Charlie Apegian` — Montserrat 500, 12px / 14px, ls 0.4px, #8D99AE.

Text-piece styles used in action lines:
- **Bold verb** (SemiBold): Montserrat 600, 14px / 18px, ls 0, #363B4D.
- **Value** (Medium): Montserrat 500, 14px / 18px, ls 0.25px, #363B4D.
- **Italic value**: Montserrat 500 italic, 14px / 18px, ls 0.25px, #363B4D.
- **Inline avatar**: 24 × 24 circle, initials Montserrat 600, 12px, line-height normal, ls 0.1px, #FFFFFF.

**Items (verbatim):**

1. `Priority changed from` (600) · `Low` (500 italic) · `to` (500) · `High` (500 italic)
   Ticket: `345234  ` `Can’t Connect to Server`
2. `Ticket assigned to` (600) · avatar `JD` bg #8D99AE · `John Doe` (500)
   Ticket: `345234  ` `Server Downtime`
3. `Note added` (600)
   Ticket: `345234  ` `If it’s a really long title for a ticket you should` — title is `flex:1; min-width:0` and truncates with ellipsis → renders "If it’s a really long title for a ticket you…"
4. Action line wraps (`flex-wrap:wrap; gap:6px; width:100%`): `Contact` (600) · avatar `ML` bg #2B376B · `Marcus Lee of Company` (500) · avatar `ST` bg #87CFE7 · `StratusCore Technologies` (500) · `was added to ticket` (600)
   (renders on 2 lines: line 1 "Contact [ML] Marcus Lee of Company [ST]", line 2 "StratusCore Technologies was added to ticket")
   Ticket: `345234  ` `SSL Issue for StratusCore Technologies`
5. Action line gap 8px: `Incoming email from` (600, ls 0.1px) · avatar `JS` bg #8D99AE · `Joy Smith` (500)
   Ticket: `345234  ` `SSL Issue for StratusCore Technologies`

All timestamps: `9/19/24 4:35 PM by Charlie Apegian`.
Ticket ids (blue) likely link to the ticket; items appear clickable.

---

## Interactive elements (inferred)
- Settings gear button (header right).
- 4 top cards (component name "… Button Card", state "default" → clickable cards; add hover).
- To-Do: `Tickets` / `Checklist Items` checkboxes, sort button, each ticket card (hover bg #F2F3F7 as shown on row 3), ticket numbers.
- Recent Activity: each item / ticket id.

## Assets (`assets/icons/`)
| file | size | use |
|---|---|---|
| home-card-priority.svg | 40×40, white | High Priority tile |
| home-card-due-soon.svg | 40×40, white | Due Soon tile |
| home-card-closed-today.svg | 40×40, white | Closed Today tile |
| home-card-mentions.svg | 40×40, white | Mentions tile |
| home-settings.svg | 24×24, #5F6475 | header gear button |
| home-sort.svg | 24×24, #5F6475 | To-Do sort button |
| home-checkbox-checked.svg | 24×24, #007FAD | filter checkboxes |
| home-checklist.svg | 16×16, #FFA630 | checklist sub-rows |
| home-divider-todo.svg | 1220×1, #F2F3F7 | ticket card divider |
| home-divider-activity.svg | 356×1, #CED0D4 | activity divider |
| home-filter.svg / home-filter-chevron.svg | 20×20, #5F6475 | hidden dropdown variant only (not visible) |
| home-background.png | 1920×968 | flattened visible background (recommended) |
| home-bg-wave-back.svg / home-bg-wave-front.svg | 2923.94×2123.5 / 2802.91×2001.84 | background wave layers (if rebuilding) |
| home-bg-lines-a.svg / home-bg-lines-b.svg | ~665×663, 5.8 MB each | top-right hatching (if rebuilding; heavy) |
