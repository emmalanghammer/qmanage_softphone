# Group B — Idle tabs (Figma file 6iYNH8CMLcJZCto956H6ZC)

Screens: Keypad - empty (2278:13198), Contacts (2278:13447), Contacts - no results (2278:13599),
Users / "Extensions" tab (2278:13664), History (2278:13001), History - No missed calls (2278:12944).

Font family everywhere: Montserrat. Weights: Medium = 500, SemiBold = 600.
All icon assets live in `assets/icons/`. Render every `<img>` at the stated box size (the SVG root
width/height already matches it; don't stretch it).

---

## 0. Shared chrome (same on all 6 screens)

Panel, top header and bottom nav match the ALREADY KNOWN spec exactly. No deviations found.
Panel = column, `justify-content: space-between`, `overflow: hidden`, padding 0.

### Top header icons
| Slot | Asset | Rendered box | SVG root | Fill |
|---|---|---|---|---|
| Left drag button (40×40, padding 8, radius 200) | `b-header-drag.svg` | 24×24 | 24×24 | #CED0D4 |
| Minimize (40×40 button) | `b-header-minimize.svg` | 20×20 | 20×20 | #CED0D4 |
| Pop-out / open in new | `b-header-popout.svg` | 20×20 | 20×20 | #CED0D4 |
| Close | `b-header-close.svg` | 20×20 | 20×20 | #CED0D4 |

Left side: flex row, gap 8, align center (drag button + "Phone"). Right side: flex row, gap 0.

### Bottom nav
Row, `justify-content: space-between`, align center, padding 12, width 400, background
`linear-gradient(rgba(0,0,0,.1),rgba(0,0,0,.1)), #363B4D`. No top border.
Each item: width 75, column, gap 4, align+justify center, padding 4, radius 4, overflow hidden.
Icon box 20×20. Label Montserrat Medium 12px / line-height 14px / letter-spacing 0.4px, centered,
nowrap; active label #FFFFFF, inactive label #8D99AE.

| Tab | Active asset (white fill) | Inactive asset (#8D99AE fill) | Active on screen |
|---|---|---|---|
| Keypad | `b-nav-keypad-active.svg` | `b-nav-keypad-inactive.svg` | Keypad - empty |
| Contacts | `b-nav-contacts-active.svg` | `b-nav-contacts-inactive.svg` | Contacts, Contacts - no results |
| Extensions | `b-nav-extensions-active.svg` | `b-nav-extensions-inactive.svg` | Users |
| History | `b-nav-history-active.svg` | `b-nav-history-inactive.svg` | History, History - No missed calls |

All nav SVGs are 20×20 at the root.

### Shared list-row building blocks (Contacts and Extensions)
- **Divider:** `b-divider-line.svg` (root 360×1, stroke #5F6475, 1px). In Figma it's a 0-height
  full-width box with the img positioned `inset: -1px 0 0 0`. CSS equivalent:
  `height:0; border-top:1px solid #5F6475` (or `height:1px; background:#5F6475`). It sits as its
  own child in the list column, so the list's 12px gap applies above and below it.
- **Avatar:** 24×24, radius 100, bg #B23C69, column, centered, overflow hidden (Figma padding 10;
  ignore it and just center the text). Initials: Montserrat SemiBold 12px, line-height normal,
  letter-spacing 0.1px, #FFFFFF, centered.
- **Trailing call button:** 36×36, padding 0 4px, radius 4, flex centered, overflow hidden, no
  background. Contains a 24×24 icon `b-contact-call-green.svg` (fill #94CC86, root 24×24).

---

## 1. Keypad - empty (2278:13198)

Main content (between header and nav): `flex: 1 0 0`, column, `align-items: center`,
`justify-content: space-between`, padding 20, width 100%.

1. **Input field**: width 100%, height 40, column, justify center, gap 4.
   - Inner box: `flex: 1 0 0` (fills the 40px), width 100%, border 1px solid #5F6475, radius 8,
     padding 8, row, align center, gap 8, overflow hidden. **No trailing icon in the empty state.**
   - Text container: `flex: 1 0 0`, height 18.
   - **Placeholder** "Enter a name or number": Montserrat **Medium Italic** (weight 500,
     `font-style: italic`), 14px, line-height 18px, letter-spacing 0.25px, color **#CED0D4**,
     nowrap, `overflow: hidden; text-overflow: ellipsis`, left-aligned.
2. **Keypad grid**: `display: inline-grid`, 3 columns of fit-content, 5 rows, column-gap 24,
   row-gap 16. It stays centered horizontally, and `space-between` pushes it to the bottom of the
   main content.
   - Rows 1–4: "1" "2" "3" / "4" "5" "6" / "7" "8" "9" / "*" "0" "#". Each is 48×48, radius 200,
     bg #5F6475, padding 8, centered. Label Montserrat SemiBold 14px / 18px, ls 0, #FFFFFF, centered.
   - Row 5, column 2: **disabled call button**. 48×48, radius 200, padding 8, centered,
     **bg #4A6643** (token color/green/700, instead of the active #94CC86). Icon 20×20
     `b-call-disabled-green.svg`: the phone glyph is fill **#253322** (dark green), root 20×20.
     No opacity is applied in Figma; the colors themselves carry the disabled look.

Nav: Keypad active.

---

## 2. Contacts (2278:13447)

Main content: `flex: 1 0 0`, column, `align-items: center`, **gap 20**, padding 20, overflow
hidden, width 100%. Items are top-aligned (no space-between).

1. **Search bar**: wrapper is a column, centered, width 100%. Inner box: height 40, width 100%,
   border 1px solid #5F6475, radius 8, padding 8px 12px, row, align center, gap 8, overflow hidden.
   - Label container `flex: 1 0 0`, row, align center.
   - Placeholder "Search contacts": Montserrat Medium 16px / line-height 20px / ls 0.5px, color
     #8D99AE, nowrap.
   - Trailing icon 24×24 `b-search.svg` (fill white, root 24×24).
2. **List** ("Recent Calls List"): column, gap 12, align start, width 100%. The rows alternate
   with dividers: row, divider, row, divider, … row. There are 6 rows and 5 dividers, with no
   divider after the last row.
   - **Row**: width 100%, row, `justify-content: space-between`, align center.
     - Left side: row, gap 4, align center.
       - Avatar (see shared).
       - Text column: gap 4, align start, justify center.
         - Line 1 ("Recent Call Info"): row, gap 8, align center, nowrap.
           - Name: Montserrat SemiBold 12px / 16px / ls 0.1px, #FFFFFF.
           - Company: Montserrat Medium 12px / 14px / ls 0.4px. Color varies per row (see table).
         - Line 2: row, gap 8, align start. Number: Montserrat Medium 12px / 14px / ls 0.4px, #8D99AE.
     - Right: call button 36×36 with `b-contact-call-green.svg` 24×24.

| # | Initials | Name | Company | Company color | Number |
|---|---|---|---|---|---|
| 1 | CA | Charlie Apegian | Creative Solutions LLC | #FFFFFF | (555) 123 -4567 |
| 2 | EF | Eleanor Foster | Creative Solutions LLC | #FFFFFF | (555) 123 -4567 |
| 3 | JS | Joe Smith | Apple | #CED0D4 | (555) 123 -4567 |
| 4 | PR | Pam Reynolds | Zendesk | #CED0D4 | (555) 123 -4567 |
| 5 | ML | Marcus Lee | Zeplin | #CED0D4 | (555) 123 -4567 |
| 6 | ML | Henry Rhodes | Smoothie King | #CED0D4 | (555) 123 -4567 |

Notes, kept verbatim from Figma:
- The number string really is "(555) 123 -4567", with a space before the hyphen.
- Henry Rhodes really has the initials "ML" in Figma, a likely copy-paste error; use "HR" if you
  prefer correctness.
- Company color is inconsistent: white on rows 1–2, #CED0D4 on rows 3–6. #CED0D4 is probably the
  intent.

Nav: Contacts active.

---

## 3. Contacts - no results (2278:13599)

Main content: `flex: 1 0 0`, column, align center, **gap 24**, padding 20, overflow hidden.

1. **Search bar (filled/focused)**: same geometry as on Contacts, but the **border is 1px #8D99AE**
   instead of #5F6475.
   - Value "Zepplin corp": Montserrat Medium 16px / 20px / ls 0.5px, **#FFFFFF**.
   - Trailing icon 24×24 `b-search-clear.svg` (an X, fill white, root 24×24), replacing the search icon.
2. **Empty-state block**: `flex: 1 0 0` (fills the remaining height), column, gap 24, align center,
   justify center, width 100%.
   - Text group: width 306, column, gap 12, align center, Montserrat Medium.
     - Title `No contacts match "Zepplin corp"` (straight double quotes): 14px / 18px / ls 0.25px,
       #FFFFFF, text-align center, width 100%.
     - Subtitle "Check the spelling, or search by phone number": 12px / 14px / ls 0.4px, #8D99AE,
       width 100%. Figma sets no text-align, but the text nearly fills 306px; use center.
   - **Primary button "Add Contact"**: height 36, bg #007FAD, border 1px solid #007FAD, radius 4,
     padding 8px 8px, overflow hidden. Inner container has padding 0 8px, centered. Label Montserrat
     Medium 14px / 18px / ls 0.25px, #FFFFFF, nowrap. Effective horizontal padding: 16 + 1px border.

Nav: Contacts active.

---

## 4. Users — Extensions tab (2278:13664)

Main content: identical to Contacts (gap 20, padding 20, column, align center, overflow hidden).

1. **Search bar**: identical to Contacts. Placeholder "Search extensions" in #8D99AE, icon
   `b-search.svg` 24×24, border #5F6475.
2. **List**: column, gap 12, width 100%. Pattern: row, divider, … row, divider. There are 5 rows
   and **5 dividers; unlike Contacts, a divider does follow the last row.**
   - Row layout matches Contacts, with these differences:
     - Line 1: Name SemiBold 12/16 ls 0.1 #FFFFFF, then a gap of 8, then **Title** in Medium
       12/14 ls 0.4 **#CED0D4** (#CED0D4 on every row).
     - Line 2: row, **gap 12**, align center:
       - "Ext. NNN": Medium 12/14 ls 0.4, #8D99AE.
       - Status group: row, gap 4, align center. An 8×8 dot (presence SVG, root 8×8, a filled
         circle) followed by the status text: Medium 12px / 14px / ls 0.4px, #8D99AE.
   - Right: call button 36×36 with `b-contact-call-green.svg` 24×24.

| # | Initials | Name | Title | Ext | Status text | Dot asset | Dot color |
|---|---|---|---|---|---|---|---|
| 1 | CA | Charlie Stile | Product Support Specialist I | Ext. 204 | Available | `b-presence-available.svg` | #94CC86 |
| 2 | EF | Eleanor Foster | Product Support Specialist II | Ext. 201 | Available | `b-presence-available.svg` | #94CC86 |
| 3 | JS | Joe Smith | Product Support Specialist I | Ext. 207 | On a call | `b-presence-busy.svg` | #ED4B52 |
| 4 | PR | Pam Reynolds | Product Support Manager | Ext. 210 | Away | `b-presence-away.svg` | #FFA630 |
| 5 | ML | Marcus Lee | Product Support Team Lead | Ext. 212 | Offline | `b-presence-busy.svg` | #ED4B52 |

Offline uses the same red dot as "On a call" in Figma (the same asset).

Nav: Extensions active.

---

## 5. History (2278:13001)

Main content: `flex: 1 0 0`, column, align center, gap 20, **padding 16px 20px** (16 top/bottom,
20 left/right), overflow hidden.

1. **Segmented control ("tabs")**: width 100%, bg #5F6475, radius 4, padding 2, row, align center,
   no gap.
   - Each segment: `flex: 1 0 0`, padding 8, radius 4, centered.
     Label Montserrat SemiBold 14px / 18px / ls 0, centered, nowrap.
   - **Selected** segment "All": bg **#F4F6FB**, label **#363B4D**.
   - **Unselected** segment "Missed (2)": no bg (transparent over #5F6475), label #FFFFFF.
   - Height: 18 + 16 + 4 = 38.
2. **Recent list**: column, gap 12, align start, width 100%, overflow hidden, padding-top 0.
   The list **starts with a divider**. The order of children is:
   divider, R1, divider, R2, divider, R3, divider, R4, divider, R5, divider, R6, **R7 (no divider
   between R6 and R7)**. There is no trailing divider. Divider: `b-divider-line.svg`, #5F6475 1px.
   - **Row**: width 100%, row, `justify-content: space-between`, align center.
     - Left side: **width 250**, row, gap 4, `align-items: flex-start`.
       - Direction icon 24×24 (see table).
       - Text column: gap 4, align start, justify center, nowrap.
         - Primary: Montserrat **SemiBold 14px / 18px / ls 0.1px**, #FFFFFF (name or number).
         - Meta row: row, gap 8, align start. Three separate text nodes (direction, date, time),
           each Montserrat Medium 12px / 14px / ls 0.4px, #8D99AE.
     - Duration: Montserrat Medium 14px / 18px / ls 0.25px, #FFFFFF, width 40 (rows R1, R3, R4, R5)
       or auto-width centered (R7). On missed rows the text is still present ("05:23" / "16:32")
       but its color is **transparent**. Render an invisible placeholder so the layout stays the
       same: `visibility:hidden` or `color:transparent`.
     - Call button 36×36, padding 0 4, radius 4, with a 24×24 icon `b-history-call-green.svg`
       (#94CC86; byte-identical to `b-contact-call-green.svg`).

| Row | Icon asset | Icon color | Primary text | Direction | Date | Time | Duration |
|---|---|---|---|---|---|---|---|
| R1 | `b-history-incoming.svg` | #94CC86 | (555) 123-4567 | Incoming | 03/17/26 | 6:38 PM | 05:23 |
| R2 | `b-history-missed.svg` | #ED4B52 | Charlie Apegian | Missed | 03/17/26 | 12:55 PM | (hidden "05:23") |
| R3 | `b-history-incoming.svg` | #94CC86 | (589) 216-4863 | Incoming | 03/17/26 | 11:38 AM | 35:08 |
| R4 | `b-history-incoming.svg` | #94CC86 | Joe Smith | Incoming | 03/17/26 | 09:15 AM | 23:54 |
| R5 | `b-history-outgoing.svg` | #94CC86 | Pam Reynolds | Outgoing | 03/16/26 | 5:28 PM | 16:32 |
| R6 | `b-history-missed.svg` | #ED4B52 | Pam Reynolds | Missed | 03/16/26 | 5:08 PM | (hidden "16:32") |
| R7 | `b-history-incoming.svg` | #94CC86 | (360) 296-1400 | Incoming | 03/16/26 | 11:38 AM | 35:08 |

Icon shapes: incoming is an arrow pointing down-left, outgoing an arrow pointing up-right, and
missed a bent red arrow pointing down-left.

Figma oddities:
- R5 and R6 have a trailing space in the name ("Pam Reynolds ").
- The phone format here is "(555) 123-4567", with no space before the hyphen, unlike Contacts.
- The phone-number SemiBold text and the names use the same style.
- The missed-call primary text stays **white**. Only the icon is red.
- The list is clipped by `overflow: hidden`, and R7 sits just above the nav in the 600px frame.
  For the build, make the list scroll (`overflow-y:auto`) instead.

Nav: History active.

---

## 6. History - No missed calls (2278:12944)

Main content: column, align center, gap 20, **padding 20** (all sides; differs from History's 16/20).

1. **Segmented control**: identical to History. Note that Figma still shows **"All" as selected**
   (#F4F6FB bg) and "Missed (2)" unselected here, which is likely a design error. The empty copy is
   meant for the Missed tab. Recommendation: render Missed as selected in this state (same styles,
   swapped), and confirm with the designer.
2. **Empty state**: `flex: 1 0 0`, column, gap 12, align center, justify center, width 100%,
   Montserrat Medium.
   - "No missed calls": 14px / 18px / ls 0.25px, #FFFFFF, centered.
   - "You're all caught up." (straight apostrophe): 12px / 14px / ls 0.4px, #8D99AE, nowrap
     (renders centered because its parent uses align-items:center).

Nav: History active.

---

## Asset inventory (assets/icons/)

| File | Root W×H | Color(s) | Used for |
|---|---|---|---|
| b-header-drag.svg | 24×24 | #CED0D4 | header drag handle |
| b-header-minimize.svg | 20×20 | #CED0D4 | header minimize |
| b-header-popout.svg | 20×20 | #CED0D4 | header open-in-new |
| b-header-close.svg | 20×20 | #CED0D4 | header close |
| b-nav-keypad-active.svg | 20×20 | white | nav |
| b-nav-keypad-inactive.svg | 20×20 | #8D99AE | nav |
| b-nav-contacts-active.svg | 20×20 | white | nav |
| b-nav-contacts-inactive.svg | 20×20 | #8D99AE | nav |
| b-nav-extensions-active.svg | 20×20 | white | nav |
| b-nav-extensions-inactive.svg | 20×20 | #8D99AE | nav |
| b-nav-history-active.svg | 20×20 | white | nav |
| b-nav-history-inactive.svg | 20×20 | #8D99AE | nav |
| b-call-disabled-green.svg | 20×20 | #253322 | disabled keypad call button (on bg #4A6643) |
| b-search.svg | 24×24 | white | search bar trailing icon (empty) |
| b-search-clear.svg | 24×24 | white | search bar clear X (with value) |
| b-contact-call-green.svg | 24×24 | #94CC86 | row call button (Contacts/Extensions) |
| b-history-call-green.svg | 24×24 | #94CC86 | row call button (History), identical to the above |
| b-divider-line.svg | 360×1 | stroke #5F6475 | list dividers |
| b-presence-available.svg | 8×8 | #94CC86 | Available dot |
| b-presence-busy.svg | 8×8 | #ED4B52 | On a call / Offline dot |
| b-presence-away.svg | 8×8 | #FFA630 | Away dot |
| b-history-incoming.svg | 24×24 | #94CC86 | incoming direction icon |
| b-history-outgoing.svg | 24×24 | #94CC86 | outgoing direction icon |
| b-history-missed.svg | 24×24 | #ED4B52 | missed direction icon |

(The #D9D9D9 fills inside several SVGs are alpha-mask rectangles, not visible colors.)
