# L-14 · Documents and exports

> Source: UIUX Part B "L-14 · Documents and exports · L-15 · Settings" (p.15); SCOPE §2 (March panic), §12 (CX-04, CX-08, CX-12), §17. Build phase 7 (with L-15; done when "all four CSVs open correctly in Excel with the rupee symbol intact").

## Meta

| | |
|---|---|
| Route | **Not specified in source** (OPEN-39) |
| Access | Signed in |
| Purpose | Every uploaded file in one place, and the year-end exports for the accountant ("one export, one file, done in March in a minute", SCOPE §17). |
| Arrives from | Sidebar "Documents" (mobile: "More" sheet) |
| Leads to | File download / share sheet; email app |

## Components and interactions

| ID | Type | Content · what happens |
|---|---|---|
| L14-TBL-DOCS | Data table | Every uploaded file: **type, what it belongs to, uploaded on**. Actions: **Download, share, delete**. |
| L14-BTN-EXPORT-* | Buttons | Four exports, **each with a date range picker**: |
| · L14-BTN-EXPORT-RENT [+] | | Rent ledger |
| · L14-BTN-EXPORT-MAINT [+] | | Maintenance spend (per unit) |
| · L14-BTN-EXPORT-TENANTS [+] | | Tenant list |
| · L14-BTN-EXPORT-DEPOSITS [+] | | Deposit register |
| L14-BTN-EMAILCA | Secondary button | Opens the email composer addressed to the **saved accountant address** (L15-FLD-CAEMAIL), subject **"Rental records — FY 2025-26"**, body listing what is attached. Helper text reminds the landlord to **attach the downloaded file**. |

## Rules

- Document types: agreement, ID proof, photo, receipt, statement (ERD). Settled statements from L-13 are filed here.
- Delete is destructive: Danger button behaviour, behind a confirm dialog naming the action (A2).
- Exports are **CSV** and must open correctly in Excel with the **₹ symbol intact** (Part F).
- Download success shows a toast, e.g. "Downloaded rent-2026-02.csv" (E1-04).
- The FY label follows the Indian financial year (April–March), e.g. "FY 2025-26".
- Share uses S03-BTN-SHARE behaviour.
- Documents of another landlord → Not found (E4-07).

## States

| State | Display |
|---|---|
| Loading | Table skeleton (E3) |
| Empty | Not specified in E2 (OPEN-54) |

## Open items

> OPEN: [OPEN-39] The route is not specified.

> OPEN: [OPEN-31] "Opens the email composer": S-01 or a direct `mailto:` hand-off? It is also undefined what happens when no accountant email is saved.

> OPEN: [OPEN-37] L14-TBL-DOCS lists "every uploaded file", but this screen has no upload control.

> OPEN: [OPEN-43] The CSV column definitions for the four exports are not specified. The FY label's dependence on the date-range picker is not specified.

## Related

L-15, L-13, L-11, L-04 (per-view export), [cross-cutting CX-12](../../cross-cutting.md#connections).
