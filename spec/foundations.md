# RentRoll — Foundations (design system)

> Source: **[UIUX]** "How to read this document" and Part A (A1 Design tokens, A2 Component library, A3 Global navigation, A4 Responsive rules), p.2–4.
> Section numbers A1–A4 are kept from the source. A0 (identifiers) is added by this spec.

---

## A0 · Identifier scheme

Every screen, component and interaction has a stable ID. Use these IDs in tickets, commit messages, PR descriptions, code comments and QA notes, so a bug can be traced to a line in the spec. *(UIUX p.2)*

### A0.1 Screen and component IDs

| Pattern | Example | Meaning |
|---|---|---|
| `L-nn` | L-03 | Landlord screen, requires sign-in |
| `T-nn` | T-01 | Tenant screen, public link, no sign-in |
| `S-nn` | S-02 | Shared component used on several screens |
| `P-nn` | P-01 | Print view |
| `Lnn-TYPE-NAME` | L04-BTN-REMIND | A specific element on a specific screen (same pattern for `Tnn-`, `Snn-`) |

### A0.2 Element type codes

Defined in the source legend:

| Code | Element |
|---|---|
| BTN | button |
| LNK | link |
| FLD | input field |
| SEL | dropdown (also used for the L-04 month stepper) |
| CHK | checkbox |
| TAB | tab |
| ROW | table or list row |
| CRD | card |
| MOD | modal |
| TST | toast |
| CHP | chip or badge |

Used in the source but **not** in its legend (adopted here as valid codes):

| Code | Element | First seen |
|---|---|---|
| SEG | segmented choice | L04-SEG-FILTER |
| TBL | data / editable table | L02-TBL-UNITS |
| STRIP | summary strip | L04-STRIP-SUMMARY |
| HDR | screen / panel / modal header | L05-HDR |
| SEC | section / content / key-value block | L05-SEC-AMOUNT |
| TML | timeline | L05-TML-REMINDERS |
| GAL | photo strip / gallery | L07-GAL-PHOTOS |
| COL | board column | L06-COL-NEW |
| LST | list | L03-LST-ATTENTION |
| CHT | chart | L03-CHT-INCOME |
| UPL | uploader | T01-UPL-PHOTO |
| IMG | image | S02-IMG-QR |
| ZONE, THUMB, ERR | uploader drop zone, thumbnail, inline error | S-04 |

Added by this spec for elements the source describes but does not name:

| Code | Element |
|---|---|
| FRM | inline form or form state |
| BNR | banner |

### A0.3 IDs added by this spec

Where the source describes an element without giving it an ID, this spec assigns one and marks it **`[+]`** (for example `L07-CHK-NOCOST [+]`). IDs without the mark are verbatim from the source. Never rename a source ID.

Other ID families used across `spec/`:

