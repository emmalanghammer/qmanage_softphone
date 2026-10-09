# Ticket Detail View — implementation spec

Source: Figma `JpJeMQQT7kuTghyeV8rbgB`, node `1890:24506` ("2.1.1 Empty State"), 1920×1870.
App header (`2104:12030`, 0–64px) is out of scope. Everything below is spec'd from `get_design_context`.

Font family everywhere: **Montserrat**. Icons live in `assets/icons/`; render every `<img>` at the stated size (SVG root width/height already match).

## Color tokens used

| Token | Hex |
|---|---|
| page background (measured from render) | `#F2F8FB` |
| background/primary, input-default | `#FFFFFF` |
| border/border | `#CED0D4` |
| text/primary | `#363B4D` |
| text/secondary, icon/secondary | `#5F6475` |
| text/accent (empty-state text) | `#8D99AE` |
| text/disabled (placeholders) | `#CED0D4` |
| text/blue, button-primary, icon/primary | `#007FAD` |
| color/purple/800 (badge, avatar) | `#2B376B` |
| button-secondary | `#F2F3F7` |
| component/attachments (dropzone) | `#F0FBFF` |
| card shadow | `drop-shadow(0 2px 3.5px rgba(0,125,171,0.10))` — i.e. `box-shadow: 0 2px 7px 0 rgba(0,125,171,0.10)` (the Activity tile literally uses this box-shadow) |

## Type styles

| Name | weight / size / line-height / letter-spacing |
|---|---|
| header/small | 500 / 24px / 26px / 0 |
| title/large (card titles) | 600 / 18px / 24px / 0 |
| body/medium | 500 / 14px / 18px / 0.25px |
| accent/medium | 400 / 14px / 18px / 0 |
| body/small (field labels) | 500 / 12px / 16px / 0.4px |
| body/special (placeholders) | 500 italic / 14px / 18px / 0.25px |
| title/small (time values) | 600 / 14px / 18px / 0.1px |

## Page layout (below app header)

`Content` frame (y=64, 1920×1806), bg `#F2F8FB`:
1. **Title bar** (`2901:21292`) — full width, 102px tall, at y=0 of Content.
2. 16px gap.
3. **Main Body** (`1890:24562`) — y=118, 1920 wide, row: `padding: 0 16px 16px`, `gap: 16px`, `align-items: flex-start`.
   - **Left Side** (`1890:24563`): 1240 wide (x=16), flex column, `gap: 16px`. → make this `flex: 1 1 0; min-width: 0`.
   - **Right Side** (`1890:24605`): 632 wide (x=1272), flex column, `gap: 16px`. → make this `flex: 0 0 632px` (fixed).
   - Narrower screens: left flexes, right stays 632. Below ~1100px viewport, stacking (right column under left, full width) is the sensible fallback; Figma has no breakpoint for it.
   - Note: the Description card is 1238 wide while the Activity tile is 1240 (2px Figma slop) — use `width: 100%` for both.

---

## 1. Title bar (`2901:21292`)

Box: bg `#FFFFFF`, `border-bottom: 1px solid #CED0D4`, shadow `0 2px 7px rgba(0,125,171,0.10)`, `padding: 16px`, flex column, `gap: 8px`, height 102 (16 + 26 + 8 + 36 + 16).

### Row 1 — "Ticket number and name" (flex row, `gap: 32px`, align center; Figma width fixed 1329 — use auto)
- Text group: flex row, `gap: 8px`, header/small (500/24px/26px), color `#363B4D`, nowrap:
  - `#1`
  - `First Ticket`
- Edit pencil: `td-edit-pencil.svg`, 24×24, fill `#007FAD`. Interactive (rename).

### Row 2 — "Info" (flex row, `justify-content: space-between`, align center, width 100%)

**Left group** "Main details": flex row, `gap: 32px`, align center.

