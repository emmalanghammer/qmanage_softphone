# Group C — Active call screens (Figma 6iYNH8CMLcJZCto956H6ZC)

Screens: 2280:15348 Active Call · 2280:15425 Muted + on hold · 2280:15502 In-call keypad · 2280:15630 Contact details in call · 2280:15767 Unknown caller in call

Icons live in `/Users/emmalanghammer/qmanage_softphone/assets/icons/` (paths below are relative to it).
All SVGs have root width/height attrs equal to the rendered size listed — render `<img>` at exactly that size.

## 0. Global notes / deviations from the known shell

- **No bottom nav on any of the 5 screens.** Panel = header (+ optional green call banner) + one `main content` box that is `flex: 1 0 0`.
- Panel: identical to known shell (400×600, #363B4D, radius 8, Dropshadow/SM, `flex-direction: column; justify-content: space-between; overflow: hidden; padding 0`).
- Header: identical to known shell (padding 4, bg #363B4D + rgba(0,0,0,.1) overlay, border-bottom 1px rgba(255,255,255,.1), width 400, `justify-content: space-between; align-items: center`). Header total height = 4+40+4 + 1 border = 49.
  - Left: `display:flex; gap 8; align-items:center` → 40×40 round button (padding 8, radius 200) containing 24×24 `c-header-drag.svg` (#CED0D4) + title text (Montserrat SemiBold 600, 12px / 16px, ls 0.1px, #FFFFFF, nowrap).
  - Title string: **"On a call"** on Active Call, Muted+hold, In-call keypad, Unknown caller. **"Phone"** on Contact details in call.
  - Right: `display:flex; align-items:center; gap 0` → [timer chip (only on some screens)] + three 40×40 round buttons (padding 8, radius 200, content centered) holding 20×20 icons: `c-header-minimize.svg`, `c-header-open-in-new.svg`, `c-header-close.svg` (all #CED0D4).
- Font family everywhere: Montserrat.

### 0.1 Header timer chip ("Lozenge")
Present on: Active Call, Muted + on hold, Unknown caller in call. **Absent** on In-call keypad and Contact details in call (those show the green call banner instead).
- Placed as the FIRST child of the header right-side group, directly before the minimize button, **no gap** (the 40px button's own 8px padding gives the visual spacing).
- Box: `display:flex; align-items:center; gap 8; height 24; padding 4px 8px; border-radius 200px; background #CED0D4`.
- Text: "02:14" — Montserrat Medium 500, 14px / 18px, ls 0.25px, color #363B4D, nowrap.
- No icon.

### 0.2 Green call banner ("Call Info") — In-call keypad & Contact details in call
Sits directly under the header, full width (400), `flex-shrink:0`.
- Box: `display:flex; align-items:center; justify-content:space-between; padding 8px 16px; background rgba(148,204,134,0.2)` (over panel #363B4D); `border-bottom: 1px solid rgba(255,255,255,0.1)`; overflow hidden. Height = 32 + 16 + 1 = 49.
- Left group "Active Call Info": `display:flex; align-items:center; gap 20`
  1. Phone icon 20×20 → `c-banner-phone.svg` (green #94CC86 phone-in-talk glyph).
  2. Vertical divider: 1px wide × 23px tall line, color #CED0D4. (Figma asset `c-banner-divider.svg` is 23×1 horizontal stroke rotated 90°; simplest equivalent: `<div style="width:1px;height:23px;background:#CED0D4">`. If using the SVG: wrapper `width:0;height:23px; display:flex; align-items:center; justify-content:center`, inner `transform:rotate(90deg)` with the 23×1 img.)
  3. Contact: `display:flex; align-items:center; gap 8`
     - Avatar 32×32 circle (radius 100), bg #007FAD, content centered: "CA" Montserrat SemiBold 600, 14px / 18px, ls 0.1px, #FFFFFF.
     - Name "Charlie Apegian": Montserrat SemiBold 600, 16px / 20px, ls 0.15px, #FFFFFF, nowrap.
- Right group: `display:flex; align-items:center; gap 8`
  - "00:02": Montserrat **Regular 400**, 14px / 18px, ls 0.25px, #FFFFFF.
  - Chevron 20×20 → `c-banner-chevron-right.svg` (white).

### 0.3 Call-control buttons (Mute / Hold / Keypad / Add / Transfer)
Container "Actions": `display:flex; flex-wrap:wrap; justify-content:center; align-items:flex-start; align-content:flex-start; width 174px; row-gap 29px; column-gap 27px`. 5 items of width 40 → row 1 = Mute, Hold, Keypad (40·3 + 27·2 = 174); row 2 = Add, Transfer centered.

Each item: `display:flex; flex-direction:column; align-items:center; gap 4; width 40`.
- Circle: `padding 8; border-radius 200; display:flex; align-items:center; justify-content:center` with a 20×20 icon → **36×36 circle**.
- Label: Montserrat Regular 400, 12px / 14px, ls 0, text-align center, nowrap (labels "Keypad", "Transfer", "Unmute", "Resume" are wider than 40 and overflow symmetrically — keep the item 40 wide and let the label overflow centered, or use `white-space:nowrap` with the column centered).

States:
| State | Circle bg | Icon | Label color | Item opacity |
|---|---|---|---|---|
| Default | #5F6475 | white glyph (files below) | #8D99AE | 1 |
| On (active, filled white) | #FFFFFF | dark glyph #5F6475 | #FFFFFF | 1 |
| Disabled | #5F6475 | white glyph | #8D99AE | **0.25 on the whole item** (circle + label) |

Icons per button:
- Mute (default): `c-mic-off.svg` (white, mic with slash); label "Mute".
- Mute ON: `c-mic-dark.svg` (#5F6475 mic, no slash); label "**Unmute**", white.
- Hold (default): `c-pause.svg` (white); label "Hold".
- Hold ON: `c-play-dark.svg` (#5F6475 play arrow); label "**Resume**", white.
- Keypad: `c-dialpad.svg` (white); label "Keypad". Disabled variant uses `c-dialpad-disabled.svg` (byte-identical glyph to c-dialpad.svg; dimming comes from opacity 0.25).
- Add: `c-person-add.svg` (white); label "Add".
- Transfer: `c-transfer.svg` (white); label "Transfer".

### 0.4 Shared contact block (call screens)
"contacts": `display:flex; flex-direction:column; align-items:center; justify-content:center; gap 8`.
- Avatar 48×48 circle (radius 100), content centered.
- Name row: `display:flex; gap 8; align-items:center` → name text Montserrat SemiBold 600, 16px / 20px, ls 0.15px, #FFFFFF.
- Sub-text column: `display:flex; flex-direction:column; align-items:center; gap 8` → Montserrat Medium 500, 14px / 18px, ls 0.25px, #FFFFFF, centered.

### 0.5 End button
`width:100%; height 36; padding 8px 8px; border-radius 4; background #ED4B52; display:flex; align-items:center; justify-content:center; overflow hidden`; inner container padding 0 8; text "End" Montserrat Medium 500, 14px / 18px, ls 0.25px, #FFFFFF.

---

## 1. Active Call (2280:15348)

```
Panel
├─ Header  (title "On a call"; right: timer chip "02:14" + minimize/open/close)
└─ main content: flex:1 0 0; flex-direction:column; align-items:center; justify-content:center;
                 gap 20; padding 32px 20px; width 100%
   ├─ contacts (§0.4)
   │   ├─ Avatar 48, bg #B23C69, "CA" SemiBold 16/20 ls .15 #FFFFFF
   │   ├─ "Charlie Apegian"  (SemiBold 16/20 ls .15 #FFFFFF)
   │   ├─ text column gap 8: "(555)-123-4567", "Creative Solutions LLC" (Medium 14/18 ls .25 #FFFFFF, centered)
   │   └─ Link button: display:flex; gap 8; height 24; align-items:center
   │        ├─ "Contact Details"  Medium 14/18 ls .25 #87CFE7
   │        └─ 20×20 c-chevron-right.svg (#87CFE7)
   ├─ Actions (§0.3) — all 5 in DEFAULT state
   └─ End button (§0.5)
```
No green banner, no bottom nav.

## 2. Muted + on hold (2280:15425)
Identical structure/values to Active Call except the Actions:
- Mute → ON: white circle, `c-mic-dark.svg`, label "Unmute" #FFFFFF.
- Hold → ON: white circle, `c-play-dark.svg`, label "Resume" #FFFFFF.
- Keypad → DISABLED: item opacity 0.25 (circle #5F6475, `c-dialpad-disabled.svg`, label #8D99AE).
- Add, Transfer → default.
Header still "On a call" + "02:14" chip. No banner, no bottom nav.

## 3. In-call keypad (2280:15502)

```
Panel
├─ Header  (title "On a call"; NO timer chip; minimize/open/close only)
├─ Green call banner (§0.2): phone | divider | [CA avatar 32 #007FAD] "Charlie Apegian" ...... "00:02" >
└─ main content: flex:1 0 0; flex-direction:column; align-items:center; justify-content:flex-start;
                 gap 32; padding 20; width 100%
   ├─ wrapper: flex column; gap 16; width 100%
   │   └─ Input field: height 40; width 100%
   │        box: border 1px solid #5F6475; radius 8; padding 8; display:flex; align-items:center; gap 8
   │        ├─ text (flex 1, height 18): "14#" Montserrat Medium 500, 14/18, ls .25, #FFFFFF, ellipsis
   │        └─ 24×24 c-input-close.svg (white)
   └─ group: flex column; align-items:center; gap 20
       ├─ keypad: inline-grid; grid-template-columns repeat(3, auto); 4 rows; column-gap 24; row-gap 16
       │    12 buttons: 48×48, radius 200, bg #5F6475, padding 8, centered;
       │    label Montserrat SemiBold 600, 14px / 18px, ls 0, #FFFFFF, centered
       │    order: 1 2 3 / 4 5 6 / 7 8 9 / * 0 #
       │    (same size as known keypad: 48px; no letter sub-labels)
       │    grid size: 3·48 + 2·24 = 192 wide; 4·48 + 3·16 = 240 tall
       └─ text button: display:flex; gap 8; align-items:center; justify-content:center
            "Hide keypad"  Montserrat Medium 500, 14/18, ls .25, #FFFFFF (white, NOT blue)
```
No call-control buttons, no End button, no bottom nav.

## 4. Contact details in call (2280:15630)

```
Panel
├─ Header  (title "Phone"; NO timer chip)
├─ Green call banner (§0.2) — identical to In-call keypad
└─ main content: flex:1 0 0; flex-direction:column; align-items:center; justify-content:center;
                 gap 20; padding 20; overflow hidden; width 100%
   └─ Card content: flex:1 0 0; flex-direction:column; align-items:flex-start; gap 12; width 100%
      │            (no bg/border; bottom radii 8 — invisible)
      ├─ Back row: flex; align-items:center; width 100%
      │   └─ button: flex; gap 8; height 24; align-items:center
      │        ├─ 20×20 c-chevron-left.svg (#87CFE7)
      │        └─ "Back to call"  Medium 14/18 ls .25 #87CFE7
      ├─ column: flex column; gap 16; width 100%
      │   └─ Contact Info row: flex; align-items:center; gap 16; width 100%
      │       ├─ Avatar 48×48, radius 100, bg #B23C69, "CA" SemiBold 16/20 ls .15 #FFFFFF
      │       └─ Contact Details: flex:1 0 0; min-width 0; flex column; gap 8; align-items:flex-start
      │           ├─ Name row: flex; gap 8; height 20; align-items:center
      │           │   (Figma has width 538 — an artifact; use auto / 100%)
      │           │   ├─ "Charlie Apegian"  SemiBold 600, 16/20, ls .15, #87CFE7
      │           │   ├─ 20×20 c-rmx.svg (#87CFE7 building/RMX glyph)
      │           │   └─ 20×20 c-info.svg (#87CFE7 info-outlined)
      │           └─ container: flex column; gap 8; width 100%; align-items:flex-start
      │               ├─ Badge: height 24; padding 4px 8px; radius 4; bg #E2E6F5;
      │               │   "Superuser" Medium 14/18 ls .25 #363B4D
      │               ├─ Email row: flex; gap 8; align-items:center; width 100%
      │               │   ├─ 18×18 c-mail.svg (#87CFE7)
      │               │   └─ "thisisaverylongemailIdontknowwhy@email.com"
      │               │       Montserrat Medium 500, 14px, line-height normal, ls 0.4px, #87CFE7,
      │               │       flex:1 0 0; min-width 0; overflow hidden; text-overflow ellipsis; nowrap
      │               └─ Phone row: flex; gap 8; align-items:center
      │                   ├─ 18×18 c-phone-blue.svg (#87CFE7)
      │                   └─ "(123) 456-7890"  Medium 14, lh normal, ls 0.4, #87CFE7
      ├─ Divider: width 100%, 1px #5F6475  (c-divider.svg 360×1, or border-top 1px solid #5F6475)
      ├─ Info column: flex column; gap 12; width 100%
      │   ├─ row gap 8, align center (Medium 14/18 ls .25):
      │   │    "Company" #8D99AE  +  "Creative Solutions LLC" #87CFE7 (ellipsis)
      │   ├─ row gap 16, align center:
      │   │    "Type" Medium 14/18 ls .25 #8D99AE
      │   │    Lozenge: height 24; padding 4px 8px; radius 4; bg #BCC4E8; "Regular Company" Medium 14/18 ls .25 #363B4D
      │   │    sub-row gap 8: 16×16 c-building.svg (#C47000) + "Per Unit" Medium 14/18 ls .25 #FFFFFF
      │   └─ row gap 8, align center (Montserrat Medium 14, lh normal, ls 0.4):
      │        "Company Code" #8D99AE  +  "CSLLC" #FFFFFF
      ├─ Divider (same as above)
      ├─ Tickets column: flex column; gap 12; width 100%
      │   ├─ Header row: flex; justify-content:space-between; align-items:center; width 100%
      │   │   ├─ "Recent Tickets"  SemiBold 600, 14/18, ls 0.1, #8D99AE
      │   │   └─ button: flex; gap 8; height 18; align center
      │   │        "See 5 tickets" Medium 14/18 ls .25 #87CFE7 + 20×20 c-arrow-drop-down.svg (#87CFE7)
      │   └─ list: flex column; gap 8; width 100%; Medium 500, 14/18, ls .25
      │        each row: flex; gap 16; align center; width 100%
      │          id (#87CFE7, shrink 0)  + title (#FFFFFF, flex 1, min-width 0, ellipsis, nowrap)
      │          345234  Can’t Connect to Server      (id text in Figma has 2 trailing spaces, whitespace pre)
      │          544364  Error in distribution calculation
      │          544365  Missing data in input file
      │          544366  Invalid format for date entry
      │          654347  User unable to access document after creation   (truncates → "after…")
      └─ Add Ticket button: width 100%; height 36; padding 8; radius 4; bg #007FAD; border 1px solid #007FAD;
           centered; inner padding 0 8; "Add Ticket" Medium 14/18 ls .25 #FFFFFF
```
No bottom nav.

## 5. Unknown caller in call (2280:15767)

```
Panel
├─ Header  (title "On a call"; timer chip "02:14")
└─ main content: flex:1 0 0; column; align-items:center; justify-content:center; gap 20; padding 32px 20px
   ├─ contacts (§0.4)
   │   ├─ Avatar 48×48, radius 100, bg #8D99AE, padding 10, centered:
   │   │    32×32 c-person-placeholder.svg (white person)
   │   ├─ "(555) 987-6543"  SemiBold 16/20 ls .15 #FFFFFF
   │   └─ text column: "Not in contacts"  Medium 14/18 ls .25 #FFFFFF centered
   │   (no "Contact Details" link)
   ├─ Actions (§0.3) — all DEFAULT
   ├─ "Who is this?" card: width 100%; flex column; gap 16; padding 16; radius 4;
   │     border 1px solid #5F6475; background: rgba(255,255,255,0.1) over #363B4D
   │     (= linear-gradient(rgba(255,255,255,.1),rgba(255,255,255,.1)), #363B4D)
   │   ├─ "Who is this?"  Medium 14/18 ls .25 #FFFFFF, width 100%
   │   └─ row: flex; gap 16; align-items:center; width 100%
   │       ├─ Secondary button: height 36; padding 0 8; radius 4; bg #F2F3F7; inner padding 0 8;
   │       │    "New Contact" Medium 14/18 ls .25 #5F6475
   │       └─ Secondary button (same): "Link to Existing"
   └─ End button (§0.5)
```
No banner, no bottom nav.

---

## Asset index (all SVG, root width×height)
| File | Size | Color | Used in |
|---|---|---|---|
| c-header-drag.svg | 24×24 | #CED0D4 | header left |
| c-header-minimize.svg | 20×20 | #CED0D4 | header |
| c-header-open-in-new.svg | 20×20 | #CED0D4 | header |
| c-header-close.svg | 20×20 | #CED0D4 | header |
| c-chevron-right.svg | 20×20 | #87CFE7 | "Contact Details" link |
| c-chevron-left.svg | 20×20 | #87CFE7 | "Back to call" |
| c-banner-chevron-right.svg | 20×20 | white | green banner right |
| c-banner-phone.svg | 20×20 | #94CC86 | green banner left |
| c-banner-divider.svg | 23×1 | stroke #CED0D4 | banner vertical divider (rotate 90°) |
| c-mic-off.svg | 20×20 | white | Mute default |
| c-mic-dark.svg | 20×20 | #5F6475 | Mute ON (Unmute) |
| c-pause.svg | 20×20 | white | Hold default |
| c-play-dark.svg | 20×20 | #5F6475 | Hold ON (Resume) |
| c-dialpad.svg | 20×20 | white | Keypad default |
| c-dialpad-disabled.svg | 20×20 | white (identical glyph) | Keypad disabled (item opacity .25) |
| c-person-add.svg | 20×20 | white | Add |
| c-transfer.svg | 20×20 | white | Transfer |
| c-input-close.svg | 24×24 | white | in-call keypad input clear |
| c-rmx.svg | 20×20 | #87CFE7 | contact details name row |
| c-info.svg | 20×20 | #87CFE7 | contact details name row |
| c-mail.svg | 18×18 | #87CFE7 | email row |
| c-phone-blue.svg | 18×18 | #87CFE7 | phone row |
| c-divider.svg | 360×1 | stroke #5F6475 | contact details section dividers |
| c-building.svg | 16×16 | #C47000 | "Per Unit" row |
| c-arrow-drop-down.svg | 20×20 | #87CFE7 | "See 5 tickets" |
| c-person-placeholder.svg | 32×32 | white | unknown caller avatar |

Color tokens used: #363B4D panel/text-primary · #5F6475 secondary · #8D99AE accent · #CED0D4 neutral-500 · #87CFE7 blue-500 (links) · #007FAD button-primary · #ED4B52 error/End · #B23C69 avatar magenta · #94CC86 call green · #E2E6F5 purple-400 · #BCC4E8 purple-500 · #F2F3F7 button-secondary · #C47000 company icon.