| Family | Meaning | Defined in |
|---|---|---|
| `GR-n` | Global rules that apply to every screen | [cross-cutting.md](cross-cutting.md) |
| `PR-n` | Product principles | [product.md §2](product.md#2-vision-and-design-principles-scope-3) |
| `MOD-n` | Product modules | [product.md §4](product.md#4-modules-scope-6) |
| `J-n`, `DF-n`, `RENT-n`, `REQ-n`, `M-n` | Journeys, data flows, lifecycle rules, metrics | [product.md](product.md) |
| `CX-nn` | The twelve connections | [cross-cutting.md](cross-cutting.md#connections) |
| `AI-n` | Assistant touch-points | [cross-cutting.md](cross-cutting.md#assistant) |
| `E1-nn`, `E2-nn`, `E4-nn` | System messages, empty states, permission tests | [cross-cutting.md](cross-cutting.md) |
| `OPEN-nn` | Unresolved contradictions or gaps | [index.md](index.md#open-items) |

### A0.4 What each screen spec contains *(UIUX p.2)*

- **Meta** — route, who can reach it, why it exists, where users arrive from and leave to
- **Layout** — the regions of the screen, top to bottom
- **Components** — every element with its ID and content
- **Interactions** — what happens on every click, in order
- **States** — loading, empty, error, and any state-specific display
- **Rules** — validation, permissions, edge cases

---

## A1 · Design tokens

### A1.1 Colour

| Token | Value | Used for |
|---|---|---|
| `ink` | `#14202B` | Headings, primary text, numbers on cards |
| `body` | `#3C4A57` | Body copy, table cells |
| `muted` | `#7C8B99` | Labels, helper text, placeholders, timestamps |
| `line` | `#E2E8ED` | Borders, dividers, table rules |
| `canvas` | `#F6F8FA` | Page background |
| `surface` | `#FFFFFF` | Cards, panels, table background |
| `primary` | `#1B3A5C` | Primary buttons, active nav, links |
| `primary-soft` | `#DCE7F0` | Selected rows, active tab background |
| `success` | `#1E7A4D` | Paid status, confirmations |
| `warning` | `#B4761A` | Due soon, expiring, 1–9 days late |
| `danger` | `#B3352C` | Overdue 10+ days, urgent requests, destructive actions |
| `neutral` | `#8A98A5` | Vacant, closed, archived |

**Rule:** status colour is never the only signal. Every status chip carries a text label as well as a colour, so the board is readable in print, in greyscale, and by anyone with colour vision deficiency.

> OPEN: [OPEN-24] Several A1 token pairs fail the E5 contrast floor ("text contrast at least 4.5:1; status chips are tested against their tinted backgrounds specifically"). Computed WCAG ratios:
>
> | Pair | Ratio | Passes 4.5:1? |
> |---|---|---|
> | `muted` text on `surface` / `canvas` | 3.49 / 3.28 | No |
> | `warning` chip text on 12% tint (over surface / canvas) | 3.31 / 3.11 | No |
> | `neutral` chip text on 12% tint | 2.65 / 2.49 | No |
> | `success` chip text on 12% tint | 4.52 / 4.26 | Only on surface |
> | `danger` chip text on 12% tint | 5.05 / 4.76 | Yes |
> | `ink`, `body`, `primary` on surface/canvas; white on `primary` | ≥ 8.5 | Yes |
>
> Either the token values or the E5 threshold must change. This spec changes neither.

### A1.2 Type scale

| Token | Size / weight | Used for |
|---|---|---|
| `display` | 28px / 600 | Dashboard headline numbers only |
| `h1` | 20px / 600 | Page title |
| `h2` | 16px / 600 | Card and panel titles |
| `body` | 14px / 400 | Default text, table cells, form values |
| `small` | 13px / 400 | Helper text, secondary detail |
| `label` | 11px / 600, uppercase, 0.6px tracking | Field labels, column headers, stat captions |

- One typeface throughout.
- Numbers in tables and money columns use **tabular figures** so digits align vertically.

> OPEN: [OPEN-40] The typeface itself is not named.

### A1.3 Spacing, radius, elevation

| Token | Value | Rule / used for |
|---|---|---|
| `space-1 … space-6` | 4, 8, 12, 16, 24, 32px | Nothing outside this scale. Card padding is 16px on mobile, 24px on desktop. |
| `radius-sm` | 6px | Buttons, inputs, chips |
| `radius-md` | 10px | Cards, panels, modals |
| `shadow-1` | `0 1px 2px rgba(20,32,43,.06)` | Cards at rest |
| `shadow-2` | `0 8px 24px rgba(20,32,43,.12)` | Modals, drawers, dropdown menus |

> OPEN: [OPEN-25] `radius-sm` (6px) is assigned to chips, but the Status chip is defined as a "Rounded pill".

---

## A2 · Component library

Build these once. Every screen refers to them by name.

### A2.1 Buttons

| Variant | Appearance | Use for | Notes |
|---|---|---|---|
| Primary | Solid `primary`, white text | The one main action on a screen | Maximum one per screen region |
| Secondary | White, `primary` border and text | Supporting actions | Any number |
| Quiet | No border, `body` text, hover fill | Row-level actions, cancel | Used inside tables |
| Danger | White, `danger` border and text | Delete, remove, end tenancy | Always behind a confirm dialog |
| Icon | 32×32, icon only | Call, copy, share, print | Must carry a tooltip and an accessible label |

Button rules:
- Heights: **40px** default; **32px** compact in table rows; **48px** on tenant screens (touch targets).
- Disabled buttons show a tooltip explaining why.
- A button that triggers a network call shows an inline spinner and becomes non-interactive until it resolves. Never a full-page block.

### A2.2 Form fields

| Component | Behaviour |
|---|---|
| Text field | Label above, helper text below; an error replaces the helper text in `danger` colour. **Validates on blur, not on keystroke.** |
| Money field | Prefixed **₹**, digits only, thousands separators shown as the user types, **no decimals**. |
| Phone field | Prefixed **+91**, accepts 10 digits, strips spaces and dashes on save. |
| Date field | Native date picker. Displays as **DD MMM YYYY** everywhere in the product. |
| Dropdown | Native select on mobile. Always has a placeholder that is not a valid choice. |
| Segmented choice | 2–4 options shown as adjacent buttons. Used for urgency and status filters. |
| Photo uploader | See [S-04](screens/shared/S-04-photo-uploader.md). |
| Text area | Auto-grows to 8 lines, then scrolls. Character counter appears past 400 characters. |

> OPEN: [OPEN-43] The thousands-separator convention is not stated: Indian grouping (1,00,000) or international (100,000)? Neither is the compact display used in wireframes and copy ("2.1L", "36k", "₹2.1 lakh"), the "amount in words" style on P-01, the timezone used for the 1st-of-month job and all date maths, or the UI language(s).
### A2.3 Display components

| Component | Definition |
|---|---|
| Stat card | Uppercase label, display-size number, optional comparison line. Clickable when it has a destination; the **whole card** is the target, not just the number. |
| Status chip | Rounded pill, coloured background at 12% opacity, text in the full colour. Always includes a word. |
| Data table | Sticky header, sortable columns marked with an arrow, row hover fill, 48px rows. Row click opens the detail panel; buttons inside the row stop the click from propagating. |
| Detail panel | Slides in from the right, 480px wide on desktop, full screen on mobile. Closes on Escape, on backdrop click, and on the close button. Warns before closing if a field has unsaved edits. |
| Timeline | Vertical list of events, newest first, each with an icon, a line of text and a timestamp. Used for request history and reminder history. |
| Empty state | One line explaining what would appear here, and the button that creates the first one. Never just "No data". |
| Toast | Bottom-centre, 4 seconds, one line, optional Undo. Never used for errors that need a decision. |
| Confirm dialog | Title as a question, one line of consequence, cancel plus a labelled action button. The action button says what it does ("Delete unit", never "OK"). |

Additional shared building blocks named in screen specs, with no separate definition in the source: key-value block, contact block (name, phone with call / message / copy icon buttons, optional email with mail button), summary strip, month stepper, editable table, inline field, inline form, board column and card, file list, photo strip, banner, calculation block, chip row, bar chart. Build them with the A1 tokens and the A2 rules above.

> OPEN: [OPEN-26] The detail panel "closes on backdrop click", but A4 says that over 1024px it "opens alongside rather than over content", so there is no backdrop on desktop.

---

## A3 · Global navigation

| Region | Contents and behaviour |
|---|---|
| Sidebar (desktop) | Fixed **220px**. Logo, then: **Dashboard, Rent, Maintenance, Units, Tenants, Agreements, Deposits, Documents**. **Settings** and **account** sit at the bottom. Active item has `primary-soft` background and a 3px left bar. |
| Bottom bar (mobile) | Five items only: **Dashboard, Rent, Maintenance, Units, More**. "More" opens a sheet with the rest (Tenants, Agreements, Deposits, Documents, Settings, account). |
| Page header | Title on the left, primary action on the right, filters on the row beneath. Persists while the table scrolls. |
| Global search | **Not in version one.** Filters on each board cover the need. |

Sidebar → screen mapping:

| Nav item | Screen | Route |
|---|---|---|
| Dashboard | L-03 | `/` |
| Rent | L-04 | `/rent` |
| Maintenance | L-06 | `/maintenance` |
| Units | L-08 | `/units` |
| Tenants | L-10 | `/tenants` |
| Agreements | L-12 | `/agreements` |
| Deposits | L-13 | `/deposits` |
| Documents | L-14 | *not specified* (OPEN-39) |
| Settings | L-15 | *not specified* (OPEN-39) |
| account | *no screen defined* (OPEN-11) | — |

**Tenant screens have no navigation at all**: no sidebar, no menu, no links to anything except the tenant's own pages. *(See OPEN-18: the source says "three pages".)*

---

## A4 · Responsive rules

| Breakpoint | Behaviour |
|---|---|
| Under 640px | Data tables become **stacked cards**: one card per row, key fields only, tap to open the detail panel full-screen. Bottom navigation bar. Stat cards go **two per row**. |
| 640–1024px | Sidebar collapses to icons. Tables keep **three columns plus actions**. |
| Over 1024px | Full sidebar, full tables, detail panel opens **alongside** rather than over content. |

- Tenant screens are designed **mobile-first** and are never tested on desktop only.
- Minimum touch target on tenant screens is **48×48px**.

> OPEN: [OPEN-40] For each data table the source does not say which three columns survive at 640–1024px, or which "key fields" appear on mobile cards.
