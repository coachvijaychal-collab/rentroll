# L-15 · Settings

> Source: UIUX Part B "L-14 · Documents and exports · L-15 · Settings" (p.15); UIUX L-02, S-02, A3. Build phase 7.

## Meta

| | |
|---|---|
| Route | **Not specified in source** (OPEN-39) |
| Access | Signed in |
| Purpose | The landlord's payment, branding, escalation and reminder defaults. |
| Arrives from | Sidebar bottom "Settings"; S-02 "no UPI ID" prompt; any payment feature's "add UPI ID" prompt |
| Leads to | — |

## Components

| ID | Type | Content and behaviour |
|---|---|---|
| L15-FLD-UPI | Text field | UPI ID used in **every payment link and QR**. Shape-validated `name@handle`, not verified (L-02). |
| L15-FLD-RECEIPTNAME | Text field | Name printed on **receipts and statements** |
| L15-UPL-LOGO | Photo uploader | **Optional** logo for print views (P-01, P-02; also "landlord's name or logo" on T01-HDR) |
| L15-FLD-ESCDEFAULT | Text field | Default rent escalation percentage (L12-FLD-ESCALATION default) |
| L15-TBL-LADDER | Editable table | The reminder ladder: **day 3 gentle, day 10 direct, day 20 formal**. **Days are editable; the three levels are fixed.** |
| L15-FLD-CAEMAIL | Text field | Accountant's email, used by L14-BTN-EMAILCA |

## Rules

- L15-FLD-UPI and L15-FLD-RECEIPTNAME are the same values captured by L02-FLD-UPI and L02-FLD-BIZNAME.
- Ladder levels cannot be added, removed or renamed; only their days change. The ladder drives the S-01 tone pre-selection (RENT-3, RENT-5).
- Saving follows the common rule: failed save → "Could not save. Your changes are still here — try again." inline above the form (E1-07).

## Open items

> OPEN: [OPEN-39] The route is not specified.

> OPEN: [OPEN-11] The sidebar has "Settings **and account**", but no account fields (name, phone, email, password change, sign out) are defined. The landlord's phone, needed by T-01, T-04 and P-03, has no input anywhere.

> OPEN: [OPEN-05] Ladder days are relative to what (day of month or days past due)? Should the ladder days be validated as ascending?

> OPEN: [OPEN-29] Whether chip colour thresholds (1–9 / 10+) follow the edited ladder days.

> OPEN: [OPEN-43] The escalation % field type (decimals allowed?) is not specified.

## Related

L-02, L-12, L-14, S-01, S-02, P-01, P-02.
