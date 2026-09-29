# L-11 · Tenant detail

> Source: UIUX Part B "L-10 · Tenant list · L-11 · Tenant detail" (p.13); SCOPE §6 (MOD-6), §12 (CX-03, CX-04, CX-05, CX-07, CX-08). Build phase 2.

## Meta

| | |
|---|---|
| Route | `/tenants/:tenantId` |
| Access | Signed in; tenant must belong to the signed-in landlord (else Not found, E4-05) |
| Purpose | Contact, agreement and payment history for a person, past or present. |
| Arrives from | L10-TBL-TENANTS row click |
| Leads to | L-13 (End tenancy); email app (Send agreement); dialler; messaging |

## Components and interactions

| ID | Type | Content · what happens |
|---|---|---|
| L11-SEC-CONTACT | Contact block | Phone with **call**, **message** and **copy** buttons; email with a **mail** button if present |
| L11-SEC-AGREEMENT | Key-value block | Start, end, rent, deposit paid, notice status, with a **countdown when within 90 days** |
| L11-SEC-PAYMENTS | Table | Every rent entry for this tenant, with a **paid-on-time percentage** at the top |
| L11-SEC-DOCS | File list | Agreement, ID proof, anything else uploaded. Each with **download** and **share**. |
| L11-BTN-ENDTENANCY | Danger button | "End tenancy" → **confirm dialog** → routes to **L-13 with this tenant selected** |
| L11-BTN-SENDAGREEMENT | Quiet button | Opens the email composer with the agreement referenced. Helper text: **"Attach the file after your email app opens."** |

## Rules

- Confirm dialog for End tenancy follows A2: title as a question, one line of consequence, a labelled action button (e.g. "End tenancy", never "OK").
- End tenancy does **not** itself close the tenancy. Closing happens at L13-BTN-CLOSE ("Mark settled").
- Call follows CX-05 (dial, then offer to log).
- Share uses S03-BTN-SHARE behaviour.

## Open items

> OPEN: [OPEN-45] L11-SEC-PAYMENTS needs rent entries attributed to this tenancy; the ERD links rent entries only to the unit. "Paid on time" depends on the undefined due date (OPEN-05).

> OPEN: [OPEN-31] "Opens the email composer" is ambiguous: S-01, or a direct `mailto:` hand-off? The same question applies to the "message" button in L11-SEC-CONTACT.

> OPEN: [OPEN-37] L11-SEC-DOCS lists uploaded files, but no upload control is defined for agreements or ID proofs.

> OPEN: [OPEN-12] Notice status is displayed but not editable anywhere.

> OPEN: [OPEN-53] Whether calls placed from L11-SEC-CONTACT are logged, and where.

> OPEN: [OPEN-33] SCOPE MOD-6 lists "share the unit link" as a tenant-record action; no such control is defined here (it exists on L-09).

> OPEN: [OPEN-46] Build phase 2 (L-11) routes End tenancy to L-13, which is phase 7.

## Related

L-10, L-09, L-12, L-13, S-01, S-03.
