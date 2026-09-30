# S-01 · Message composer

> Source: UIUX Part D S-01 (p.18); UIUX E1, E3; SCOPE §3 (PR-2), §10, §11, §12 (CX-03, CX-04, CX-07). Build phase 5 (done when "draft arrives, is editable, and the send-confirmation step records correctly").

## Meta

| | |
|---|---|
| Type | **Modal**: 560px on desktop, full screen on mobile |
| Opened from | L-03, L-04, L-05, L-07, L-12, L-13 (also S02-BTN-SENDLINK) |
| Purpose | The **single place** where every outgoing message is reviewed and sent. This component is where the **"nothing sends by itself"** rule (GR-1) is **enforced in code**. |

## Components

| ID | Type | Content and behaviour |
|---|---|---|
| S01-HDR | Modal header | e.g. **"Message to Suresh Khan · Flat 4C"** |
| S01-CHP-CONTEXT | Chip row | Context reminder, e.g. **"Rent · 18 days overdue · Level 3 of 3"** |
| S01-SEG-TONE | Segmented choice | **Gentle · Direct · Formal**. Pre-selected by days overdue. Changing it **regenerates the draft**. |
| S01-FLD-MESSAGE | Text area | The drafted message, **fully editable**. Auto-grows. A normal editable field, **not a preview**. |
| S01-CHK-PAYLINK | Checkbox | **"Include a payment link"**. Ticked by default for rent messages; **absent** for others. |
| S01-BTN-REGENERATE | Quiet button | **"Write it differently"**. Requests a new draft, keeping any edits in a **restorable** state. |
| S01-BTN-WHATSAPP | Primary button | **"Open in WhatsApp"** |
| S01-BTN-COPY | Secondary button | **"Copy"** |
| S01-BTN-EMAIL | Quiet button | **"Email instead"**, shown **only when an email address exists** |
| S01-BTN-CANCEL | Quiet button | **"Cancel"** |
| S01-MOD-CONFIRMSENT [+] | Modal state | **"Did you send it?"** with **Yes** and **Not yet** |

## Interactions

| Trigger | Result |
|---|---|
| Modal opens | A draft is requested and a **skeleton** shows in the text area for **up to 4 seconds**. If it does not arrive, a plain **template** appears with the quiet note **"Wrote this from a template — edit as needed."** The composer is **never blocked** by the assistant. |
| S01-BTN-WHATSAPP | Opens WhatsApp **in a new tab** with the current text pre-filled → the modal switches to a second state: **"Did you send it?"** with **Yes** and **Not yet**. **Only "Yes" writes the reminder to the timeline.** |
| S01-BTN-COPY | Copies to the clipboard (called directly from the click, S-03), toast confirms ("Copied.", E1-03), and the same **"Did you send it?"** prompt appears |
| S01-SEG-TONE | If the message has been edited, warn before regenerating: **"This will replace your edits."** |
| S01-BTN-REGENERATE | New draft; previous edits kept restorable |
| S01-BTN-CANCEL | Closes with **no record written**. If edited, confirm first. |
| "Yes" in S01-MOD-CONFIRMSENT [+] | Writes the record (for rent: Reminder with level, time, method) → toast **"Reminder recorded on the tenant's history."** (E1-02) → close; calling screen refreshes (e.g. L-03 row) |
| "Not yet" | No record written |

## Why "Did you send it?" is mandatory (from source)

> The "Did you send it?" step is **not optional**. The app hands the message to WhatsApp; it cannot know whether the landlord actually pressed send there. Recording a reminder that was never sent would corrupt the escalation history and produce a wrong tone next time.

## Draft types by caller

| Caller | Draft | Recipient | Pay link | Source |
|---|---|---|---|---|
| L03 "Remind", L04-BTN-REMIND, L05-BTN-REMIND | Rent reminder at the escalation level for days overdue (Gentle / Direct / Formal) | Tenant | Ticked by default | L-03, L-04, L-05 |
| L07-BTN-DISPATCH | Vendor-flavoured: the problem, the unit's address, the tenant's phone, a Maps link | **Vendor** (default) | Absent | L-07 |
| L07-BTN-UPDATETENANT; L-06 drag toast; L-07 Done | Status update; **never** cost or vendor rates (status and category only) | Tenant | Absent | L-06, L-07 |
| L12-BTN-NOTICE | Renewal: current rent, new rent, effective date | Tenant | Absent | L-12 |
| L13-BTN-SEND | Settlement summary | Tenant | Absent | L-13 |
| S02-BTN-SENDLINK | Message with the payment link already embedded | Tenant | Embedded | S-02 |

## Rules

- GR-1: no send path exists other than a landlord click on WhatsApp / Copy / Email, and even those only **hand off**.
- The text area is the draft. What the landlord sends is exactly what is in the field.
- Tone pre-selection follows the ladder in L15-TBL-LADDER (RENT-3, RENT-5).
- Focus is trapped while open, returns to the trigger on close, and Escape closes (E5); Escape with edits confirms first.

## Open items

> OPEN: [OPEN-06] The source example "Rent · 18 days overdue · Level 3 of 3" contradicts the default ladder (day 20 = Formal = level 3), under which 18 days is **Direct, level 2**. Wireframe B also describes the 18-day draft as "firm tone", which is not one of the three levels.

> OPEN: [OPEN-05] The pre-selected tone before the first ladder step (days overdue < 3, or Due and not late) is undefined.

> OPEN: [OPEN-31] Several S-01 gaps: (a) There is no recipient field or selector, yet L-07 needs vendor vs tenant. (b) It is unclear whether the tone segment is shown for non-rent drafts. (c) It is unclear whether "Email instead" also goes through "Did you send it?" (implied, but not stated). (d) "The email composer" in L-11 and L-14 could be S-01 or a direct `mailto:`. (e) What gets recorded, and where, for non-rent messages: E1-02 says "the tenant's history", and L07-TML-HISTORY lists "message sent". (f) The "Opened from" list omits L-06 and S-02. (g) The contact-block "message" buttons (L-05, L-11) could open S-01 or WhatsApp directly.

> OPEN: [OPEN-16] Whether non-rent drafts (vendor, tenant update, renewal) are written by the assistant, which SCOPE limits to "three places only".

> OPEN: [OPEN-33] Welcome messages (new tenant + unit link) and sending receipts are CX-03 uses with no S-01 caller.

## Related

L-03, L-04, L-05, L-06, L-07, L-12, L-13, S-02, S-03, [cross-cutting GR-1](../../cross-cutting.md#gr-1), [Assistant](../../cross-cutting.md#assistant).
