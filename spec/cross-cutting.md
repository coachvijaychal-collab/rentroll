# RentRoll — Cross-cutting rules

> Source: **[UIUX]** p.2 ("Two rules that apply to every screen"), Part E (E1–E5), and the general notes in Parts C–D; **[SCOPE]** §3, §11, §12, §13, §16.
> These rules apply to **every** screen and component. A screen spec never overrides them. If a screen spec appears to conflict with a rule here, treat it as OPEN and escalate.

---

## Global rules

<a id="gr-1"></a>
### GR-1 · Nothing sends by itself

> No message ever leaves the system without the landlord pressing send. The assistant drafts into an editable field and never dispatches. *(UIUX p.2; SCOPE §3 PR-2, §11, §16)*

- Every outgoing message (reminder, receipt, notice, vendor job, tenant update, renewal, settlement) goes through **S-01 Message composer**. S-01 is where this rule is enforced in code (UIUX S-01).
- Hand-off only: the app opens WhatsApp, the email app, the dialler, the share sheet or the clipboard, with content pre-filled. The landlord completes the send in that app.
- A send is recorded only after the landlord confirms "Did you send it?" → **Yes** (S-01).
- Firm rule: **the assistant drafts, the landlord decides.** Nothing written by the assistant reaches a tenant without the landlord reading it first. This is a product rule, not a preference (SCOPE §11).
- "Automatic sending" is deliberately excluded. It is a principle, not a limitation to be removed later (SCOPE §16).
- There is no scheduled, timed, on-save or background dispatch of any kind.

<a id="gr-2"></a>
### GR-2 · Tenant-facing data boundary

> No tenant-facing screen ever queries or displays rent amounts, repair costs, other units, or other tenants. *(UIUX p.2; SCOPE §3 PR-3, §4, §8)*

- Applies to what is **rendered** and to the **data behind** the page (API responses, embedded state). See E4-04.
- The tenant side has no path to any money screen (SCOPE §8).
- Tenant-safe wording: tenant updates are built from **status and category only**. Never expose the vendor's rate, the cost recorded, internal notes, or any other unit (UIUX L-07).
- T-04 shows agreement dates but **not rent**: "any screen that displays a money figure is one refactor away from displaying the wrong one" (UIUX T-04 note).

> OPEN: [OPEN-02] UIUX makes an explicit exception: "Receipts on T-05 **do** show amounts, because those are the tenant's own payments", and T05-BTN-PRINT opens P-01, which shows the amount. This contradicts GR-2 as worded, SCOPE §4 ("Only their own unit, and no money"), SCOPE §8 ("no path to any money screen") and E4-04 ("Contains no rent amount"). It is also unclear whether "tenant-facing" covers messages and print views the landlord sends to the tenant: day-10 reminders "state the amount", P-02 lists deduction amounts, and the tenant-liable payment request carries a repair cost.

### GR-3 · Escalate, don't implement

Any ticket that appears to breach GR-1 or GR-2 must be **escalated, not implemented** (UIUX p.2).

### GR-4 · Unit history belongs to the unit

A unit keeps its history when tenants change. Rent entries, requests and photos stay with the unit, not the person (SCOPE §15).

---

<a id="assistant"></a>
## Assistant

The app has an assistant built in. It is used in **three places only**, and **never to send anything** (SCOPE §11).

| ID | Where | What it does | Why it matters | Screens |
|---|---|---|---|---|
| AI-1 | Rent reminders | Writes the message at the right tone for how late the payment is: warm at day three, direct at day ten, formal at day twenty | This is the feature that changes behaviour. Landlords avoid chasing early because the words feel rude; having the right words ready removes that hesitation. | S-01 (from L-03, L-04, L-05) |
| AI-2 | Maintenance requests | Reads what the tenant typed and suggests a category and an urgency | Consistent sorting is what makes the "what keeps breaking" view possible later (e.g. L09-TAB-MAINT "Plumbing reported 4 times in 12 months"). | T-01 (background), L07-SEL-CATEGORY |
| AI-3 | Deposit settlement | Turns the deposit amount, the deductions and their reasons into a written statement | A clear statement that explains each deduction turns an argument into a signature. | L13-BTN-GENERATE, P-02, S-01 |

