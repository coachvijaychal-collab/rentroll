# L-13 · Deposit and settlement

> Source: UIUX Part B L-13 (p.14); UIUX E2; SCOPE §5 (J6), §6 (MOD-8), §11 (AI-3). Build phase 7 (with P-02; done when "deductions pull from repair history with photos attached").

## Meta

| | |
|---|---|
| Route | `/deposits` (list) · `/deposits/:tenantId` (settlement page) |
| Access | Signed in; tenant must belong to the signed-in landlord (else Not found) |
| Purpose | Turn a potential argument into a document. **This screen exists to be printed.** |
| Arrives from | Sidebar "Deposits"; L11-BTN-ENDTENANCY (with this tenant selected) |
| Leads to | P-02 (print), S-01 (send), Documents (statement filed) |

## Components

### Deposits list (`/deposits`)

| ID | Type | Content and behaviour |
|---|---|---|
| L13-TBL-HELD | Data table | Every deposit currently held: **unit, tenant, amount, since when**. **Total at the top.** Row → settlement page for that tenant. |

### Settlement page (`/deposits/:tenantId`)

| ID | Type | Content and behaviour |
|---|---|---|
| L13-SEC-DEPOSIT | Key-value block | Amount held, date received, agreement reference |
| L13-TBL-DEDUCTIONS | Editable table | Each row: **description · reason · amount · photo**. Add and remove rows. |
| L13-BTN-FROMREQUESTS | Secondary button | "Pull from repair history". Lists **this tenancy's** requests with costs and lets the landlord **tick the ones to deduct**, carrying their **photos** across |
| L13-SEC-BALANCE | Calculation block | **Deposit held − total deductions = refund due.** Large, unmissable. |
| L13-BTN-GENERATE | Primary button | "Prepare settlement statement" (assistant-written statement, AI-3) |
| L13-BTN-PRINT | Secondary button | Opens **P-02** |
| L13-BTN-SEND | Secondary button | Opens **S-01** with the settlement summary |
| L13-BTN-CLOSE | Primary button | "Mark settled" → **confirm** → tenancy closes, unit becomes vacant, statement is filed under documents |

## Interactions

| Trigger | Result |
|---|---|
| L13-BTN-FROMREQUESTS | Shows this tenancy's requests with costs; ticked ones become deduction rows with their photos |
| L13-BTN-GENERATE | Assistant turns the deposit amount, deductions and reasons into a written statement (AI-3; template fallback per S-01 rules) |
| L13-BTN-PRINT | P-02 in a new tab, print dialog on load |
| L13-BTN-SEND | S-01 with the settlement summary (GR-1) |
| L13-BTN-CLOSE | Confirm dialog → tenancy closed; unit → Vacant; statement filed in Documents (type "statement"); former tenant's link stops working (T-01, E4-02) |

## States

| State | Display |
|---|---|
| Loading | Skeleton (E3) |
| Empty (list) | **"Deposits appear here once you add tenants."** Action: **Add tenant** (E2-06) |
| Tenant owes | If deductions exceed the deposit, the balance shows as an **amount owed by the tenant**, in **danger** colour, and the statement wording changes accordingly |
| Settled | Statement is **read-only** |

## Rules

- A deduction **without a written reason cannot be saved**.
- A deduction **without a photo shows a warning but is allowed**, since not everything is photographable.
- If deductions exceed the deposit → amount owed by tenant, danger colour, statement wording changes.
- Once marked settled, the statement becomes **read-only**. Corrections require a **new statement that references the first**.
- "Evidence, always": photos at move-in, on every repair, a written reason on every deduction (PR-5).

## Open items

> OPEN: [OPEN-42] It is undefined how a correction statement is created once the tenancy is closed; whether the refund paid out (or the amount owed by the tenant) is recorded; what End tenancy does when no deposit is held; and where the assistant's written statement appears (on P-02, in the S-01 message, or both).

> OPEN: [OPEN-44] The deposit ledger, deductions and settlement statement are not entities in the ERD. The deposit's "date received" and "agreement reference" are not ERD attributes.

> OPEN: [OPEN-02] P-02 and the S-01 settlement message show deduction amounts and repair costs to the tenant. Is that consistent with GR-2 / PR-3 ("tenant's pages never show … repair costs")?

> Note: two Primary buttons (GENERATE, CLOSE) appear on the settlement page. A2 allows at most one per screen **region**, so they must sit in different regions.

## Related

L-11, L-14, P-02, S-01, L-07 (repair costs and photos).
