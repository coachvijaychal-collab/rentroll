# T-03 · My reports

> Source: UIUX Part C "T-03 · My reports · T-04 · My unit · T-05 · My receipts" (p.17); UIUX E2; SCOPE §8 ("Track what I reported"), §9. Build phase 6 (with T-04, T-05; done when "verified against every test in E4").

## Meta

| | |
|---|---|
| Route | **Not specified in source** (OPEN-18) |
| Access | Tenant link holder; no sign-in |
| Purpose | Let the tenant see that their reports were heard and where each one stands ("to be heard, and to have proof"). |
| Arrives from | T01-LNK-MYREPORTS; T02-BTN-TRACK |
| Leads to | T-01 (empty-state action) |

## Components

| ID | Type | Content · what happens |
|---|---|---|
| T03-LST-REPORTS | List | Every request from **this unit's current tenancy**. Each shows: **number, category, date, status chip, and the landlord's latest update if any**. |
| T03-CHP-STATUS | Status chip | **Received · Assigned · In progress · Done**. Plain words, no internal jargon. |
| T03-TML-ITEM | Timeline | Expanding a report shows its history (**reported, assigned, updated, completed**) with **tenant-safe wording only** |

## States

| State | Display |
|---|---|
| Loading | Skeleton list (E3) |
| Empty | **"You have not reported anything yet."** Action: **Report a problem** (→ T-01) (E2-07) |
| Invalid / vacant / former-tenant token | E1-10 full screen (as T-01) |

## Rules

- Scope is the **current tenancy only**. Earlier tenants' requests for the same unit are never shown (GR-2 "other tenants").
- Status mapping from landlord statuses: New → **Received**, Assigned → Assigned, In progress → In progress, Done → Done.
- Tenant-safe: never the vendor's rate, the cost recorded, internal notes, or any other unit (L-07 rule; GR-2). History text is built from status and category only.
- A reopened request (L-06) shows as the same request with further history, not a new one.

## Open items

> OPEN: [OPEN-17] "The landlord's latest update" has no defined source. Is it the text of the S-01 message sent via L07-BTN-UPDATETENANT? That text is free-form and landlord-edited, so it could contain costs, which conflicts with "tenant-safe wording only". Or is it a separate tenant-visible field that no screen defines?

> OPEN: [OPEN-18] The route is not specified. There is no way back to T-01 other than the empty-state action.

## Related

T-01, T-02, L-06, L-07.
