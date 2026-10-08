# Group E — Conference screens (Figma 6iYNH8CMLcJZCto956H6ZC)

Screens: `2283:18924` Add someone, `2283:19111` Adding - ringing, `2283:19201` Conference call, `2283:19286` People on the call.

Font: Montserrat everywhere. Icons in `assets/icons/`. All SVGs have root width/height attrs; render each `<img>` in a box exactly that size (given below).

## Shared / deviations from known shell

- Panel is 400×600, bg `#363B4D`, radius 8, shadow as known. Root is `display:flex; flex-direction:column; justify-content:space-between; overflow:hidden`.
- **No bottom nav on any of the 4 screens.**
- Header (400×48 incl. 1px bottom border) is as known. Assets: drag `e-drag-indicator.svg` (24×24, fill #CED0D4), `e-minimize.svg`, `e-open-in-new.svg`, `e-close.svg` (20×20, fill #CED0D4). Left group gap 8.
- **Deviation: main content padding.** "Add someone" uses padding **16** (not 20). The other three use 20. Main content in Ringing/Conference/People is a fixed box 400×552.

### Header timer chip ("Lozenge") — screens Ringing, Conference, People (NOT on Add someone)
- Placed as FIRST child of header right-side group (before minimize), right group has no gap (chip abuts the 40px minimize button).
- Box: height 24, padding 4px 8px, gap 8, radius 200 (pill), bg `#CED0D4`, display flex, align center.
- Text: Montserrat Medium 500, 14px / 18px, letter-spacing 0.25px, color `#363B4D`.
- Values: Ringing `01:45`; Conference `00:20`; People `01:32`.

### Header titles
- Add someone: `Add to call`
- Ringing: `On a call`
- Conference: `Conference call (3)`
- People: `Conference call (3)`

### Common text styles
| name | weight | size/line-height | letter-spacing |
|---|---|---|---|
| title/xs | 600 | 12/16 | 0.1px |
| title/small | 600 | 14/18 | 0.1px |
| title/medium | 600 | 16/20 | 0.15px |
| body/medium/regular | 500 | 14/18 | 0.25px |
| body/medium/accent | 400 | 14/18 | 0.25px |
| body/medium/semibold | 600 | 14/18 | 0 |
| body/large/regular | 500 | 16/20 | 0.5px |
| body/small/regular | 500 | 12/14 | 0.4px |
| body/small/accent | 400 | 12/14 | 0 |

### Common buttons
- **Secondary button** (Cancel / Remove / Leave Call / Add Someone): height 36, padding 0 8px, radius 4, bg `#F2F3F7`, overflow hidden, display flex, align center (justify center when full width). Inner container: padding 0 8px, flex center. Text body/medium/regular (500 14/18 ls 0.25) color `#5F6475`. Inline buttons (Cancel/Remove) hug content → width = 8+8+text+8+8.
- **Danger button** (End / End Call for Everyone): height 36, padding 8px 8px, radius 4, bg `#ED4B52`, flex center; inner container padding 0 8px; text 500 14/18 ls 0.25 color `#FFFFFF`.
- **Link button** ("Back to call", "3 people"): height 24, display flex, gap 8, align center, no bg/padding. Text 500 14/18 ls 0.25 color `#87CFE7`.

### Avatars (circle, radius 100, overflow hidden, flex center, text white, Montserrat 600, centered)
| size | font | ls | used in |
|---|---|---|---|
| 24×24 | 600 12px / line-height normal | 0.1 | Add-someone user rows |
| 32×32 | 600 14/18 | 0.1 | Banner, On-this-call rows, People rows |
| 48×48 | 600 16/20 | 0.15 | Conference avatar stack |
Colors: pink `#B23C69`, grey `#8D99AE`, blue `#007FAD`.

### Call controls grid (Ringing + Conference — identical)
- Container "Actions": width 174, `display:flex; flex-wrap:wrap; justify-content:center; align-items:flex-start; align-content:flex-start; row-gap:29px; column-gap:27px`. Results in row 1 = Mute, Hold, Keypad; row 2 = Add, Transfer (centered).
- Each item: width 40, flex column, align center, gap 4.
  - Circle: padding 8, radius 200, bg `#5F6475` → 36×36, holds a 20×20 icon.
  - Label: Montserrat Regular 400, 12/14, ls 0, color `#8D99AE`, text-align center (labels may overflow 40px — "Keypad"/"Transfer" are nowrap and overflow centered).
- Icons (20×20, white glyph):
  | label | Conference asset | Ringing asset (identical artwork, different mask id) |
  |---|---|---|
  | Mute | `e-mic-off.svg` | `e-ringing-mic-off.svg` |
  | Hold | `e-pause.svg` | `e-ringing-pause.svg` |
  | Keypad | `e-dialpad.svg` | `e-ringing-dialpad.svg` |
  | Add | `e-person-add.svg` | `e-ringing-person-add.svg` |
  | Transfer | `e-transfer.svg` | `e-ringing-transfer.svg` |
- **Disabled/dimmed state: NOT present in Figma.** In "Adding - ringing" the controls are exactly the same as the default (bg #5F6475, white icons, #8D99AE labels, no opacity). If a dimmed state is desired, it is not specified by the design. (Either variant file can be used interchangeably as `<img>`; separate files only avoid mask-id collisions if inlined.)

---

## Screen 1 — Add someone (2283:18924)

Bottom nav: **no**.

```
root column 400×600, justify space-between
├─ header (title "Add to call", no timer chip)
├─ Call Info banner
└─ main content (flex:1, column, padding 16, gap 20, align center, justify center, overflow hidden)
   └─ Card content (flex:1, column, gap 16, align start, width 100%, bottom radii 8)
      ├─ Card header (row, align center, width 100%) → "Back to call" link
      └─ column, gap 16, width 100%
         ├─ segmented tabs
         ├─ search bar
         └─ user list (column, gap 12, width 100%)
```

### Green call banner ("Call Info")
- Full width (400), padding 8px 16px, bg `rgba(148,204,134,0.2)`, border-bottom 1px `rgba(255,255,255,0.1)`, display flex, justify space-between, align center, overflow hidden. Rendered height 49 (32 avatar + 16 padding + 1 border).
- Left group: flex row, gap 20, align center:
  1. Phone icon `e-banner-phone-green.svg` 20×20 (fill #94CC86; phone-in-talk glyph).
  2. Vertical divider: 1px wide × 23px tall line, color `#CED0D4`. Asset `e-banner-divider-vertical.svg` is 23×1 horizontal, rotated 90° (wrapper w 0 / h 23, inner rotate(90deg)). Simpler equivalent: `<div style="width:1px;height:23px;background:#CED0D4">` (or use the asset rotated).
  3. Contact: row gap 8 align center:
     - Avatar 32×32 bg `#007FAD`, text `CA` (600 14/18 ls 0.1 white).
     - Name `Charlie Apegian` — 600 16/20 ls 0.15, white.
- Right group: row gap 8, align center:
  - `00:02` — Montserrat Regular 400, 14/18, ls 0.25, white.
  - `e-chevron-right-white.svg` 20×20 (white).

### "Back to call" link
- Row gap 8, height 24: `e-chevron-left-blue.svg` 20×20 (fill #87CFE7), then text `Back to call` 500 14/18 ls 0.25 `#87CFE7`.

### Segmented control (3-way)
- Container: width 100% (368), bg `#5F6475`, padding 2, radius 4, display flex, align center. No gap.
- 3 segments each `flex:1 0 0`, padding 8, radius 4, flex center. Segment height = 18+16 = 34; container 38.
- Text: Montserrat SemiBold 600, 14/18, ls 0, centered.
  - `Users` — selected: bg `#F4F6FB`, text `#363B4D`.
  - `Queues` — unselected: no bg, text `#FFFFFF`.
  - `Number` — unselected: no bg, text `#FFFFFF`.

### Search input
- Wrapper column, width 100%. Inner: height 40, border 1px solid `#5F6475`, radius 8, padding 8px 12px, gap 8, flex row align center, overflow hidden. No fill (transparent).
- Placeholder `Search users`: Montserrat Medium 500, 16/20, ls 0.5, color `#8D99AE`; label wrapper `flex:1`.
- Trailing icon `e-search.svg` 24×24 (white), on the RIGHT.

### User rows ("Recent Calls List": column gap 12, width 100%)
Each row followed by a full-width 1px divider (`e-row-divider.svg`, 368×1, stroke #5F6475 — or `border-top:1px solid #5F6475`, height 0 element). Divider also after the last row. Gap 12 between row and divider.

Row: flex, justify space-between, align center, width 100%. Height 36 (button).
- Left side: row gap 4, align center.
  - Avatar 24×24, bg `#B23C69` (all rows), initials 600 12px line-height normal ls 0.1 white.
  - Text column, gap 4, justify center:
    - Line 1 ("Contact info"): row gap 8, align center, nowrap:
      - Name: 600 12/16 ls 0.1 white.
      - Title: 500 12/14 ls 0.4 color `#CED0D4`.
    - Line 2: row gap 12, align center:
      - `Ext. NNN`: 500 12/14 ls 0.4 `#8D99AE`.
      - Status: row gap 4 align center: dot 8×8 + text 500 12/14 ls 0.4 `#8D99AE`.
- Right: button 36×36, padding 0 4px, radius 4, flex center, no bg; icon `e-phone-green.svg` 24×24 (fill #94CC86).

Row data (verbatim):
| initials | name | title | ext | dot asset | status |
|---|---|---|---|---|---|
| CA | Charlie Stile | Product Support Specialist I | Ext. 204 | `e-dot-available.svg` (#94CC86) | Available |
| EF | Eleanor Foster | Product Support Specialist II | Ext. 201 | `e-dot-available.svg` | Available |
| JS | Joe Smith | Product Support Specialist I | Ext. 207 | `e-dot-red.svg` (#ED4B52) | On a call |
| PR | Pam Reynolds | Product Support Manager | Ext. 210 | `e-dot-away.svg` (#FFA630) | Away |
| ML | Marcus Lee | Product Support Team Lead | Ext. 212 | `e-dot-red.svg` (#ED4B52) | Offline |

(Note: Offline uses the same red dot as "On a call" in this design.)

---

## Screen 2 — Adding - ringing (2283:19111)

Bottom nav: **no**. Header title `On a call`, timer chip `01:45`.

```
main content: 400×552, column, padding 20, gap 20, align center, justify center
├─ call users list (flex:1, column, gap 20, align center, width 100%)
│  ├─ "Avatar and Name" section (column, gap 8, align start, width 100%)
│  │  ├─ label "On this call"
│  │  ├─ row 1 (on hold)
│  │  ├─ divider
│  │  ├─ row 2 (ringing + Cancel)
│  │  └─ divider
│  └─ Actions grid (see shared)
└─ End button (width 336, NOT 100%)
```

### "On this call" section
- Label `On this call`: Montserrat Regular 400, 12/14, ls 0, white `#FFFFFF`.
- Dividers: `e-ringing-divider.svg` 360×1 stroke `#5F6475` (equiv. 1px line `#5F6475`, full width).
- Row: flex row, gap 8, align center, padding 4, width 100%.
  - Left side: `flex:1`, row gap 4, align center:
    - Avatar 32×32 (600 14/18 ls 0.1 white).
    - Text column gap 4, justify center:
      - Name: 600 14/18 ls 0.1 white.
      - Sub-line: row gap 8, align start; text 500 12/14 ls 0.4 `#8D99AE`.
  - Optional right button (secondary, 36 tall).

Rows:
1. Avatar bg `#B23C69` `CA`; name `Charlie Apegian`; sub-line `On hold` + `01:12` (two spans, gap 8). No button. Row height 40.
2. Avatar bg `#8D99AE` `EF`; name `Eleanor Foster`; sub-line `Ringing...`. Right: secondary button `Cancel` (bg #F2F3F7, text #5F6475 500 14/18 ls 0.25, h 36, padding 0 8 + inner 0 8, radius 4). Row height 44.

### Controls: default (identical to Conference; no dimming — see shared section). Uses `e-ringing-*.svg` assets.

### End button
- Danger button, **width 336** (centered by parent align center), height 36, text `End`.

---

## Screen 3 — Conference call (2283:19201)

Bottom nav: **no**. Header title `Conference call (3)`, timer chip `00:20`.

```
main content: 400×552, column, padding 20, gap 20, align center, justify center
├─ call users list (flex:1, column, gap 20, align center, width 100%)
│  ├─ contacts block (column, gap 8, align center, justify center)
│  │  ├─ avatar stack
│  │  ├─ names
│  │  └─ "3 people >" link
│  └─ Actions grid
├─ End Call for Everyone (danger, width 100%)
└─ Leave Call (secondary, width 100%)
```

### Overlapping avatar stack
- Row, align center. Three 48×48 avatars, first two have `margin-right:-8px` (8px overlap; later avatar paints on top of earlier). Total width 128. No border/ring.
  1. bg `#B23C69`, `CA`
  2. bg `#8D99AE`, `EF`
  3. bg `#007FAD`, `EL`
- Initials 600 16/20 ls 0.15 white.

### Names line
- `Charlie, Eleanor, & you` — 600 16/20 ls 0.15 white.

### "3 people >" link
- Link button height 24, gap 8: text `3 people` (500 14/18 ls 0.25 `#87CFE7`) then trailing `e-chevron-right-blue.svg` 20×20 (fill #87CFE7).

### Controls: default state, assets `e-mic-off.svg`, `e-pause.svg`, `e-dialpad.svg`, `e-person-add.svg`, `e-transfer.svg`.

### Bottom buttons (stacked with main-content gap 20 between them)
- `End Call for Everyone`: danger, width 100% (360), h 36.
- `Leave Call`: secondary (bg #F2F3F7, text #5F6475), width 100%, h 36, justify center.

---

## Screen 4 — People on the call (2283:19286)

Bottom nav: **no**. Header title `Conference call (3)`, timer chip `01:32`.

```
main content: 400×552, column, padding 20, gap 20, align center (justify start)
├─ Card header (row, width 100%) → "Back to call" link (e-chevron-left-blue.svg 20×20 + text)
├─ call users list (column, gap 20, align center, width 360, height 404 fixed)
│  ├─ Contacts section (column gap 8, width 100%)
│  │  ├─ label "Contacts (1)"
│  │  └─ row: Charlie Apegian + Remove
│  ├─ divider (360×1 #5F6475)
│  └─ Users section (column gap 8, width 100%)
│     ├─ label "Users (2)"  (wrapped in column gap 12 — single child, no effect)
│     ├─ row: Eleanor Foster + Remove
│     ├─ divider
│     ├─ row: Emma Langhammer (you), no button
│     └─ divider
└─ Add Someone button (secondary, width 100%)  — sits at bottom because list height is fixed 404
```
(Add Someone top = 20 + 24 + 20 + 404 + 20 = 488 within main; bottom edge 524 → 28 px below to 552. Screenshot confirms button bottom ≈ 20px above panel bottom area.)

### Section labels
- `Contacts (1)`, `Users (2)`: Montserrat Regular 400, 12/14, ls 0, white.

### Rows
Same text styles as Ringing rows (avatar 32, name 600 14/18 ls 0.1 white, sub-line 500 12/14 ls 0.4 `#8D99AE` two spans gap 8).
- **Contacts row** ("recent call"): flex row gap 8, align center, **padding 4**, width 100%; left side flex:1 row gap 4 (no padding).
  - Avatar `#B23C69` `CA`; `Charlie Apegian`; `Connected` `01:32`; right: secondary `Remove`.
- **Users rows**: outer row flex gap 8 align center, **no padding**; left side flex:1, row gap 4, **padding 8**, radius 4 (no fill). So avatars in Users section are inset 8px vs 4px in Contacts (visible in screenshot).
  - Avatar `#8D99AE` `EF`; `Eleanor Foster`; `Connected` `00:20`; right: secondary `Remove`.
  - Self row (no outer wrapper; the "left side" box itself, width 100%, padding 8, gap 4, radius 4): Avatar `#8D99AE` `EF` (sic — Figma shows EF, not EL); `Emma Langhammer (you)`; `Connected` `01:32`; no button.
- Dividers: `e-people-divider.svg` 360×1 stroke `#5F6475` (between Contacts and Users sections, after Eleanor row, after self row). No divider between Contacts label/row.

### Remove button
- Secondary: h 36, bg `#F2F3F7`, radius 4, padding 0 8 + inner 0 8, text `Remove` 500 14/18 ls 0.25 `#5F6475`.

### Add Someone button
- Secondary, width 100% (360), h 36, justify center, text `Add Someone`.

---

## Asset index (`/Users/emmalanghammer/qmanage_softphone/assets/icons/`)
| file | root w×h | color | usage |
|---|---|---|---|
| e-drag-indicator.svg | 24×24 | #CED0D4 | header left (all screens) |
| e-minimize.svg | 20×20 | #CED0D4 | header |
| e-open-in-new.svg | 20×20 | #CED0D4 | header |
| e-close.svg | 20×20 | #CED0D4 | header |
| e-banner-phone-green.svg | 20×20 | #94CC86 | Add someone banner phone icon |
| e-banner-divider-vertical.svg | 23×1 | stroke #CED0D4 | banner divider (rotate 90°) |
| e-chevron-right-white.svg | 20×20 | white | banner right chevron |
| e-chevron-left-blue.svg | 20×20 | #87CFE7 | "Back to call" (Add someone, People) |
| e-chevron-right-blue.svg | 20×20 | #87CFE7 | "3 people" link |
| e-search.svg | 24×24 | white | search input trailing |
| e-phone-green.svg | 24×24 | #94CC86 | user-row call button |
| e-dot-available.svg | 8×8 | #94CC86 | Available |
| e-dot-red.svg | 8×8 | #ED4B52 | On a call / Offline |
| e-dot-away.svg | 8×8 | #FFA630 | Away |
| e-row-divider.svg | 368×1 | stroke #5F6475 | Add someone list dividers |
| e-ringing-divider.svg | 360×1 | stroke #5F6475 | Ringing dividers |
| e-people-divider.svg | 360×1 | stroke #5F6475 | People dividers |
| e-mic-off.svg / e-ringing-mic-off.svg | 20×20 | white | Mute |
| e-pause.svg / e-ringing-pause.svg | 20×20 | white | Hold |
| e-dialpad.svg / e-ringing-dialpad.svg | 20×20 | white | Keypad |
| e-person-add.svg / e-ringing-person-add.svg | 20×20 | white | Add |
| e-transfer.svg / e-ringing-transfer.svg | 20×20 | white | Transfer |
