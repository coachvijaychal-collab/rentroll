# P-01 · Rent receipt

> Source: UIUX Part D "Print views" (p.19); UIUX L-04, T-05; SCOPE §2, §12 (CX-02, CX-10). Build phase 4 (done when it "prints cleanly to A4 with the landlord's branding").

## Meta

| | |
|---|---|
| Type | Print view: separate page, new tab, print dialog on load |
| Route | **Not specified in source** (OPEN-39) |
| Opened from | L04-BTN-RECEIPT (landlord); T05-BTN-PRINT (tenant) |
| Purpose | A numbered proof of rent paid, for the tenant and for the landlord's year-end records. |

## Contents (in order)

1. Landlord name (L15-FLD-RECEIPTNAME) and logo (L15-UPL-LOGO, optional)
2. Receipt number (e.g. `RR-0847`)
3. Tenant
4. Unit
5. Month
6. Amount **in figures and in words**
7. Date received
8. Payment reference
9. Payment QR (CX-02, "printed on every receipt")
10. A signature line

## Rules (common print rules)

- A separate page with **no navigation, no buttons and a white background**, opened **in a new tab** with the **print dialog triggered on load**.
- **Do not** try to hide the app's own interface with print styles.
- Prints cleanly to **A4**.
- For a part payment, the receipt shows the **amount actually received** (L-04).
- A receipt exists only after the landlord marks the payment received.

## Open items

> OPEN: [OPEN-39] No route. When opened from T-05, P-01 must be authorised by the tenant token and must not expose anything beyond this receipt (GR-2, E4-04).

> OPEN: [OPEN-02] P-01 shows a rent amount on a tenant-reachable page.

> OPEN: [OPEN-43] The "amount in words" convention is not specified (Indian lakh/crore wording? "Rupees … only"?).

> OPEN: [OPEN-08] Receipt numbering scope and behaviour on Undo.

> OPEN: [OPEN-56] The source does not say what amount the receipt's payment QR encodes on a receipt for a payment already made: the outstanding balance, the monthly rent, or none.

## Related

L-04, T-05, L-15, S-02.
