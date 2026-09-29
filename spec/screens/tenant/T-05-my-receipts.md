# T-05 · My receipts

> Source: UIUX Part C "T-03 · My reports · T-04 · My unit · T-05 · My receipts" (p.17); UIUX E2; SCOPE §2, §8 ("My receipts"), §16. Build phase 6.

## Meta

| | |
|---|---|
| Route | **Not specified in source** (OPEN-18) |
| Access | Tenant link holder; no sign-in |
| Purpose | Proof of rent paid, on hand when the tenant needs it ("has receipts on hand for their own proof of rent", SCOPE §17). |
| Arrives from | **Not specified** (OPEN-18) |
| Leads to | P-01 (per receipt) |

## Components

| ID | Type | Content · what happens |
|---|---|---|
| T05-LST-RECEIPTS | List | **Month · amount · receipt number · a print button each** |
| T05-BTN-PRINT | Icon button | Opens **P-01** for that receipt |

## States

| State | Display |
|---|---|
| Loading | Skeleton list (E3) |
| Empty | **"Receipts appear here once your landlord records a payment."** No action (E2-08) |

## Design note (from source)

> Receipts on T-05 **do** show amounts, because those are the tenant's own payments and the receipt is the point.

## Rules

- Only receipts for payments the landlord has recorded (Mark paid). Nothing appears from a payment link alone (S-02 never claims payment).
- The icon button carries a tooltip and accessible label (A2, E5), with a 48×48 touch target.

## Open items

> OPEN: [OPEN-02] **Money on a tenant screen.** The amounts on this screen, and on P-01 opened from it, contradict GR-2 as written ("no tenant-facing screen ever … displays rent amounts"), SCOPE §4 ("no money"), SCOPE §8 ("no path to any money screen") and E4-04 ("contains no rent amount"). UIUX states this exception explicitly, but the other rules were not amended to match.

> OPEN: [OPEN-45] Scope is undefined: receipts for the **current tenancy only** (like T-03), or all receipts for the unit? Rent entries are not linked to a tenancy in the ERD.

> OPEN: [OPEN-39] P-01 opened from a tenant page needs a tenant-scoped (token-authorised) route. P-01's route is unspecified.

> OPEN: [OPEN-18] No route and no entry point: no tenant screen links to T-05.

## Related

P-01, T-04, L-04 (Mark paid).
