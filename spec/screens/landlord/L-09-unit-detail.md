# L-09 · Unit detail

> Source: UIUX Part B L-09 (p.13); SCOPE §5 (J1, J2), §6 (MOD-5), §12 (CX-06, CX-07, CX-08, CX-11), §15. Build phase 2.

## Meta

| | |
|---|---|
| Route | `/units/:unitId`. **A full page, not a panel**, because it holds a lot. |
| Access | Signed in; unit must belong to the signed-in landlord (else Not found, E4-05) |
| Purpose | The unit's whole life: who lives there, what it earns, what it has cost, what it looked like at move-in. |
| Arrives from | L08-TBL-UNITS row click |
| Leads to | Tenant form (Add tenant); unit QR modal; Maps; share sheet |

## Layout

Header with unit identity and status → four tabs: **Overview · Rent history · Maintenance history · Photos & documents**.

## Components

| ID | Type | Content and behaviour |
|---|---|---|
| L09-HDR [+] | Header | Unit identity (unit number, property) and status chip (as L08-CHP-STATUS) |
| L09-TAB-OVERVIEW | Tab | Rent, deposit, current tenant card, the unit's **reporting link with copy and share buttons**, and **lifetime figures**: total rent collected, total maintenance spend, net |
| L09-TAB-RENT | Tab | Every month, every tenant, ever. Paid or not, and how much. |
| L09-TAB-MAINT | Tab | Every request against this unit, with cost. A repeated category shows a quiet note, e.g. **"Plumbing reported 4 times in 12 months."** |
| L09-TAB-PHOTOS | Tab | Move-in condition photos **grouped by tenancy**, plus repair photos, plus documents |
| L09-BTN-COPYLINK | Icon button | Copies the unit's tenant link to the clipboard (S03-BTN-COPY behaviour) |
| L09-BTN-SHARELINK | Icon button | Opens the device share sheet; on desktop falls back to copy (S03-BTN-SHARE behaviour) |
| L09-BTN-QR | Icon button | Shows the unit QR in a modal with a print option |
| L09-MOD-QR [+] | Modal | Unit QR + print option (→ P-03 for this unit) |
| L09-BTN-MAP | Icon button | Opens the property address in Maps in a new tab (CX-06) |
| L09-BTN-ADDTENANT | Primary button | **Visible only when vacant.** Opens the tenant form. |

## Design note (from source)

> The lifetime figures on the Overview tab are the quiet insight in this product. "This unit earned ₹2.1 lakh and cost ₹34,000 last year" is a fact most landlords have never seen for a single flat. **Give it space.**

## Rules

- History belongs to the unit: rent entries, requests and photos stay with the unit across tenancies (GR-4).
- Net = total rent collected − total maintenance spend.
- Icon buttons carry tooltips and accessible labels (A2, E5).

## Open items

> OPEN: [OPEN-34] The Overview specifies **lifetime** figures, but the design note quotes "**last year**". The period(s) to show are unresolved.

> OPEN: [OPEN-10] The fields of "the tenant form" (L09-BTN-ADDTENANT) are not specified anywhere. SCOPE J2 implies name, phone, agreement dates, deposit, and condition photos, plus a welcome message with the unit link (CX-03). The pro-rata first month (L-04) is presumably triggered by the move-in date.

> OPEN: [OPEN-37] L09-TAB-PHOTOS lists move-in condition photos and documents, but no upload control is defined there (or anywhere) for condition photos, agreements or ID proofs.

> OPEN: [OPEN-01] Whether the unit's reporting link shown here changes when the tenancy changes.

> OPEN: [OPEN-38] Whether tenant-liable repair costs count in "total maintenance spend".

## Related

L-08, L-11, L-13, P-03, S-03, S-04, T-01.
