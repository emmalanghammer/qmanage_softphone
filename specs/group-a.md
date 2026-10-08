# Group A spec: header button, minimized bars, incoming call

Figma fileKey `6iYNH8CMLcJZCto956H6ZC`. All fonts are Montserrat. Weights: Medium = 500, SemiBold = 600.
Assets live in `assets/icons/`. Every SVG has root width/height attributes (listed below). Render each one at that size and don't override it.

## Shared tokens used in this group

| Token | Value |
|---|---|
| panel / bar bg (neutrals/800, text/primary) | `#363B4D` |
| text/on-primary | `#FFFFFF` |
| text/accent | `#8D99AE` |
| text/secondary | `#5F6475` |
| status/success (green button) | `#94CC86` |
| status/error (red button) | `#ED4B52` |
| green/700 | `#4A6643` |
| green/600 | `#6F9965` |
| green/800 | `#253322` |
| blue/500 (links on dark) | `#87CFE7` |
| avatar magenta | `#B23C69` |
| red/600 (app avatar) | `#A4495D` |
| app header border | `#CED0D4` |
| button-secondary / selector bg | `#F2F3F7` |
| button-primary | `#007FAD` |
| Dropshadow/SM | `0 0 2px 0 rgba(0,0,0,.16), 0 1px 4px 0 rgba(0,0,0,.16)` |

**Standard button ("Button" instance):** `display:flex; align-items:center; height:36px; padding:8px 8px; border-radius:4px; overflow:hidden`. It has an inner "Container" with `display:flex; justify-content:center; align-items:center; padding:0 8px`. The label is Medium 14/18, ls 0.25px, `white-space:nowrap`. Some variants add a 1px solid border, so they stay 36px tall overall (Figma border is inside the box, so use `box-sizing:border-box`).

Text styles:
- **title/xs**: SemiBold 12/16, ls 0.1
- **title/small**: SemiBold 14/18, ls 0.1
- **title/medium**: SemiBold 16/20, ls 0.15
- **body/small**: Medium 12/14, ls 0.4
- **body/medium**: Medium 14/18, ls 0.25
- **body/large**: Medium 16/20, ls 0.5

---

## 1. Header button all states (node 2274:2428)

The frame is a column with `gap:20px` and 4 rows. Each row is the full qManage app header: **1920 x 64**. Only the first button in the right-side "Buttons" group changes between states.

### App header row (same for all 4)
`display:flex; align-items:center; gap:16px; padding:8px 24px 12px 24px; background:#FFFFFF; border-bottom:1px solid #CED0D4; overflow:hidden; width:100%` (height 64).