Behavioural guarantees:
- **Never blocking.** S-01 shows a skeleton for at most **4 seconds**, then falls back to a plain template with the quiet note "Wrote this from a template — edit as needed." (UIUX S-01, E1-09, E3).
- **Never waited on.** T-01 creates the request with the tenant's own choices if the assistant is slow or unavailable (UIUX T-01).
- Output is always an editable draft or an editable pre-fill (L07-SEL-CATEGORY "Pre-filled by the assistant, editable").

> OPEN: [OPEN-16] "Three places only" conflicts with S-01, which requests a draft (with template fallback) every time it opens, including for vendor dispatch (L07-BTN-DISPATCH), tenant status updates (L07-BTN-UPDATETENANT) and renewal notices (L12-BTN-NOTICE). It is undefined whether those drafts come from the assistant or from templates.

> OPEN: [OPEN-15] When the assistant suggests a category or urgency that differs from the tenant's choice, the source does not say which one is stored or shown on L-06 and L-07.

---

<a id="connections"></a>
## Connections

All twelve are available from day one. **None is a screen of its own.** Each appears inside the workflow where it is needed. They open apps the landlord and tenant already use: nothing to install, nothing to configure, nothing that can stop working or start charging (SCOPE §12, §13).

| ID | Connection | What it does | Source-listed uses | Where it lives in UIUX |
|---|---|---|---|---|
| CX-01 | Pay by UPI | Opens the tenant's payment app with the exact amount already filled in | Monthly rent from a reminder · deposit at move-in · a repair the tenant is liable for · a late fee | S-02 (S02-BTN-PAY, S02-BTN-COPYLINK, S02-BTN-SENDLINK); S01-CHK-PAYLINK; L05-BTN-PAYLINK; L07-CHK-TENANTLIABLE |
| CX-02 | Payment QR | The same payment as a scannable code | Printed on every receipt · shown on the rent screen so a landlord can hold up his laptop · shared with a tenant whose phone will not open links | S02-IMG-QR, S02-BTN-DOWNLOADQR; P-01 |
| CX-03 | Send on WhatsApp | Opens WhatsApp with the message already typed, for the landlord to review and send | Rent reminders · receipts · maintenance updates · sending a vendor the job and address · welcoming a new tenant with their link · renewal notices | S01-BTN-WHATSAPP; contact-block message buttons (L05, L11); T04-BTN-MESSAGE (tenant → landlord, blank) |
| CX-04 | Send by email | Opens the email app with subject and body ready | The year's rent records to the accountant in March · a copy of the agreement to a tenant who needs it for their office · a monthly statement to a property owner | S01-BTN-EMAIL; L11-BTN-SENDAGREEMENT; L14-BTN-EMAILCA |
| CX-05 | Tap to call | Dials without copying the number, then offers to log the call | Calling a tenant from an overdue rent row · calling from a maintenance request · calling a vendor · on the tenant's own page, so they can reach the landlord without saving his number | L05-SEC-TENANT call icon (+ "Log this call?"); L11-SEC-CONTACT; T01-BTN-CALL; T04-BTN-CALL |
| CX-06 | Open in Maps | Turns an address into directions | The vendor being sent to a flat · a prospective tenant coming to view a vacant unit · the location shown on the property record | L09-BTN-MAP; Maps link inside the L07-BTN-DISPATCH draft |
| CX-07 | Copy in one tap | Puts text on the clipboard | Any drafted message · a unit's link · the landlord's UPI ID · a receipt number | S03-BTN-COPY; S01-BTN-COPY; L09-BTN-COPYLINK; S02-BTN-COPYLINK; contact-block copy buttons |
| CX-08 | Share | Opens the phone's own share menu | Sending a new tenant their unit link · passing a receipt to someone · sharing vacancy details with a broker | S03-BTN-SHARE; L09-BTN-SHARELINK; T02-BTN-SAVE; L11-SEC-DOCS share; L14-TBL-DOCS share |
| CX-09 | Add to calendar | Creates a calendar entry in whatever calendar the landlord already uses | Agreement expiry · the notice period ending · a scheduled vendor visit · a rent due date | L12-BTN-CALENDAR (downloads a calendar file) |
| CX-10 | Print or save as PDF | A clean printable page | Rent receipts · the monthly statement · the deposit settlement · a one-page summary of an agreement | P-01, P-02, P-03 |
| CX-11 | Unit QR code | A printable code that opens that unit's reporting page | A sticker inside the flat door · the welcome sheet handed over at move-in · a notice board in the building | P-03; L09-BTN-QR; L08-BTN-PRINTQR |
| CX-12 | Export to a spreadsheet | Downloads the data as a file | The rent ledger for the accountant · maintenance spend per unit · the current tenant list · the deposit register | L04-BTN-EXPORT; L14-BTN-EXPORT-* |

