# T-04 · My unit

> Source: UIUX Part C "T-03 · My reports · T-04 · My unit · T-05 · My receipts" (p.17); SCOPE §8 ("My unit and contact details"), §12 (CX-03, CX-05). Build phase 6.

## Meta

| | |
|---|---|
| Route | **Not specified in source** (OPEN-18) |
| Access | Tenant link holder; no sign-in |
| Purpose | The tenant's unit, their agreement dates, and a way to reach the landlord without saving his number. |
| Arrives from | **Not specified** (OPEN-18) |
| Leads to | Dialler; WhatsApp |

## Components

| ID | Type | Content · what happens |
|---|---|---|
| T04-SEC-UNIT | Info block | Unit, property, landlord's name. Agreement start and end dates. **No rent figure.** |
| T04-BTN-CALL | Primary button | Calls the landlord (CX-05) |
| T04-BTN-MESSAGE | Secondary button | Opens WhatsApp to the landlord with a **blank** message (CX-03) |

## Design note (from source)

> T-04 shows agreement dates but not rent. The tenant knows their own rent; the app does not need to state it, and **any screen that displays a money figure is one refactor away from displaying the wrong one.**

## Rules

- No rent, deposit or any money figure is rendered **or present in the data** behind this page (GR-2, E4-04).
- Dates as DD MMM YYYY.
- Buttons 48px tall.

## Open items

> OPEN: [OPEN-18] No route and no entry point: no tenant screen links to T-04.

> OPEN: [OPEN-11] Call and WhatsApp need the landlord's phone number, which no screen collects.

> OPEN: [OPEN-03] Agreement dates and the landlord's contact are visible to anyone holding the link (e.g. from a building notice-board QR).

## Related

T-01, T-05, P-03.
