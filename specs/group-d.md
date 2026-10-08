# Group D — Transfer screens (Figma file 6iYNH8CMLcJZCto956H6ZC)

Screens: 2280:17661 Transfer to a user · 2280:17524 Transfer to a queue · 2280:17414 Transfer to a number · 2280:17338 Choose how to transfer · 2280:17215 Consulting · 2280:17149 Transferred

Font family everywhere: Montserrat. Weights: Regular 400, Medium 500, SemiBold 600. Format below: `weight size/line-height ls letter-spacing color`.

**No screen in this group has a bottom nav.** Panel = header (48px: 4 + 40 + 4, plus 1px bottom border) + optional call banner + main content filling the rest (flex 1).

Icons live in `/Users/emmalanghammer/qmanage_softphone/assets/icons/`. Every SVG has root width/height attributes; render each `<img>` at exactly that size (listed per file at the bottom). Don't restyle the SVGs. Their colors are baked in.

---

## 0. Shared components

### 0.1 Panel and header: matches what's ALREADY KNOWN, with these deviations
- Panel: column flex, `justify-content: space-between`, overflow hidden, 400×600.
- Header icons: `d-drag-indicator.svg` (24, #CED0D4), `d-minimize.svg` / `d-open-in-new.svg` / `d-close.svg` (20 each, all #CED0D4).
- Header titles: "Transfer call" (user / queue / number / choose screens), "Consulting" (Consulting), "Call transferred" (Transferred). SemiBold 12/16 ls 0.1 #FFFFFF.
- **Header timer chip (Consulting only).** It's the first child of the header's right-side flex, before the minimize button, with no gap between it and the 40px buttons.
  - Box: height 24, padding 4px 8px, border-radius 200, background #CED0D4. Inline flex, align-items center, gap 8.
  - Text "00:20": Medium 14/18 ls 0.25 #363B4D.

### 0.2 Green call banner ("Call Info")
Appears on: Transfer to a user, Transfer to a queue, Transfer to a number, Choose how to transfer. Not on Consulting or Transferred.

- Container:
  - width 100% (400), padding 8px 16px, row flex, justify-content space-between, align-items center.
  - background `rgba(148,204,134,0.2)` drawn over the panel's #363B4D.
  - border-bottom 1px `rgba(255,255,255,0.1)`, overflow hidden.
  - Height = 32 avatar + 16 padding + 1 border = 49.
- Left group ("Active Call Info"): row, gap 20, align center. Children in order:
  1. Phone icon: `d-banner-phone.svg`, 20×20. It's a green #94CC86 phone-in-talk glyph.
  2. Vertical divider: a 1px line 23px tall, color #CED0D4.
     - Figma draws it with `d-banner-divider.svg` (23×1, stroke #CED0D4) rotated 90°.
     - Simplest equivalent: `<div style="width:1px;height:23px;background:#CED0D4">`. If you use the SVG, wrap it in a box with width 0 and height 23 and rotate the img 90°.
  3. Contact: row, gap 8, align center.
     - Avatar: 32×32 circle (radius 100), background #007FAD, content centered. Text "CA": SemiBold 14/18 ls 0.1 #FFFFFF.
     - Name "Charlie Apegian": SemiBold 16/20 ls 0.15 #FFFFFF.
- Right group: row, gap 8, align center.
  - Text "00:02": Regular 14/18 ls 0.25 #FFFFFF.
  - `d-chevron-right.svg`, 20×20, white.

### 0.3 Main content wrapper (banner screens)
- Outer box: flex 1, column, padding 20, gap 20, align-items center, justify-content center, overflow hidden, width 100%.
- Inner "Card content": flex 1, column, align-items flex-start, width 100% (360). Gap is 16 on user / queue / number and **20** on Choose.

### 0.4 "Back to call" link (Card header)
- Wrapper: row, width 100%, align center.
- Inner button: row, gap 8, height 24, align center.
  - `d-chevron-left.svg`, 20×20, #87CFE7.
  - Text "Back to call": Medium 14/18 ls 0.25 #87CFE7.

### 0.5 Extensions/Keypad segmented control ("tabs")
- Track:
  - width 100%, padding 2, background #5F6475, border-radius 4.
  - Row, align center, no gap.
  - Height = 2 + 34 + 2 = 38.
- Each segment: flex 1 (`flex: 1 0 0`), padding 8, border-radius 4, centered. Text is SemiBold 14/18 ls 0, centered.
  - Active segment: background #F4F6FB, text #363B4D.
  - Inactive segment: transparent background, text #FFFFFF.
- Which segment is active:
  - User and Queue screens: "Extensions".
  - Number screen: "Keypad".

### 0.6 Filter row ("Filter By" or "Queues" dropdown + search button)
- Row: width 100%, gap 16, align center.
- Dropdown field:
  - flex 1 (computed width 304 = 360 − 16 − 40).
  - Box: height 36, border 1px #5F6475, border-radius **4** (not 8), padding 8. Row, gap 8, align center, overflow hidden.
  - Text area: flex 1, height 18, single line, ellipsis.
  - User screen: placeholder "Filter By", **Medium Italic** 14/18 ls 0.25 #8D99AE.
  - Queue screen: value "Queues", Medium (not italic) 14/18 ls 0.25 #FFFFFF.
  - Trailing icon: `d-filter.svg`, 24×24, white.
- Square search button:
  - Box: height 36, border 1px #5F6475, border-radius 4, padding 8. Content is `d-search.svg`, 24×24, white.
  - Rendered width = 40 (8 + 24 + 8), so it's a 40×36 box.
  - Figma's code reports `w-[248px]` on the inner state. That's a stale component width and the screenshot shows 40px, so **use width 40**.

### 0.7 "Transfer" row button (Secondary button)
It isn't outlined. It's a light filled button:
- height 36, padding 0 8, border-radius 4, background #F2F3F7, no border. Row, align center, overflow hidden.
- Inner container: padding 0 8.
- Text "Transfer": Medium 14/18 ls 0.25 #5F6475.
- Total width ≈ 91 (8 + 8 + text + 8 + 8).
- Leading and trailing icons are hidden. The component's hidden icon assets were saved as `d-add.svg` and `d-arrow-drop-down.svg` (20×20, #5F6475) but **they are not displayed**.

### 0.8 Primary and secondary full buttons
- Secondary (also used for Consult First, Cancel & Return to Caller, Done, Swap):
  - background #F2F3F7, height 36, padding 0 8, radius 4, content centered.
  - Inner container padding 0 8. Text Medium 14/18 ls 0.25 #5F6475.
- Primary (Transfer Now, Complete Transfer):
  - background #007FAD, border 1px #007FAD, height 36, padding 8 (border-box), radius 4, centered.
  - Text Medium 14/18 ls 0.25 #FFFFFF.

### 0.9 List divider
- A 1px line, width 100% (360), color #5F6475.
- Asset: `d-list-divider.svg` (360×1). Equivalent CSS: `height:1px;background:#5F6475` (Figma draws the line on the row's top edge, offset -1).
- It goes after every row, **including the last one**.

---

## 1. Transfer to a user (2280:17661)
No bottom nav. Header title "Transfer call". Banner as in §0.2.

Layout tree:
```
main content (§0.3)
└ Card content: column, gap 16, w 360
  ├ Back to call (§0.4)
  └ wrapper: column, gap 16, w 100%
    ├ tabs (§0.5), Extensions active
    ├ filter row (§0.6), "Filter By" italic placeholder
    └ "Recent Calls List": column, gap 12, w 100%
       repeat for each row: [row] then [divider §0.9]
```

### User row
- Row: width 100%, justify-content space-between, align center.
- Left side: row, gap 4, align center.
  - Avatar: 24×24 circle (radius 100), background **#B23C69**, centered. Initials: SemiBold 12 / line-height normal, ls 0.1, #FFFFFF.
  - Text column: column, gap 4, justify center, align flex-start.
    1. Name: SemiBold 12/16 ls 0.1 #FFFFFF.
    2. Title: Medium 12/14 ls 0.4 **#CED0D4**.
    3. Meta row: row, gap 12, align center.
       - Ext text: Medium 12/14 ls 0.4 #8D99AE.
       - Status group: row, gap 4, align center. An 8×8 dot icon, then the status label in Medium 12/14 ls 0.4 #8D99AE.
- Right side: "Transfer" button (§0.7).

Row data (verbatim):

| Initials | Name | Title | Ext | Status dot | Status label |
|---|---|---|---|---|---|
| CA | Charlie Stile | Product Support Specialist I | Ext. 204 | d-status-dot-green.svg (#94CC86) | Available |
| EF | Eleanor Foster | Product Support Specialist II | Ext. 201 | d-status-dot-green.svg | Available |
| JS | Joe Smith | Product Support Specialist I | Ext. 207 | d-status-dot-red.svg (#ED4B52) | On a call |
| PR | Pam Reynolds | Product Support Manager | Ext. 210 | d-status-dot-orange.svg (#FFA630) | Away |
| ML | Marcus Lee | Product Support Team Lead | Ext. 212 | d-status-dot-red.svg (#ED4B52; Figma uses the same red asset) | Offline |

- All avatars use #B23C69.
- The list overflows the 600 panel; the last row is clipped by the panel's overflow hidden. Use overflow-y auto on the list if you want it scrollable.
- Row height = 3 text lines (16 + 4 + 14 + 4 + 14) = 52, which is taller than the 36 button. Rows are 12 apart with dividers between them, so each row block is row + 12 + 1px divider + 12.

---

## 2. Transfer to a queue (2280:17524)
No bottom nav. Header "Transfer call". Banner §0.2.

Layout tree:
```
main content (§0.3)
└ Card content: column, gap 16, w 360
  ├ Back to call (§0.4)
  ├ tabs (§0.5), Extensions active (Figma shows Extensions active on this screen too)
  ├ filter row (§0.6), dropdown value "Queues" (Medium 14/18 ls .25 #FFFFFF, not italic), filter icon, search square
  └ list: column, gap 12, w 100%; [row][divider] repeated
```
Note: there is no extra wrapper here. The tabs, filter row and list are direct children of Card content at gap 16, so spacing matches the User screen.

### Queue row
- Row: width 100%, justify-content space-between, align center.
- Left side: row, gap 4, align center.
  - Icon: `d-queue.svg`, 24×24, white headset/agent glyph. No circle background.
  - Text column: column, gap 4, justify center.
    1. Queue name: SemiBold 12/16 ls 0.1 #FFFFFF.
    2. Meta row: row, gap 12, align center. Two texts, each Medium 12/14 ls 0.4 #8D99AE.
- Right side: "Transfer" button (§0.7).

Row data (verbatim):

| Name | Waiting | Agents |
|---|---|---|
| General support | 3 waiting | 4 agents available |
| Billing | 0 waiting | 2 agents available |
| Sales | 1 waiting | 1 agent available |
| Premium Escalations | 0 waiting | 0 agents available |

Row height = 36 (the button is the tallest element). There's a divider after each row, including the last.

---

## 3. Transfer to a number (2280:17414)
No bottom nav. Header "Transfer call". Banner §0.2.

Layout tree:
```
main content (§0.3)
└ Card content: column, gap 16, w 360, flex 1
  ├ Back to call (§0.4)
  ├ tabs (§0.5), Keypad active (first segment transparent/white text "Extensions"; second #F4F6FB/#363B4D "Keypad")
  └ inner "main content": flex 1, column, gap 20, align center, padding 0, w 100%
     ├ input wrapper: column, gap 16, w 100%
     │  └ Input Field: h 40, w 100%
     │     box: border 1px #5F6475, radius 8, padding 8, row gap 8 align center, flex 1 (fills 40)
     │     ├ text "(555) 444-12": Medium 14/18 ls .25 #FFFFFF, flex 1, ellipsis, line box h 18
     │     └ trailing icon d-input-close.svg 24×24 (white)
     ├ keypad wrapper: column, gap 20, align center
     │  └ grid: inline-grid, 3 cols × 4 rows (fit-content), column-gap 24, row-gap 16
     │     buttons 48×48, radius 200, bg #5F6475, padding 8, centered
     │     label SemiBold 14/18 ls 0 #FFFFFF
     │     order: 1 2 3 / 4 5 6 / 7 8 9 / * 0 #
     └ actions: row, gap 16, w 100%, justify center, align center
        ├ "Consult First": secondary (§0.8), flex 1 (172 wide)
        └ "Transfer Now": primary (§0.8), flex 1 (172 wide)
```
- Keypad deviations from the known spec: none. Buttons have no sub-letters; label only, ls 0.
- Grid size: width 3×48 + 2×24 = 192; height 4×48 + 3×16 = 240.
- The input box here uses radius 8 and height 40, unlike the filter fields' radius 4 and height 36.
- The input-close icon is white (#FFFFFF), not grey.

---

## 4. Choose how to transfer (2280:17338)
No bottom nav. Header "Transfer call". Banner §0.2.

Layout tree:
```
main content (§0.3)
└ Card content: column, **gap 20**, align flex-start, w 360, flex 1 (content sits at top)
  ├ Back to call (§0.4)
  ├ "contacts": column, gap 8, align center, justify center, w 100%
  │  ├ Avatar 48×48 circle, bg #8D99AE, centered; "EF" SemiBold 16/20 ls .15 #FFFFFF
  │  ├ name row (row gap 8): "Eleanor Foster" SemiBold 16/20 ls .15 #FFFFFF
  │  ├ meta row: row, gap 12, align center
  │  │  texts Medium 12/14 ls .4 **#FFFFFF**: "Ext. 201" · "Product Support Specialist II"
  │  └ status: row, gap 4, align center
  │     d-status-dot-green.svg 8×8 + "Available" Medium 12/14 ls .4 #FFFFFF
  └ actions: row, gap 16, w 100%, justify center
     ├ "Consult First": secondary (§0.8), flex 1
     └ "Transfer Now": primary (§0.8), flex 1
```
Everything below the actions row is empty #363B4D.

---

## 5. Consulting (2280:17215)
No bottom nav. **No green banner.**
- Header title: "Consulting".
- Header right side, in order: timer chip "00:20" (§0.1), then minimize, open-in-new, close.

Layout tree:
```
main content: w 400, h 552 (fixed; = 600 − 48 header), column, gap 20, padding 20, align center, justify center
├ "call users list": flex 1, column, gap 20, align center, w 100%
│  ├ On hold section: column, gap 8, align flex-start, w 100%
│  │  ├ label "On hold": Regular 12/14 ls 0 #FFFFFF
│  │  └ row: w 100%, padding 4, row, gap 8, align center
│  │     ├ left: flex 1, row, gap 4, align center
│  │     │  ├ Avatar 32×32 circle, bg #B23C69; "CA" SemiBold 14/18 ls .1 #FFFFFF
│  │     │  └ text col: column, gap 4
│  │     │     ├ "Charlie Apegian" SemiBold 14/18 ls .1 #FFFFFF
│  │     │     └ meta row: row, gap 8, align flex-start; Medium 12/14 ls .4 #8D99AE
│  │     │        "On hold" · "01:12"
│  │     └ "Swap" button: secondary, h 36, padding 0 8 (+ inner 0 8), radius 4, bg #F2F3F7
│  │        text Medium 14/18 ls .25 #5F6475; content width (not full width)
│  ├ Talking to section: column, gap 8, w 100%
│  │  ├ label wrapper (column gap 12): "Talking to" Regular 12/14 ls 0 #FFFFFF
│  │  └ row: w 100%, row, gap 8, align center
│  │     └ card: flex 1, bg rgba(255,255,255,0.05), radius 4, padding 8, row, gap 4, align center
│  │        ├ Avatar 32×32 circle, bg #8D99AE; "EF" SemiBold 14/18 ls .1 #FFFFFF
│  │        └ text col: column, gap 4
│  │           ├ "Eleanor Foster" SemiBold 14/18 ls .1 #FFFFFF
│  │           └ meta row: row, gap 8; Medium 12/14 ls .4 #8D99AE
│  │              "Ext. 201" · "00:20"
│  └ Actions: w 174, flex-wrap, row-gap 29, column-gap 27, align flex-start (centered by parent)
│     each control: column, gap 4, align center, w 40
│        circle: padding 8, radius 200, bg #5F6475 → 36×36, icon 20×20 centered
│        label: Regular 12/14 ls 0 #8D99AE, centered
│     1. d-mic-off.svg   label "Mute"
│     2. d-dialpad.svg   label "Keypad"
│     3. d-merge.svg     label "Merge"
└ actions (bottom): column, gap 16, w 100%, align center
   ├ "Complete Transfer": primary (§0.8), w 100%
   └ "Cancel & Return to Caller": secondary (§0.8), w 100%
```
- The circles are 36×36: 20 icon + 8 padding on each side.
- Controls row width: 3×40 + 2×27 = 174.
- The bottom button pair sits flush to the bottom padding because "call users list" is flex 1.

---

## 6. Transferred (2280:17149)
No bottom nav. **No green banner.** Header title "Call transferred", with the standard three right buttons and no chip.

Layout tree:
```
main content: flex 1, column, **gap 32**, **padding 32**, align center, w 100% (inner width 336)
├ Toast (success): w 100%, min-width 344, padding 16, radius 8, bg **#C9E5C3**, row, align center
│  text "Call transferred successfully!" Medium 14/18 ls .25 **#363B4D**
├ contact block: column, gap 16, align center
│  ├ Avatar 48×48 circle, bg #B23C69; "CA" SemiBold 16/20 ls .15 #FFFFFF
│  ├ "Charlie Apegian" SemiBold 16/20 ls .15 #FFFFFF
│  └ text col: column, gap 8, align center; Medium 14/18 ls .25 #FFFFFF, centered
│     "(555)-123-4567"
│     "Creative Solutions LLC"
├ "4m 02s": Medium 14/18 ls .25 #FFFFFF, centered
└ "Done": secondary (§0.8), w 100%
```
- The toast has no icon, border or shadow.
- Width conflict: Figma gives `min-width 344`, but the inner width is only 336 (400 − 2×32), so the toast overflows to 344. In the screenshot it's 28 → 372, i.e. it overflows 4px each side and stays centered. To match the screenshot exactly, use width 344 with `align-self: center`.

---

## 7. Asset files (all in `/Users/emmalanghammer/qmanage_softphone/assets/icons/`)

| File | Root W×H | Color | Used where (render size) |
|---|---|---|---|
| d-drag-indicator.svg | 24×24 | #CED0D4 | header left 40px button (24) |
| d-minimize.svg | 20×20 | #CED0D4 | header right (20) |
| d-open-in-new.svg | 20×20 | #CED0D4 | header right (20) |
| d-close.svg | 20×20 | #CED0D4 | header right (20) |
| d-banner-phone.svg | 20×20 | #94CC86 (masked) | green banner, leftmost (20) |
| d-banner-divider.svg | 23×1 | stroke #CED0D4 | banner vertical divider (rotate 90° → 1×23) |
| d-chevron-right.svg | 20×20 | white | banner, after timer (20) |
| d-chevron-left.svg | 20×20 | #87CFE7 | "Back to call" (20) |
| d-filter.svg | 24×24 | white | filter/queues dropdown trailing (24) |
| d-search.svg | 24×24 | white | square search button (24) |
| d-status-dot-green.svg | 8×8 | #94CC86 | Available (8) |
| d-status-dot-red.svg | 8×8 | #ED4B52 | On a call / Offline (8) |
| d-status-dot-orange.svg | 8×8 | #FFA630 | Away (8) |
| d-list-divider.svg | 360×1 | stroke #5F6475 | list dividers (360×1) |
| d-queue.svg | 24×24 | white | queue row icon (24) |
| d-input-close.svg | 24×24 | white | number input trailing clear (24) |
| d-mic-off.svg | 20×20 | white (masked) | Consulting "Mute" (20 in 36 circle) |
| d-dialpad.svg | 20×20 | white (masked) | Consulting "Keypad" (20) |
| d-merge.svg | 20×20 | white (masked) | Consulting "Merge" (20) |
| d-add.svg | 20×20 | #5F6475 | hidden leading icon of Transfer button; NOT displayed |
| d-arrow-drop-down.svg | 20×20 | #5F6475 | hidden trailing icon of Transfer button; NOT displayed |