Implementation rules for connections:
- **Share:** use the device share sheet where available. On desktop, fall back to copy with a toast. Never show a broken share icon (S-03).
- **Copy:** must be called directly from the click, never after an `await`. The icon changes to a tick for 2 seconds (S-03).
- **Pay app button:** disabled on desktop with the tooltip "Scan the code with your phone instead." (S-02).
- **No UPI ID saved:** payment features show a prompt to add it, with a link to L-15. They are never hidden, and the QR is never broken (L-02, S-02).
- **Calendar:** downloads a calendar file; toast "Added — open the file to save it to your calendar." (L-12, E1-05).
- **Email with attachments:** the app cannot attach files. Helper text tells the landlord to attach the downloaded file after the email app opens (L11-BTN-SENDAGREEMENT, L14-BTN-EMAILCA).
- **Exports:** CSV that opens correctly in Excel **with the ₹ symbol intact** (UIUX Part F).

> OPEN: [OPEN-33] These source-listed connection uses have no screen or control in UIUX:
>
> | Connection | Uses with no screen or control |
> |---|---|
> | CX-01 | Deposit payment at move-in; late fee (late fees are not defined anywhere) |
> | CX-03 | Sending a receipt; welcoming a new tenant with their link |
> | CX-04 | Monthly statement to a "property owner" (a role not defined elsewhere) |
> | CX-06 | Prospective tenant viewing a vacant unit |
> | CX-07 | Copying the landlord's UPI ID; copying a receipt number |
> | CX-08 | Passing a receipt; sharing vacancy details with a broker |
> | CX-09 | Notice-period end; vendor visit; rent due date |
> | CX-10 | "Monthly statement"; one-page agreement summary (no print view defined) |
> | CX-11 | Welcome sheet; building notice board |

---

## Formats and identifiers

| Item | Rule | Source |
|---|---|---|
| Dates | Display as **DD MMM YYYY** everywhere | UIUX A2 |
| Months | Shown as "February 2026" (L-04, L-05); URL param `month=YYYY-MM` | UIUX L-04 |
| Money | ₹, whole rupees, no decimals, thousands separators; tabular figures in tables | UIUX A1, A2 |
| Phone | +91, 10 digits; spaces and dashes stripped on save | UIUX A2 |
| UPI ID | Shape `name@handle`; validated for shape, not verified | UIUX L-02 |
| Receipt number | `RR-` + number, e.g. `RR-0847` | UIUX L-04, E1 |
| Request number | `R-` + number, e.g. `R-0412` | UIUX T-02, E1 |
| Export filename | e.g. `rent-2026-02.csv` | UIUX L-04, E1 |
| Financial year label | "FY 2025-26" | UIUX L14-BTN-EMAILCA |

> OPEN: [OPEN-08] The numbering scope (per landlord or global), zero-padding width, and what happens to a receipt number when "Mark paid" is undone (reused or burned) are not specified. See also OPEN-43 for locale formats.

---

## E1 · Every message the system shows

Exact copy. Match the wording verbatim.