1. **Header Left Container**: `flex:1 0 0; display:flex; gap:16px; align-items:center` (670 wide).
   - Menu icon, 24x24: `a-hdr-menu.svg` (24x24, fill #5F6475)
   - Logo, 195x44: `a-hdr-logo.svg` (195x44)
2. **Search bar**: `width:500px; min-width:250px; flex-shrink:0`.
   - Inner box: `display:flex; gap:8px; align-items:center; height:40px; padding:8px 12px; background:#F2F3F7; border-radius:8px`.
   - Label "Search qManage": body/large (Medium 16/20, ls 0.5), color `#8D99AE`, `flex:1`.
   - Search icon, 24x24: `a-hdr-search.svg` (24x24, fill #007FAD)
3. **Right Content**: `flex:1 0 0; display:flex; justify-content:flex-end; align-items:center` (670 wide).
   - "regular content": `display:flex; gap:24px; align-items:center`.
     - **Buttons**: `display:flex; gap:16px; align-items:center`.
       1. **[STATE BUTTON]**, see the table below.
       2. Remote Support button: bg `#F2F3F7`, height 36, padding 0 8px, radius 4, no border, width 174.
          - Leading icon 20x20: `a-hdr-agent.svg` (20x20, fill #5F6475)
          - Container padding 0 8px. Label "Remote Support" body/medium in color `#5F6475`.
       3. Add Ticket button: bg `#007FAD`, `border:1px solid #007FAD`, height 36, padding 8px, radius 4, width 110. Label "Add Ticket" body/medium in white. No icons.
       4. Inner "Buttons" group: `display:flex; gap:12px; align-items:center`.
          - A sub-row `display:flex; gap:16px` holding:
            - `a-hdr-communication.svg` 24x24 (chat, fill #5F6475)
            - `a-hdr-notifications.svg` 24x24 (fill #5F6475)
          - Ticket Summary Button: 30x30, bg white, radius 16, padding 4px 8px, centered. Holds `a-hdr-ai-star-color.svg` 20x20 (gradient star #00A6E0 / #50239D).
     - **Avatar**: 32x32, radius 100, bg `#A4495D`, padding 10, centered. Holds `a-hdr-person.svg` 14x14 (white).

### State button (first item in Buttons)

| Row | State | Rendering |
|---|---|---|
| 1 | idle | Icon button 36x36, bg `#F2F3F7`, radius 4, padding 0 4px, centered. Holds `a-hdr-add.svg` 24x24 (plus, fill #5F6475). |
| 2 | Incoming | Green chip, text "Incoming..." (width 133) |
| 3 | Ringing | Green chip, text "Ringing..." |
| 4 | active | Green chip, text "00:02" |

**Green call chip** (rows 2 to 4): `display:flex; align-items:center; height:36px; padding:8px; background:#94CC86; border-radius:4px; overflow:hidden; no border`. Children:
- Container `padding:0 8px`, label body/medium (Medium 14/18, ls 0.25) in color `#253322` (green/800).
- Trailing icon 20x20, directly after the container with no gap: `a-hdr-call-chip-phone.svg` (20x20). It is a phone-in-call glyph, fill `#363B4D`.

Interactive: the state button is clickable. In the idle state it is the "+" (add/new call). In the call states it opens or focuses the softphone. In row 4 the label is a live timer (mm:ss).

---

## 2. Minimized bars (node 2277:10515)

The frame is **500 x 420**: a column with `gap:20px` holding 5 bars. Each bar is **500 x 68**.

### Bar container (same for all 5)
`display:flex; align-items:center; justify-content:space-between; padding:16px; background:#363B4D; border-radius:8px; box-shadow:0 0 2px rgba(0,0,0,.16), 0 1px 4px rgba(0,0,0,.16); overflow:hidden; width:100%`.

**Left side**: `display:flex; gap:16px; align-items:center`.
- Drag handle, 24x24: `a-drag-indicator.svg` (24x24, fill #CED0D4)
- contact: `display:flex; gap:8px; align-items:center`.
  - Avatar: 24x24, radius 100, bg `#B23C69`, centered.
    - Text "CA": SemiBold 12, line-height normal, ls 0.1, white, centered. The node has padding 10 but is fixed 24x24, so center the text.
  - Name: title/small (SemiBold 14/18, ls 0.1), white.
    - In bars 1 to 4 the name is drawn on **two lines**, "Charlie" / "Apegian". The text box is 62 wide x 36 tall. Implement with an explicit line break or `max-width:62px`.
    - In bar 5 it is a single line, "3 people" (18 tall). Its left side is 24 tall, vertically centered.

**Right side**: `display:flex; gap:16px; align-items:center`.
- Status text: body/small (Medium 12/14, ls 0.4), white, nowrap.
- Button(s): see the per-bar table.
- Expand icon, 24x24: `a-expand-content.svg` (24x24, fill #CED0D4). Clicking it restores the full panel.

### Per-bar contents

| # | Node | Status text | Buttons (in order) |
|---|---|---|---|
| 1 | 2277:10516 Incoming | `Incoming...` | **Decline**: red (bg `#ED4B52`, border 1px `#ED4B52`, white label), 88 wide. **Accept**: green (bg `#94CC86`, border 1px `#94CC86`, label `#363B4D`), 84 wide. |
| 2 | 2277:10529 Calling | `Calling...` | **Cancel**: red bg `#ED4B52`, no border, white label, 82 wide |
| 3 | 2277:10541 Active | `02:14` | **End**: red bg `#ED4B52`, no border, white label, 61 wide |
| 4 | 2277:10554 On hold | `On hold 02:14` | **Resume**: green bg `#94CC86`, border 1px `#94CC86`, label `#363B4D`, 92 wide |
| 5 | 2277:10566 Conference | `Conference 04:10` | **End**: red bg `#ED4B52`, no border, white label, 61 wide |

All buttons are the standard button (height 36, padding 8, radius 4, Container padding 0 8, label Medium 14/18, ls 0.25).

Interactive:
- The whole bar is draggable by the drag handle.
- The buttons perform the call actions.
- The expand_content icon maximizes back to the panel.

---

## 3. Minimized bar - Incoming, wide variant (node 2337:17924)

The bar is **733 x 68**. It has the same container as section 2: `display:flex; align-items:center; justify-content:space-between; padding:16px; bg #363B4D; radius 8; Dropshadow/SM; overflow:hidden`.

It has **3 direct children**, spread out by space-between:
1. **Left side**: `display:flex; gap:8px; align-items:center` (note: gap 8 here, not 16). Size 149x44, so the bar's content height is 44 and the vertical padding visually becomes 12.
   - `a-drag-indicator.svg` 24x24
   - contact: `display:flex; flex-direction:column; gap:8px; align-items:flex-start; justify-content:center`. Text is title/small (SemiBold 14/18, ls 0.1), white, nowrap.
     - "Charlie Apegian"
     - "(555)-123-4567"
   - **No avatar** in this variant.
2. **Status text** "Incoming...": body/small (Medium 12/14, ls 0.4), white. This is a standalone flex child in the middle.
3. **Right side**: `display:flex; gap:8px; align-items:center` (gap 8). Width 400.
   - **Decline** (88w): bg `#ED4B52`, border 1px `#ED4B52`, label white.
   - **Accept & Add Ticket** (180w): bg `#94CC86`, border 1px `#94CC86`, label `#363B4D`.
   - **Accept** (84w): bg `#FFFFFF`, border 1px `#6F9965` (green/600), label `#4A6643` (green/700).
   - `a-expand-content.svg` 24x24

All buttons: height 36, padding 8, radius 4, Container padding 0 8, label Medium 14/18, ls 0.25.

---

## 4. Incoming call - known contact collapsed (node 2337:17873)

The panel is **400 wide x ~256 tall** (48 header + 208 content). It uses the standard 400px panel (bg #363B4D, radius 8, shadow, overflow hidden, column).

**Deviation: there is no bottom nav on any incoming-call screen.**

### Top header ("phone top header", 400 x 48)
Same as the known header:
- padding 4, `background: linear-gradient(rgba(0,0,0,.1),rgba(0,0,0,.1)), #363B4D`, border-bottom `1px solid rgba(255,255,255,.1)`, justify-content space-between.
- Left: `display:flex; gap:8px`.
  - A 40x40 round button (padding 8, radius 200) holding `a-drag-indicator.svg` at 24x24.
  - Title **"Incoming call"**: title/xs (SemiBold 12/16, ls 0.1), white.
- Right: three 40x40 round buttons (padding 8, radius 200, no gap), each with a 20x20 icon:
  - `a-header-minimize.svg` (20x20, #CED0D4)
  - `a-header-open-in-new.svg` (20x20, #CED0D4)
  - `a-header-close.svg` (20x20, #CED0D4)
- **No timer chip.**

### Main content
**Deviation from the known padding of 20:** here it is `padding:32px 16px`, `display:flex; flex-direction:column; gap:32px; align-items:center; width:100%`.

1. **contacts row**: `display:flex; justify-content:space-between; align-items:center; width:100%` (368 x 24).
   - contact: `display:flex; gap:8px; align-items:center`, white, nowrap.
     - "Charlie Apegian": title/medium (SemiBold 16/20, ls 0.15).
     - "(555)-123-4567": body/medium (Medium 14/18, ls 0.25).
   - Chevron, 24x24: `a-incoming-chevron-down.svg` (24x24, fill #87CFE7). **Interactive**: it toggles to the expanded view (section 5).
2. **Button Container**: `display:flex; flex-direction:column; gap:16px; width:100%`.
   - **Accept & Add Ticket**: full width (368), height 36, bg `#94CC86`, no border, radius 4, padding 8, `justify-content:center`. Label `#363B4D`.
   - **Button Row**: `display:flex; gap:8px; width:100%`.
     - **Decline**: `flex:1` (180w), h36, bg `#ED4B52`, no border, radius 4, padding 8, centered. Label white.
     - **Accept**: `flex:1` (180w), h36, bg `#FFFFFF`, border `1px solid #4A6643`, radius 4, padding 4px 8px, centered. Label `#4A6643`.
     - Note: this full-panel Accept uses a green/700 border, while the minimized bar's Accept uses a green/600 border.
   - All labels: Medium 14/18, ls 0.25. Each Container has padding 0 8px.

---

## 5. Incoming call - known contact expanded (node 2333:16397)

The panel is **400 x 664**:
- Header: 48, identical to section 4 ("Incoming call", same icons).
- Main content: 616, with `padding:32px 16px; display:flex; flex-direction:column; gap:32px; align-items:center`.

### Main content children

**A. Wrapper**: `display:flex; flex-direction:column; gap:16px; width:100%` (368 x 432).

1. **contacts row**: same as section 4, but the chevron is `a-incoming-chevron-up.svg` (24x24, #87CFE7). **Interactive**: it collapses back to section 4.
2. **Card content** (368 x 392): `border:1px solid #5F6475; border-radius:8px; padding:12px; display:flex; flex-direction:column; gap:12px; overflow:hidden; width:100%`. No background fill.

   a. **Contact Info row** (344 x 72): `display:flex; gap:16px; align-items:center`.
      - **Avatar**: 48x48, radius 100, bg `#B23C69`, centered. Text "CA" is title/medium (SemiBold 16/20, ls 0.15), white.
      - **Contact Details**: `flex:1; min-width:0; display:flex; flex-direction:column; gap:8px` (280w).
        - Name row: `display:flex; gap:8px; align-items:center; height:20px`.
          - "Charlie Apegian": SemiBold 16/20, ls 0.15, color `#87CFE7`. This is a link.
          - `a-contact-rmx.svg` 20x20 (RMX building glyph, #87CFE7)
          - `a-contact-info-outlined.svg` 20x20 (#CED0D4). This is an info button.
        - Email/phone container: `display:flex; flex-direction:column; gap:8px; width:100%`.
          - Email row: `display:flex; gap:8px; align-items:center; width:100%`.
            - `a-contact-mail-blue.svg` 18x18 (#87CFE7)
            - "thisisaverylongemailIdontknowwhy@email.com": Medium 14, line-height normal (~17px), ls 0.4, color `#87CFE7`. Set `flex:1; min-width:0; overflow:hidden; text-overflow:ellipsis; white-space:nowrap`. It truncates to "thisisaverylongemailIdontknow...".
          - Phone row: `display:flex; gap:8px; align-items:center`.
            - `a-contact-phone-blue.svg` 18x18 (#87CFE7)
            - "(123) 456-7890": Medium 14, line-height normal, ls 0.4, color `#87CFE7`.

   b. **Divider**: `a-card-divider-line.svg` (344x1, stroke #5F6475). Equivalent CSS: `height:0; border-top:1px solid #5F6475; width:100%`.

   c. **Company block**: `display:flex; flex-direction:column; gap:8px`.
      - Row 1: `display:flex; gap:8px; align-items:center`. Text is Medium 14/18, ls 0.25.
        - "Company" in `#8D99AE`
        - "Creative Solutions LLC" in `#87CFE7`, ellipsis.
      - Row 2: `display:flex; gap:8px; align-items:center`.
        - Sub-row: `display:flex; gap:8px; align-items:center`.
          - `a-contact-company-icon.svg` 16x16 (orange #C47000)
          - "Per Unit": Medium 14/18, ls 0.25, white. The source string has a trailing space: "Per Unit ".
        - "Company Code": Medium 14, line-height normal, ls 0.4, `#8D99AE`.
        - "CSLLC": Medium 14, line-height normal, ls 0.4, white.

   d. **Divider**: same as b.

   e. **Recent Tickets column**: `display:flex; flex-direction:column; gap:8px; width:100%`.
      - Header: `display:flex; justify-content:space-between; align-items:center; width:100%`.
        - "Recent Tickets": title/small (SemiBold 14/18, ls 0.1), `#8D99AE`.
        - Link button: `display:flex; gap:8px; height:18px; align-items:center`.
          - "See 5 tickets": Medium 14/18, ls 0.25, `#87CFE7`.
          - `a-tickets-arrow-drop-down-blue.svg` 20x20 (#87CFE7).
          - **Interactive**: it opens or expands the ticket list.
      - Tickets list: `display:flex; flex-direction:column; gap:8px; width:100%`. Text is Medium 14/18, ls 0.25. There are 5 rows.
        - Each row: `display:flex; gap:16px; align-items:center; width:100%`.
          - ID: `#87CFE7`, shrink-0.
          - Description: white, `flex:1; min-width:0; overflow:hidden; text-overflow:ellipsis; white-space:nowrap`.

        | ID | Description |
        |---|---|
        | "345234" (source has 2 trailing spaces) | "Can’t Connect to Server" (curly apostrophe) |
        | "544364" | "Error in distribution calculation" |
        | "544365" | "Missing data in input file" |
        | "544366" | "Invalid format for date entry" |
        | "654347" | "User unable to access document after creation" (truncates) |

      - IDs are clickable links.

   f. **Comment**: `display:flex; flex-direction:column; gap:8px; width:100%`. Text is Medium 14/18, ls 0.25.
      - "Comment" in `#8D99AE`
      - "Comment here!" in white, ellipsis, full width.
   - There is no divider between e and f; only the 12px gap separates them.

**B. Button Container**: identical to section 4 (Accept & Add Ticket full width; Decline / Accept row with gap 8).

---

## 6. Incoming call - unknown number (node 2333:16646)

The Figma layer is misnamed "Incoming call - known contact collapsed". The panel is **400 x ~278**: header 48 plus content 230.

- Header: identical to section 4 ("Incoming call").
- Main content: `padding:32px 16px; gap:32px`, column.
  1. Wrapper: `display:flex; flex-direction:column; gap:8px; width:100%`.
     - contacts row (`display:flex; align-items:center`, **no chevron**): contact `display:flex; gap:8px; align-items:center`, white.
       - "Rochester, NY": title/medium (SemiBold 16/20, ls 0.15).
       - "(555)-987-6543": body/medium (Medium 14/18, ls 0.25).
     - "This caller is not in your contacts.": body/medium (Medium 14/18, ls 0.25), `#8D99AE`. The node is text-align center, but because it hugs its content it renders left-aligned.
  2. Button Container: identical to section 4.

---

## Asset index (assets/icons/)

| File | Root W x H | Color | Used in |
|---|---|---|---|
| a-hdr-menu.svg | 24x24 | #5F6475 | App header hamburger |
| a-hdr-logo.svg | 195x44 | multi | qManage logo |
| a-hdr-search.svg | 24x24 | #007FAD | Search bar |
| a-hdr-add.svg | 24x24 | #5F6475 | Idle state "+" icon button |
| a-hdr-call-chip-phone.svg | 20x20 | #363B4D | Trailing icon in green call chip (Incoming / Ringing / timer) |
| a-hdr-agent.svg | 20x20 | #5F6475 | Remote Support leading icon |
| a-hdr-communication.svg | 24x24 | #5F6475 | Chat icon |
| a-hdr-notifications.svg | 24x24 | #5F6475 | Bell |
| a-hdr-ai-star-color.svg | 20x20 | #00A6E0/#50239D | Ticket Summary button |
| a-hdr-person.svg | 14x14 | white | App avatar |
| a-drag-indicator.svg | 24x24 | #CED0D4 | Minimized bars and panel header drag handle |
| a-expand-content.svg | 24x24 | #CED0D4 | Minimized bar expand/restore |
| a-header-minimize.svg | 20x20 | #CED0D4 | Panel header minimize |
| a-header-open-in-new.svg | 20x20 | #CED0D4 | Panel header pop-out |
| a-header-close.svg | 20x20 | #CED0D4 | Panel header close |
| a-incoming-chevron-down.svg | 24x24 | #87CFE7 | Collapsed contact row chevron |
| a-incoming-chevron-up.svg | 24x24 | #87CFE7 | Expanded contact row chevron |
| a-contact-rmx.svg | 20x20 | #87CFE7 | RMX glyph next to contact name |
| a-contact-info-outlined.svg | 20x20 | #CED0D4 | Info icon next to contact name |
| a-contact-mail-blue.svg | 18x18 | #87CFE7 | Email row |
| a-contact-phone-blue.svg | 18x18 | #87CFE7 | Phone row |
| a-contact-company-icon.svg | 16x16 | #C47000 | Company "Per Unit" row |
| a-card-divider-line.svg | 344x1 | stroke #5F6475 | Card dividers (or use a CSS border-top) |
| a-tickets-arrow-drop-down-blue.svg | 20x20 | #87CFE7 | "See 5 tickets" trailing icon |

Byte-identical duplicates across screens (drag, minimize, open-in-new, close, expand) were consolidated into the single files above.
