# P-03 · Door QR card

> Source: UIUX Part D "Print views" (p.19); UIUX L-08, L-09, E2-03; SCOPE §5 (J1), §12 (CX-11). Build phase 7 (done when it prints "four to a page, scannable from print").

## Meta

| | |
|---|---|
| Type | Print view: separate page, new tab, print dialog on load |
| Route | **Not specified in source** (OPEN-39) |
| Opened from | L08-BTN-PRINTQR (one card per selected unit); L09-BTN-QR modal print option; L-06 empty-state action "Print door QR codes" |
| Purpose | A printable code that opens that unit's reporting page (T-01). |

## Contents (per card)

1. Unit number
2. Property name
3. The QR (encodes the unit's T-01 link, `/u/:unitToken`)
4. One line: **"Scan to report a problem"**
5. Landlord's phone, as a fallback

Sized **four to an A4 page**.

## Rules

- Common print rules: no navigation, no buttons, white background, new tab, print dialog on load; no print-style hiding of the app UI.
- Must be **scannable from print** (Part F).
- Intended placements (SCOPE CX-11): a sticker inside the flat door · the welcome sheet handed over at move-in · a notice board in the building.

## Open items

> OPEN: [OPEN-01] If the token must change when a tenancy ends (T-01, E4-02), every printed door sticker becomes invalid at each tenancy change. The source does not say whether stickers are meant to be reprinted.

> OPEN: [OPEN-03] A QR on a building notice board, or anywhere visible to others, gives anyone who scans it the current tenant's pre-filled name and phone (T-01), agreement dates (T-04), receipts (T-05) and reports (T-03).

> OPEN: [OPEN-11] The landlord's phone is required on the card, but no screen collects it.

> OPEN: [OPEN-39] No route.

## Related

L-08, L-09, L-06, T-01.