| ID [+] | Situation | Message | Type |
|---|---|---|---|
| E1-01 | Payment recorded | Payment recorded. Receipt RR-0847 created. | Toast with Undo |
| E1-02 | Reminder logged | Reminder recorded on the tenant's history. | Toast |
| E1-03 | Copied | Copied. | Toast, 2 seconds |
| E1-04 | Export ready | Downloaded rent-2026-02.csv | Toast |
| E1-05 | Calendar file | Added — open the file to save it to your calendar. | Toast |
| E1-06 | Request submitted (tenant) | Reported. Your request number is R-0412. | Full screen — T-02 |
| E1-07 | Save failed | Could not save. Your changes are still here — try again. | Inline, above the form |
| E1-08 | Network lost | You are offline. We will save this when you reconnect. | Banner |
| E1-09 | Assistant unavailable | Wrote this from a template — edit as needed. | Quiet note inside S-01 |
| E1-10 | Invalid tenant link | This link is not valid. Please ask your landlord for your unit link. | Full screen |
| E1-11 | Rent rows missing | This month's rent rows have not been created. | Banner with action |

Screen-specific copy that is **not** in the E1 table (defined in the screen specs): "Email or password is incorrect." (L-01); "Could not submit. Please try again." (T-01); "You are offline. Your report will be sent when you reconnect." (T-01); "Nothing needs your attention today." (L-03); "Part paid — ₹4,000 pending" (L-04); "Expired 14 days ago" (L-12); "This will replace your edits." (S-01); "Did you send it?" (S-01); "Log this call?" (L-05); "Uploading photo…" (S-04); "That file is too large" / "That file type is not supported" (S-04); "Scan the code with your phone instead." (S-02); "Scan to report a problem" (P-03).

**Wording rules:**
1. Never blame the user.
2. Never show a code or an internal identifier.
3. Never use the words **error**, **invalid**, **failed**, or **unauthorised** in tenant-facing text.
4. Always say what happens next.

> OPEN: [OPEN-50] The T-01 offline banner ("…Your report will be sent when you reconnect.") differs from E1-08 ("…We will save this when you reconnect."). The T-01 rate-limit message ("a plain message if exceeded") has no copy. Toasts default to 4 seconds (A2), but E1-01's Undo lasts 10 seconds (see OPEN-08).

---

## E2 · Empty states

| ID [+] | Screen | Message | Action offered |
|---|---|---|---|
| E2-01 | L-04 Rent, no units | Add a unit and this month's rent will appear here. | Add unit |
| E2-02 | L-04 Rent, all paid | Everything is paid for February. Nice. | None |
| E2-03 | L-06 Maintenance | No open requests. Tenants report problems through their unit link. | Print door QR codes |
| E2-04 | L-08 Units | Your properties and units live here. | Add your first unit |
| E2-05 | L-12 Agreements | Nothing expiring in the next 90 days. | Switch to All |
| E2-06 | L-13 Deposits | Deposits appear here once you add tenants. | Add tenant |
| E2-07 | T-03 Tenant reports | You have not reported anything yet. | Report a problem |
| E2-08 | T-05 Tenant receipts | Receipts appear here once your landlord records a payment. | None |

Plus the L-03 states "Nothing needs your attention today." (a deliberate **reward** state, not an empty state) and "Add your first property to see your dashboard" (see L-03).

Rule (A2): one line explaining what would appear here, plus the button that creates the first one. Never just "No data".

---

## E3 · Loading

| Context | Behaviour |
|---|---|
| Page load | Skeleton shapes matching the real layout. Never a centred spinner on a blank page. |
| Row action | Spinner inside the button only; the rest of the screen stays usable. |
| Assistant draft | Skeleton lines inside the text area, with a **4-second** ceiling before falling back to a template. |
| Photo upload | Thumbnail appears instantly from the local file with a progress ring over it. |
| Long operations | Anything expected to take **over 10 seconds** does not exist in version one. If a feature needs that long, it is scoped wrong. |

---

## E4 · Permissions — the boundary tests

QA treats these as the **highest-severity** test cases in the product.

