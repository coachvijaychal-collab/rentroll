# T-01 · Report a problem

> Source: UIUX Part C intro and T-01 (p.16); UIUX E1, E4; SCOPE §3 (PR-1), §7 Wireframe C, §9, §11 (AI-2). Build phase 3 (with T-02; done when "a request submitted from a phone appears in the database").

## Design brief (applies to all tenant screens)

> The tenant is on a phone, possibly annoyed, has never seen this before, and will not read instructions. There is no sign-in, no menu, and no way to reach anything that is not theirs. **If any screen here takes more than two minutes, they will phone the landlord instead and the product has failed.**

Tenant-screen constraints: mobile-first; never tested on desktop only; 48×48px minimum touch targets; 48px buttons; **no navigation** (A3, A4); GR-2 applies to everything rendered and every response.

## Meta

| | |
|---|---|
| Route | `/u/:unitToken`. **One unguessable token per unit, not the unit number.** |
| Access | Anyone holding the link. **No sign-in.** |
| Purpose | Capture a problem with enough detail to act on, **in under two minutes**. The entry point for tenants. |
| Arrives from | Saved link; door QR (P-03); welcome message; T02-BTN-ANOTHER |
| Leads to | T-02 (on submit); T-03 (earlier reports); dialler |

## Layout

Single column, one-screen scroll. Header identifying the unit, so the tenant knows they have the right link → form → Submit → below the fold, a link to their earlier reports.

## Components

| ID | Type | Content and behaviour |
|---|---|---|
| T01-HDR | Header | Landlord's name or logo · **"Flat 2A, Kulkarni Apartments"** · nothing else |
| T01-SEL-CATEGORY | Dropdown | "What is the problem?": **Plumbing · Electrical · Appliance · Structural · Pest · Cleaning · Something else**. **Required.** Placeholder that is not a valid choice (A2). |
| T01-FLD-DESC | Text area | "Describe it". Placeholder: **"Geyser is leaking from the bottom since yesterday."** **Required, minimum 10 characters.** |
| T01-UPL-PHOTO | Photo uploader | "Add a photo". **Up to 3.** Optional but visually encouraged. See S-04. |
| T01-SEG-URGENCY | Segmented choice | "How urgent?": **Low · Normal · Urgent**. Defaults to **Normal**. |
| T01-FLD-NAME | Text field | Pre-filled from the tenancy record, editable in case a family member is reporting |
| T01-FLD-PHONE | Phone field | Pre-filled, editable (+91, 10 digits) |
| T01-BTN-SUBMIT | Primary button | "Submit". Full width, **48px** tall, **sticky at the bottom of the viewport on mobile** |
| T01-LNK-MYREPORTS | Link | **"My earlier reports (2)"** → T-03. **Hidden when there are none.** |
| T01-BTN-CALL | Quiet button | **"Call the landlord"**. **Always visible**, below the form. Some things need a phone call. |
| T01-BNR-OFFLINE [+] | Banner | Offline banner (see States) |

## Interactions

| Trigger | Result |
|---|---|
| T01-BTN-SUBMIT | Validate → button shows spinner → **request is created** → assistant assigns a suggested category and urgency **in the background** → route to **T-02**. If the assistant is slow or unavailable, the request is still created with the tenant's own choices; **nothing waits on it**. |
| Validation failure | Scroll to the **first invalid field** and show the error **under it**. Never a summary at the top, never a popup. |
| T01-BTN-CALL | Dials the landlord's number (CX-05) |
| T01-LNK-MYREPORTS | → T-03 |

## States and rules

| State | Display |
|---|---|
| Invalid or unknown token | **"This link is not valid. Please ask your landlord for your unit link."** Nothing else; no hints about what a valid link looks like. (E1-10, full screen) |
| Unit is vacant | **Same message as above.** A former tenant's link stops working when the tenancy ends. |
| Submitting | Button spinner, form fields disabled, **no full-screen overlay** |
| Submission failed | Inline message above the button: **"Could not submit. Please try again."** The form keeps everything typed, **including the photo**. |
| Offline | Banner: **"You are offline. Your report will be sent when you reconnect."** The form remains usable. |
| Photo still uploading at submit | Submit waits; button shows **"Uploading photo…"** (S-04) |

Security rules:
- The token is **long and random**. Unit numbers are never used in the URL, because `/u/2A` would let anyone guess `/u/2B`.
- **Rate limit:** 5 submissions per token per hour, with a plain message if exceeded.
- A **bot check runs invisibly**. A tenant should never see a puzzle.
- Tenant-facing wording never uses "error", "invalid", "failed", "unauthorised" (E1 wording rules).
- Response data contains no rent amount, cost, other unit or other tenant (E4-04).

## Open items

> OPEN: [OPEN-01] "One token per unit" conflicts with "a former tenant's link stops working when the tenancy ends" (T-01, E4-02) and with SCOPE §4's "every tenant gets their own unit link". It is undefined whether the token rotates per tenancy, and whether printed door QRs (P-03) then need reprinting.

> OPEN: [OPEN-03] Name and phone are pre-filled for anyone holding the link, and the link is placed as a QR inside the door or on a building notice board (SCOPE CX-11).

> OPEN: [OPEN-18] Routes for T-02 to T-05 are unspecified. Only T-03 is linked from here; T-04 and T-05 have no entry point.

> OPEN: [OPEN-14] The label "Something else" here vs "Other" on L-07. Are they the same stored value?

> OPEN: [OPEN-15] Whether the assistant's suggested category and urgency overwrite the tenant's choices.

> OPEN: [OPEN-50] The rate-limit message copy is not given. The offline wording differs from E1-08.

> OPEN: [OPEN-11] T01-BTN-CALL needs a landlord phone number, which no screen collects.

> Wireframe C intent (SCOPE Diagram 4): "The tenant page is one short form with no sign-in and no mention of money."

> OPEN: [OPEN-23] Wireframe C shows the header "Flat 2A · Report a problem", no name/phone fields, and "Your earlier reports (2)". Wireframes are "arrangement and priority only — not … final wording"; this spec follows UIUX.

## Related

T-02, T-03, S-04, L-06 (same form, landlord side), L-07, [cross-cutting E4](../../cross-cutting.md#e4--permissions--the-boundary-tests).