1. **Limited Access badge** — bg `#2B376B`, `border-radius: 4px`, `padding: 4px 8px`, flex align center, overflow hidden. Height = 4+18+4 = 26 (icon 20).
   - Icon `td-warning.svg` 20×20, fill white.
   - Label container `padding: 0 8px`; text `Limited Access` body/medium (500/14/18/0.25px) color `#FFFFFF`.
   - Looks like a button (component named "Button"); treat as non-interactive badge or tooltip trigger.
2. **Created link** — `Created at 4/04/24 10:00 AM`, 400 / 14px / line-height normal (~17px) / 0, color `#007FAD`, `text-decoration: underline`. Interactive link.
3. **Assigned** — flex row, `gap: 8px`, align center.
   - Label `Assigned to`: accent/medium (400/14/18/0), `#5F6475`.
   - Selector: bg `#FFFFFF`, `border: 1px solid #CED0D4`, `border-radius: 4px`, **height 28px, width 194px**, `padding: 0 8px`, flex `justify-content: space-between`, align center.
     - Name group: flex, `gap: 8px`:
       - Avatar circle 20×20, bg `#2B376B`, `border-radius: 100px`, centered text `CA` — 600 / 8px / normal / 0.1px, white.
       - `Charlie Apegian` body/medium, `#363B4D`.
     - Caret `td-caret-down.svg` 24×24 (fill `#363B4D`).
   - Interactive (dropdown).
4. **Status** — flex row, `gap: 8px`, align center.
   - Label `Status`: accent/medium, `#5F6475`.
   - Selector: bg `#FFFFFF`, `border: 1px solid #CED0D4`, `border-radius: 4px`, `padding: 2px 4px 2px 8px`, `gap: 8px`, `max-width: 204px`, align center. Height = 2+24+2+2(border) = 30 (caret drives height).
     - Value chip: `padding: 2px 8px`, `border-radius: 4px` (no fill); text `None` body/medium `#363B4D`.
     - Caret `td-caret-down.svg` 24×24.
   - Interactive (dropdown).

**Right group** "Buttons": flex row, `gap: 16px`, align center.

1. **Closed** checkbox button — bg `#F2F3F7`, `border-radius: 4px`, **height 36px**, `padding: 0 8px`, no border.
   - Icon `td-checkbox-unchecked.svg` 20×20 (outline fill `#94CC86` green).
   - Label container `padding: 0 8px`; `Closed` body/medium `#5F6475`.
   - Interactive (toggle).
2–5. **Icon buttons** — each 36×36, bg `#F2F3F7`, `border-radius: 4px`, `padding: 0 4px`, centered 24×24 icon (fill `#5F6475`):
   - `td-connect-off.svg` (remote-connection off)
   - `td-group.svg` (people/watchers)
   - `td-visibility.svg` (eye / visibility)
   - `td-history.svg` (history)
6. **Actions** primary dropdown button — bg `#007FAD`, `border: 1px solid #007FAD`, `border-radius: 4px`, **height 36px**, `padding: 8px`.
   - Label container `padding: 0 8px`; `Actions` body/medium, `#FFFFFF`.
   - Trailing icon `td-caret-down-white.svg` 20×20 (fill white).
   - Interactive (menu).

---

## 2. Left column

### 2a. Description card (`1903:30566`)
Box: bg `#FFFFFF`, `border: 1px solid #CED0D4`, `border-radius: 8px`, shadow (card shadow), `padding: 16px`, flex column, `gap: 16px`. Height 126 with 3 lines of text.

- **Title row**: flex, `justify-content: space-between`, align center, width 100%.
  - Left: flex, `gap: 8px`, align center:
    - `td-description.svg` 24×24 (fill `#CED0D4`)
    - `Description` title/large (600/18/24), `#363B4D`
    - `td-edit-pencil.svg` 24×24 (`#007FAD`) — interactive (edit)
  - Right: "Create Checklist" link-button: flex, `gap: 8px`, height 24, align center:
    - `td-section-plus.svg` 24×24 (`#007FAD` add_box — same graphic as the card "+" icons)
    - `Create Checklist` body/medium (500/14/18/0.25px), `#007FAD`. Interactive.
