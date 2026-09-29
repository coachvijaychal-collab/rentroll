# S-02 · Payment sheet

> Source: UIUX Part D S-02 (p.18); UIUX L-02, L-05, L-07; SCOPE §12 (CX-01, CX-02, CX-07). Build phase 5 (done when "a phone opens the payment app with the right amount; desktop shows the QR").

## Meta

| | |
|---|---|
| Type | Sheet / modal (landlord side) |
| Opened from | L05-BTN-PAYLINK (outstanding amount); L07-BTN-PAYREQUEST [+] via L07-CHK-TENANTLIABLE (repair cost) |
| Purpose | Produce a UPI payment (link + QR) for an exact amount, to be shown, copied or sent. |

## Components

| ID | Type | Content · what happens |
|---|---|---|
| S02-FLD-AMOUNT | Money field | Pre-filled with the **outstanding amount**, editable |
| S02-FLD-NOTE | Text field | Pre-filled, e.g. **"Rent Feb 2026 — Flat 2A"**. **Appears in the tenant's payment app.** |
| S02-IMG-QR | QR image | **Regenerates whenever the amount changes.** Large enough to scan from a laptop screen. |
| S02-BTN-PAY | Primary button | **"Open payment app"**. Works on the tenant's phone; on desktop it is **disabled** with the tooltip **"Scan the code with your phone instead."** |
| S02-BTN-COPYLINK | Secondary button | Copies the payment link so it can be pasted into any message |
| S02-BTN-SENDLINK | Secondary button | Opens **S-01** with the payment link already embedded |
| S02-BTN-DOWNLOADQR | Quiet button | Saves the QR as an image |
| S02-LNK-SETTINGS [+] | Prompt with link | Shown **instead of the QR** when no UPI ID is saved; links to **L-15** |

## Rules

- The payment link and QR encode the landlord's UPI ID (L15-FLD-UPI), the amount (S02-FLD-AMOUNT) and the note (S02-FLD-NOTE).
- **No UPI ID saved:** show a prompt with a link to L-15 **rather than a broken QR** (payment features are never hidden, L-02).
- **The sheet never claims payment has been received.** Marking paid is always a separate, deliberate act by the landlord (L04-BTN-MARKPAID / L05-BTN-MARKPAID).
- Copy follows S-03 (direct from click; tick for 2 s; toast "Copied.").
- Disabled button shows its reason in a tooltip (A2).
- Amounts: whole rupees (money field).

## Open items

> OPEN: [OPEN-32] S02-BTN-PAY "works on the **tenant's** phone", but S-02 is only opened from landlord screens. On the landlord's own phone, opening a UPI app to pay himself makes no sense. The intended user and device for this button are unclear.

> OPEN: [OPEN-33] The deposit-at-move-in and late-fee payment uses (CX-01) have no S-02 caller. Late fees are not defined anywhere.

> OPEN: [OPEN-55] The exact UPI link format and parameters are not specified (only "opens the tenant's payment app with the exact amount already filled in").

## Related

L-05, L-07, L-15, S-01, S-03, P-01 (payment QR on receipts).