| ID [+] | Test | Expected |
|---|---|---|
| E4-01 | Open a unit link belonging to another landlord's unit | Invalid link message (E1-10) |
| E4-02 | Open a former tenant's link after the tenancy ended | Invalid link message (E1-10) |
| E4-03 | Alter the token in a valid tenant URL | Invalid link message (E1-10) |
| E4-04 | Inspect the data behind any tenant page | Contains no rent amount, no cost, no other unit, no other tenant |
| E4-05 | Request another landlord's rent, unit, tenant or request record while signed in | Not found |
| E4-06 | Reach any landlord route while signed out | Redirect to L-01, then return to the intended screen after signing in |
| E4-07 | Open a document belonging to another landlord | Not found |

Additional access rules stated on screens:
- L-01: a signed-in user hitting `/signin` is redirected to L-03.
- L-02: reachable only while the account has no property; cannot be revisited afterwards.
- T-01: invalid/unknown token **and** vacant unit both show E1-10, with no hints about what a valid link looks like.
- Tenant tokens are long and random. Unit numbers are never used in the URL, because `/u/2A` would let anyone guess `/u/2B`.
- Tenant submissions: rate limit of **5 per token per hour**, with a plain message if exceeded. An invisible bot check; a tenant never sees a puzzle.
- Cross-landlord access returns **Not found** (not "forbidden"), so a record's existence is not revealed.

> OPEN: [OPEN-01] E4-02 (a former tenant's link is invalid) cannot hold if the token is "one per unit" and the door QR sticker (P-03) is meant to stay on the door. The token must be per tenancy or rotated when a tenancy ends, which invalidates printed stickers.

> OPEN: [OPEN-03] The unit link grants access to T-03, T-04 and T-05 (receipts with amounts, agreement dates) and pre-fills the tenant's name and phone on T-01. SCOPE CX-11 places the same link as a QR "inside the flat door" and "on a notice board in the building", so anyone who scans it (visitors, neighbours) could see the current tenant's name, phone, receipts and report history.

> OPEN: [OPEN-02] E4-04 conflicts with T-05's receipt amounts (see GR-2).

---

## E5 · Accessibility floor

- Every control reachable and operable by keyboard, with a visible focus ring. Tab order follows reading order.
- Text contrast at least **4.5:1**; status chips are tested against their tinted backgrounds specifically. *(See OPEN-24: some A1 tokens fail this.)*
- Icon-only buttons carry an accessible label and a visible tooltip on hover.
- Form errors are announced, and the label is programmatically tied to its field.
- Detail panels and modals trap focus, return it to the trigger on close, and close on Escape.
- Status is never carried by colour alone; every chip has a word.
- Photo thumbnails carry meaningful alternative text, not the file name.

Implication: drag-and-drop on L-06 must have a keyboard-operable equivalent. The L07-HDR status dropdown provides one.

---

## Print views (common rules)

Each print view (P-01, P-02, P-03) is a **separate page** with no navigation, no buttons and a white background, **opened in a new tab with the print dialog triggered on load**. Do not try to hide the app's own interface with print styles. Print views carry the landlord's branding (name from L15-FLD-RECEIPTNAME, optional logo L15-UPL-LOGO) and print cleanly to **A4** (UIUX S-04/Print views, L-15, Part F).

---

## Interaction conventions (collected from the screens)

| Convention | Source |
|---|---|
| Filters update the table without a page reload and are reflected in the URL, so a view can be shared or bookmarked. | L04-SEG-FILTER |
| Buttons inside a table row stop row-click propagation. | A2 Data table; L04-BTN-REMIND |
| A state-changing action replaces its button the moment the state changes (no double submit). | L-04 |
| Validation on blur; on submit, scroll to the first invalid field and show the error under it. Never a summary at the top, never a popup. | A2; T-01 |
| Failed saves keep everything typed (including photos) and show an inline message above the form/button. | E1-07; T-01 |
| Offline: show a banner; the form remains usable; save/send on reconnect. | E1-08; T-01 |
| Destructive actions sit behind a confirm dialog whose button names the action. | A2 |
| Unsaved edits: panels and S-01 warn or confirm before closing or discarding. | A2 Detail panel; S-01 |
| Every state change of consequence writes a timeline entry (payments, edits, reminders, calls, request status, reopen). | L-05, L-06, L-07 |