- **Body text** (width 100%, wraps, `overflow: hidden; text-overflow: ellipsis`): 500 / 14px / 18px / 0.25px, `#5F6475`:
  > The issue reported involves a malfunction in the system's notification feature. Users are experiencing delays in receiving alerts, which affects their workflow. This problem may require a thorough investigation to identify the root cause. Please ensure to check the server logs and user settings for any discrepancies. The expected resolution time is within 48 hours, pending further analysis.

### 2b. Activity tile (`1951:43648`)
Box: bg `#FFFFFF`, `border: 1px solid #CED0D4`, `border-radius: 8px`, `box-shadow: 0 2px 7px 0 rgba(0,125,171,0.10)`, `padding: 16px`, flex column, `gap: 16px`, **height 601px**, overflow hidden, width 100%.

- **Header** (height 24, flex space-between, align center — the 36px button overflows the 24px row vertically, centered):
  - Left: flex `gap: 8px`: `td-activity.svg` 24×24 (`#CED0D4`) + `Activity` title/large `#363B4D`.
  - Right: flex `gap: 16px`, align center:
    - **Add Note** button: bg `#007FAD`, `border-radius: 4px`, height 36, `padding: 8px`, no border. Leading icon `td-add-white.svg` 20×20 (white) + label container `padding: 0 8px` with `Add Note` body/medium `#FFFFFF`. Interactive.
    - `td-open-in-full.svg` 24×24 (`#5F6475`) — interactive (expand).
- **Filters row** (flex, space-between, align center):
  - Input field: width 226px (`min-width: 200px`), flex column, `gap: 4px`:
    - Label `Find`: body/small (500/12/16/0.4px), `#5F6475`.
    - Input: bg `#FFFFFF`, `border: 1px solid #CED0D4`, `border-radius: 4px`, **height 36**, `padding: 8px`, `gap: 8px`, align center.
      - Placeholder `Search Activity`: body/special — 500 italic / 14px / 18px / 0.25px, color `#CED0D4`, ellipsis.
      - Trailing `td-search.svg` 20×20 (`#5F6475`).
  - Right: flex `gap: 8px`: `td-arrow-downward.svg` 24×24 (sort) + `td-filter.svg` 24×24 (filter), both `#5F6475`. Interactive. They sit vertically centered against the 56px field (so they appear ~10px below the label line).
- **Empty state** (`flex: 1`, column, centered both axes, `padding: 64px 0`, `gap: 16px`):
  - `No activity yet. Add a note to get started.` 500/14/18/0.25px, `#8D99AE`, nowrap.

---

## 3. Right column (fixed 632px)

### 3a. Jump to bar (`1893:26015`)
Box: bg `#FFFFFF`, `border: 1px solid #CED0D4`, `border-radius: 8px`, card shadow, `padding: 8px 16px`, flex space-between, align center. Height 48 (8+32+8).

- Left: flex `gap: 16px`, align center:
  - `Jump to` accent/medium (400/14/18/0), `#5F6475`.
  - Icon row: flex `gap: 8px`; 8 hit targets each **32×32** (flex centered) holding a 24×24 icon (all fill `#5F6475`), all interactive (scroll to section):
    1. `td-jump-contacts.svg` → Contacts
    2. `td-jump-ticket-details.svg` → Ticket Details
    3. `td-jump-custom-fields.svg` → Custom Fields
    4. `td-jump-attachments.svg` → Attachments
    5. `td-jump-links.svg` → Links
    6. `td-jump-time.svg` → Time Spent
    7. `td-jump-agreements.svg` → Service Agreements
    8. `td-jump-jira.svg` → Jira Issues
- Right: flex `gap: 8px`, align center:
  - Vertical divider: 1px `#CED0D4`, stretches full row height (32px). (Figma exports it as `td-jump-divider.svg` 24×1 rotated 90° — easier as `width:1px; align-self:stretch; background:#CED0D4`.)
  - Gear: **reuse existing `home-settings.svg`** (byte-identical to this icon) 24×24 `#5F6475`. Interactive.

