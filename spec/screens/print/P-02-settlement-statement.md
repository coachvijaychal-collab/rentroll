# P-02 · Settlement statement

> Source: UIUX Part D "Print views" (p.19); UIUX L-13; SCOPE §5 (J6), §11 (AI-3), §12 (CX-10). Build phase 7 (with L-13).

## Meta

| | |
|---|---|
| Type | Print view: separate page, new tab, print dialog on load |
| Route | **Not specified in source** (OPEN-39) |
| Opened from | L13-BTN-PRINT |
| Purpose | "Turn a potential argument into a document" / "turns an argument into a signature". |

## Contents (in order)

1. Tenancy dates
2. Deposit held
3. Each deduction **with reason and thumbnail** (photo)
4. Total (deductions)
5. Balance **refundable** or **owed** (owed by the tenant when deductions exceed the deposit; wording changes accordingly)
6. Space for **both signatures** (landlord and tenant)

Branding: landlord name and optional logo (L15-FLD-RECEIPTNAME, L15-UPL-LOGO), as for print views generally.

## Rules

- Common print rules: no navigation, no buttons, white background, new tab, print dialog on load; no print-style hiding of the app UI; A4.
- Once the settlement is marked settled (L13-BTN-CLOSE), the statement is **read-only** and filed under Documents. Corrections require a new statement that **references the first**.
- Deductions without a photo still print (the photo was optional, with a warning).

## Open items

> OPEN: [OPEN-42] Whether P-02 includes the assistant-written statement text (AI-3), and how a correction statement is printed and labelled.

> OPEN: [OPEN-02] P-02 is sent to the tenant and shows deduction amounts, including repair costs (via L13-BTN-FROMREQUESTS). The source does not say whether this falls under GR-2's "repair costs" restriction.

> OPEN: [OPEN-39] No route.

## Related

L-13, L-14, S-01.
