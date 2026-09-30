# L-05 · Rent detail panel

> Source: UIUX Part B L-05 (p.9–10); SCOPE §10, §12 (CX-05). Build phase 4 (done when "timeline shows every reminder and logged call").

## Meta

| | |
|---|---|
| Route | `/rent/:entryId`; opens as a **detail panel over L-04** |
| Access | Signed in; entry must belong to the signed-in landlord (else Not found, E4-05) |
| Purpose | Everything about one month's rent for one unit, including the **full reminder history**. |
| Arrives from | L04-ROW; L03-ROW-ATTENTION (rent rows) |
| Leads to | S-01, S-02, dialler (CX-05) |

Panel behaviour follows A2 Detail panel: 480px from the right on desktop, full screen on mobile, closes on Escape / close button, warns on unsaved edits, traps focus (E5).

## Components

| ID | Type | Content and behaviour |
|---|---|---|
| L05-HDR | Panel header | "Flat 2A · February 2026" · status chip · close button |
| L05-SEC-AMOUNT | Key-value block | Rent due · amount paid · due date · date paid · payment reference · receipt number |
| L05-SEC-TENANT | Contact block | Tenant name, phone, with **call**, **message** and **copy** icon buttons |
| L05-TML-REMINDERS | Timeline | Every reminder sent, its **level**, **when**, by **which method**; plus any logged calls; plus amount edits (old → new) |
| L05-BTN-REMIND | Primary button | "Send reminder" |
| L05-BTN-PAYLINK | Secondary button | "Payment link" |
| L05-BTN-MARKPAID | Secondary button | "Mark paid" |
| L05-BTN-LOGCALL | Quiet button | "Log a call" |
| L05-FRM-LOGCALL [+] | Inline form | Outcome (dropdown: *promised to pay / no answer / disputed / other*) · note |
| L05-BTN-EDIT | Quiet button | "Edit amount", for pro-rata or agreed adjustments. Any edit is recorded on the timeline with the old and new value. |

## Interactions

| Trigger | Result |
|---|---|
| L05-BTN-REMIND | Opens **S-01** at the correct escalation level |
| L05-BTN-PAYLINK | Opens **S-02** with the **outstanding** amount pre-filled |
| L05-BTN-LOGCALL | Opens a two-field form (L05-FRM-LOGCALL [+]): outcome dropdown and a note. Saves to the timeline as a **reminder record with method "call"**. |
| Call icon in L05-SEC-TENANT | Dials (`tel:`). **On return to the tab**, a prompt appears: **"Log this call?"** Accepting opens the same form as L05-BTN-LOGCALL. |
| Message icon in L05-SEC-TENANT | Messaging hand-off (CX-03) |
| Copy icon in L05-SEC-TENANT | Copies the phone number (S03-BTN-COPY behaviour) |
| L05-BTN-EDIT | Edit the amount due; timeline entry records old and new values |
| L05-BTN-MARKPAID | Records payment (see L-04 Mark paid behaviour) |

## Rules

- The timeline is the escalation history. Only reminders the landlord confirmed as sent ("Did you send it?" → Yes in S-01) appear (S-01, RENT-6).
- Calls are stored as Reminder records with method "call" (ERD: "call notes if phoned").
- Timeline order: newest first (A2 Timeline).

## Open items

> OPEN: [OPEN-49] L05-BTN-MARKPAID's form is not specified (presumably the same fields as L04-FRM-MARKPAID [+]). The source also does not say which buttons (Send reminder, Payment link, Mark paid, Log a call) are shown or hidden once the entry is Paid.

> OPEN: [OPEN-31] The contact-block "message" icon: it is unspecified whether this opens S-01 or opens WhatsApp directly with a blank message.

> OPEN: [OPEN-19] The route of this panel when it is opened over L-03 (not L-04) is unspecified.

## Related

L-04, S-01, S-02, S-03, [cross-cutting CX-05](../../cross-cutting.md#connections).