### 3b. Section card — shared shell
Every card: bg `#FFFFFF`, `border: 1px solid #CED0D4`, `border-radius: 8px`, card shadow, `padding: 16px`, flex column, `gap: 16px`, width 100%.

Header: flex, space-between, align center, height 24.
- Title group: flex `gap: 8px`: card icon 24×24 (fill `#CED0D4`, grey) + title, title/large (600/18/24/0), `#363B4D`.
- Actions: flex `gap: 8px`, align center: optional `td-section-plus.svg` 24×24 (`#007FAD`, interactive "add") then `td-chevron-down.svg` 24×24 (`#5F6475`, interactive collapse toggle).

Empty-state text style (all cards): 500 / 14px / 18px / 0.25px, `#8D99AE`, nowrap, centered.

| # | Node | Title | Card icon | + icon | Extra header | Body | Card height |
|---|---|---|---|---|---|---|---|
| 1 | 1920:29232 | `Contacts` | `td-contacts.svg` | yes | — | height 146, `padding: 64px 0`, centered: `Add a contact to get started.` | 218 |
| 2 | 1930:32959 | `Ticket Details` | `td-ticket-details.svg` | no | — | form (below) | 376 |
| 3 | 2350:13811 | `Custom Fields` | `td-custom-fields.svg` | no | `View All` link (body/medium, `#007FAD`, in 24px-high flex; interactive) before chevron | outer `padding: 16px 0`, inner box height 50 `padding: 16px 0` centered: `Open custom fields and fill out any you want to display here.` | 154 |
| 4 | 2350:13829 | `Attachments` | `td-attachments.svg` | yes | — | dropzone (below) | 218 |
| 5 | 2350:13853 | `Links` | `td-links.svg` | yes | — | card fixed height 154; body `flex:1`, `padding: 16px 0`, centered: `Add a link to get started.` | 154 |
| 6 | 2350:13870 | `Time Spent` | `td-time-spent.svg` | no | — | 3-cell box (below) | 132 |
| 7 | 2350:13950 | `Service Agreements` | `td-service-agreements.svg` | yes | — | `padding: 16px 0`, centered: `Add a service agreement to get started.` | 122 |
| 8 | 2350:13975 | `Jira Issues` | `td-jira.svg` | yes | — | `padding: 16px 32px`, `gap: 8px`, centered: `Add a Jira issue to get started.` | 122 |

### 3c. Ticket Details form
Body: flex column, `gap: 8px` between rows. Rows: flex, `gap: 16px`, each field `flex: 1 1 0; min-width: 200px` (→ 293px each in a 602px body).

Field (Input Field): flex column, `gap: 4px`, total height 56 (16 label + 4 + 36).
- Label: body/small (500 / 12px / 16px / 0.4px), `#5F6475`.
- Control: bg `#FFFFFF`, `border: 1px solid #CED0D4`, `border-radius: 4px`, **height 36**, `padding: 8px`, `gap: 8px`, align center; value area `flex:1`, 18px tall; trailing icon 20×20.

| Row | Field label | Placeholder | Trailing icon | Notes |
|---|---|---|---|---|
| 1 | `Priority` | (empty) | `td-field-caret.svg` 20×20 `#5F6475` | select |
| 1 | `Due Date` | `mm/dd/yy` (500 italic/14/18/0.25px, `#CED0D4`) | `td-calendar.svg` 20×20 `#5F6475` | date |
| 2 | `Product` | — | `td-field-caret.svg` | select |
| 2 | `Category` | — | `td-field-caret.svg` | select |
| 3 | `Project` | — | `td-field-caret.svg` | label row is `justify-content: space-between` with `td-link.svg` **16×16** (`#5F6475`) at right end — interactive |
| 3 | `Responsible` | — | `td-field-caret.svg` | select |
| 4 | `Ticket Tags` | — | none | full width (602) text/tag input |
| 5 | `Support Queue` | — | `td-field-caret.svg` | width 290.67 (≈ one-third of 602 — note: not the same 293 as the 2-col fields; use `width: calc((100% - 16px)/2)` if you want it aligned with column 1, Figma value is 290.67) |

