# L-10 · Tenant list

> Source: UIUX Part B "L-10 · Tenant list · L-11 · Tenant detail" (p.13); SCOPE §6 (MOD-6). Build phase 2 (with L-11; done when "a tenant can be attached to a unit with agreement dates").

## Meta

| | |
|---|---|
| Route | `/tenants` |
| Access | Signed in |
| Purpose | Contact, agreement and payment history for a person, **past or present**. |
| Arrives from | Sidebar "Tenants" (mobile: "More" sheet) |
| Leads to | L-11 |

## Components and interactions

| ID | Type | Content · what happens |
|---|---|---|
| L10-TBL-TENANTS | Data table | Columns: **Name · Unit · Phone · Agreement ends · Status**. Row click → **L-11**. |
| L10-SEG-FILTER | Segmented choice | **Current · On notice · Past** |

## States

| State | Display |
|---|---|
| Loading | Table skeleton (E3) |
| Empty | Not specified in E2 (OPEN-54). |

## Rules

- A "tenant" record is one tenancy (a person in a unit for an agreement period); past tenants stay listed under **Past** (SCOPE §4, §15).
- Dates display as DD MMM YYYY.

## Open items

> OPEN: [OPEN-12] How a tenant enters **On notice** is not defined (no control records a notice served or given).

> OPEN: [OPEN-54] The default L10-SEG-FILTER value and the empty-state copy are not specified.

> OPEN: [OPEN-10] There is no "Add tenant" action here; tenants are added only via L09-BTN-ADDTENANT, whose form is undefined.

## Related

L-11, L-09, L-12, L-13.
