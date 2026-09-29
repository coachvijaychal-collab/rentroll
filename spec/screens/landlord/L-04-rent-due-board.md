# L-04 · Rent due board

> Source: UIUX Part B L-04 (p.9); UIUX E1, E2; SCOPE §6 (MOD-2), §7 Wireframe B, §10. Build phase 4 (done when "rows generated monthly; filters, statuses and mark-paid all work").

## Meta

| | |
|---|---|
| Route | `/rent` · with state in the query string, e.g. `/rent?month=2026-02&status=overdue` |
| Access | Signed in |
| Purpose | See who has paid, and act on who has not, **without leaving the screen**. |
| Arrives from | Sidebar "Rent"; L03-CRD-DUES (Overdue filter); L03-CRD-COLLECTED (current month) |
| Leads to | L-05 detail panel · S-01 composer · S-02 payment sheet · P-01 receipt |

## Layout

Page header with month selector → summary strip → filter row → data table. On mobile the table becomes stacked cards (A4).

## Components

| ID | Type | Content and behaviour |
|---|---|---|
| L04-SEL-MONTH | Month stepper | Back arrow · "February 2026" · forward arrow. Forward is **disabled beyond the current month**. |
| L04-STRIP-SUMMARY | Summary strip | Three figures: **expected, collected, outstanding**. Updates with the filter. |
| L04-SEG-FILTER | Segmented choice | **All · Pending · Overdue · Paid**. Default **All**. Reflected in the URL. |
| L04-SEL-PROPERTY | Dropdown | Property filter. **Hidden when the landlord has one property.** |
| L04-TBL-RENT | Data table | Columns: **Unit · Tenant · Rent · Due date · Status · Actions** |
| L04-ROW | Table row | One rent entry (one unit, one month) |
| L04-CHP-STATUS | Status chip | **Paid** (success) · **Due** (neutral) · **n days late** (warning at 1–9, danger at 10+). Part payment shows "Part paid — ₹4,000 pending". Mid-month move-in rows show a small "pro-rata" note. |
| L04-BTN-REMIND | Quiet button | "Remind", shown **only when unpaid** |
| L04-BTN-MARKPAID | Quiet button | "Mark paid", shown **only when unpaid** |
| L04-FRM-MARKPAID [+] | Inline row form | Amount received · date received · payment reference (see interactions) |
| L04-BTN-RECEIPT | Icon button | Print icon, shown **only when paid** |
| L04-BTN-EXPORT | Secondary button | "Export" in the page header |
| L04-BNR-NOROWS [+] | Banner with action | "This month's rent rows have not been created" + button to create them now (E1-11) |

## Interactions

| Trigger | Result |
|---|---|
| L04-ROW (click) | Opens the **L-05** detail panel for that rent entry |
| L04-BTN-REMIND | Opens **S-01** pre-loaded with the escalation level matching days overdue. Stops row-click propagation. |
| L04-BTN-MARKPAID | Opens a small inline form in the row (L04-FRM-MARKPAID [+]): **amount received** (money field, pre-filled with rent due), **date received** (defaults to today), **payment reference** (optional). Confirm → row flips to Paid → receipt number is generated → toast **"Payment recorded. Receipt RR-0847 created."** with an **Undo** that reverses it for **10 seconds**. |
| L04-BTN-RECEIPT | Opens **P-01** in a new tab |
| L04-BTN-EXPORT | Downloads a CSV of the **current filtered view**. File named `rent-2026-02.csv`. Toast confirms ("Downloaded rent-2026-02.csv", E1-04). |
| L04-SEG-FILTER | Filters the table **without a page reload** and updates the URL so the view can be shared or bookmarked |
| L04-SEL-MONTH arrows | Changes the month shown (URL `month=YYYY-MM`) |
| L04-BNR-NOROWS [+] action | Creates the current month's rent rows now |

## States

| State | Display |
|---|---|
| Loading | Skeleton matching the table (E3) |
| No units | **"Add a unit and this month's rent will appear here."** Action: **Add unit** (E2-01) |
| All paid | **"Everything is paid for February. Nice."** No action (E2-02) |
| Rows not created | Banner L04-BNR-NOROWS [+] (E1-11) |
| Row action in progress | Spinner inside the button only (E3) |

## Rules and edge cases

- **Part payment.** If the amount received is less than the rent due, the row shows **"Part paid — ₹4,000 pending"** and remains in the **Pending** filter. A receipt is issued for the amount actually received.
- **Vacant units** do not appear at all for months in which they had no tenant.
- **Mid-month move-in.** The first month's row is created with the **pro-rata** amount and shows a small "pro-rata" note. The landlord can edit the amount before marking paid (L05-BTN-EDIT).
- **Rent rows are created on the 1st.** If that job did not run, show the L04-BNR-NOROWS [+] banner with a button to create them now.
- **Marking paid twice is impossible.** The button is replaced the moment the state changes.
- Rent changes from a renewal take effect from the new start date. Rows already generated are not altered (L-12).
- Payment is never marked automatically (no gateway in v1; S-02 never claims payment).
- Wireframe B (SCOPE §7) example rows: 1A R. Sharma 16,000 Paid · 1B A. Iyer 16,000 Paid · 2A M. Desai 18,000 5d late · 4C S. Khan 18,000 18d late.

## Open items

> OPEN: [OPEN-05] The due date, and whether ladder days count from the 1st or from the due date, are undefined. The tone S-01 pre-selects when "Remind" is pressed on a row that is **Due** (not late) is also undefined.

> OPEN: [OPEN-07] It is undefined how the remainder of a part payment is recorded (a second Mark paid? a second receipt?), given "marking paid twice is impossible" and the single paid-amount fields in the ERD.

> OPEN: [OPEN-28] **Pending** vs **Overdue** filter membership is not defined. Presumably Pending = unpaid and not yet late, Overdue = past due, but "part paid remains in Pending" leaves open where a part-paid, past-due row belongs.

> OPEN: [OPEN-08] The 10-second Undo conflicts with the 4-second toast (A2). It is undefined what happens to receipt number RR-0847 on Undo.

> OPEN: [OPEN-27] The pro-rata formula is unspecified.

> OPEN: [OPEN-22] SCOPE describes this module as "a grid of month against unit", and Wireframe B shows the drafted reminder and the Send / Pay link / Mark paid actions inline below the table. UIUX uses a single-month table plus the S-01 modal and the S-02 sheet.

> OPEN: [OPEN-29] The chip thresholds (1–9 / 10+) are fixed while the ladder days are editable (L15-TBL-LADDER).

> OPEN: [OPEN-46] Build phase 4 (L-04) needs S-01 for "Remind", but S-01 is phase 5.

## Related

L-05, S-01, S-02, P-01, L-15 (ladder), [product §10.1](../../product.md#101-rent-lifecycle-scope-10-diagram-3-uiux-l-04-l-05-l-15-s-01).