All controls are interactive.

### 3d. Attachments dropzone
Box: bg `#F0FBFF`, `border: 1px dashed #CED0D4`, `border-radius: 8px`, **height 146**, `padding: 16px`, flex column, centered both axes, `gap: 8px`.
- `td-upload.svg` 32×32 (cloud upload, `#007FAD`).
- Line: flex, `gap: 4px`, centered:
  - `Choose a file` body/medium `#007FAD` (link, 24px-high hit box) — interactive (opens file picker)
  - `or drag and drop anywhere` body/medium `#5F6475`.

### 3e. Time Spent box
Body: flex row, padding 0. Inner box: `border: 1px solid #CED0D4`, `border-radius: 8px`, `padding: 8px 0`, flex row, `justify-content: space-between`, width 100%. Box height = 8 + 18 + 8 + 18 + 8 + 2 = 62.
- 3 cells, each `flex: 1 1 0`, flex column, `gap: 8px`, centered, `padding: 0 16px`, color `#5F6475`, line-height 18, size 14:
  - value `0h 0m` — 600 / 14 / 18 / 0.1px
  - caption — 500 / 14 / 18 / 0.25px: `Billable Hours`, `Non-Billable Hours`, `Total`
- Between cells: vertical 1px `#CED0D4` divider, `align-self: stretch` (full 44px inner height). Figma asset `td-time-divider.svg` (44×1, rotated) — prefer a CSS border.

---

## Asset inventory (`assets/icons/`)

| File | Size (root) | Fill | Used at |
|---|---|---|---|
| td-edit-pencil.svg | 24×24 | #007FAD | title pencil, Description pencil |
| td-warning.svg | 20×20 | white | Limited Access badge |
| td-caret-down.svg | 24×24 | #363B4D | Assigned/Status selectors |
| td-checkbox-unchecked.svg | 20×20 | #94CC86 | Closed button |
| td-connect-off.svg | 24×24 | #5F6475 | header icon btn 1 |
| td-group.svg | 24×24 | #5F6475 | header icon btn 2 |
| td-visibility.svg | 24×24 | #5F6475 | header icon btn 3 |
| td-history.svg | 24×24 | #5F6475 | header icon btn 4 |
| td-caret-down-white.svg | 20×20 | white | Actions button |
| td-description.svg | 24×24 | #CED0D4 | Description card icon |
| td-section-plus.svg | 24×24 | #007FAD | Create Checklist + every card "+" |
| td-activity.svg | 24×24 | #CED0D4 | Activity card icon |
| td-add-white.svg | 20×20 | white | Add Note |
| td-open-in-full.svg | 24×24 | #5F6475 | Activity expand |
| td-search.svg | 20×20 | #5F6475 | Search Activity |
| td-arrow-downward.svg | 24×24 | #5F6475 | sort |
| td-filter.svg | 24×24 | #5F6475 | filter |
| td-jump-*.svg (8) | 24×24 | #5F6475 | Jump to icons |
| td-jump-divider.svg | 24×1 stroke | #CED0D4 | (optional; use CSS) |
| home-settings.svg (existing) | 24×24 | #5F6475 | Jump-to gear |
| td-contacts / td-ticket-details / td-custom-fields / td-attachments / td-links / td-time-spent / td-service-agreements / td-jira .svg | 24×24 | #CED0D4 | card header icons (same shapes as jump icons, grey) |
| td-chevron-down.svg | 24×24 | #5F6475 | card collapse |
| td-field-caret.svg | 20×20 | #5F6475 | form select carets |
| td-calendar.svg | 20×20 | #5F6475 | Due Date |
| td-link.svg | 16×16 | #5F6475 | Project label link |
| td-upload.svg | 32×32 | #007FAD | Attachments dropzone |
| td-time-divider.svg | 44×1 stroke | #CED0D4 | (optional; use CSS) |
