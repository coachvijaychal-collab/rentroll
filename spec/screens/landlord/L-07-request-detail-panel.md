# L-07 · Request detail panel

> Source: UIUX Part B L-07 (p.11–12); SCOPE §11 (AI-2), §12 (CX-01, CX-03, CX-06). Build phase 3.

## Meta

| | |
|---|---|
| Route | `/maintenance/:requestId` (detail panel over L-06) |
| Access | Signed in; request must belong to the signed-in landlord (else Not found, E4-05) |
| Purpose | Everything about one reported problem, and every action needed to close it. |
| Arrives from | L06-CRD-REQUEST; L03-ROW-ATTENTION (request rows) |
| Leads to | S-01 (vendor job, tenant update), S-02 (tenant-liable cost) |

## Components

| ID | Type | Content and behaviour |
|---|---|---|
| L07-HDR | Panel header | Request number · unit · urgency chip · **status dropdown** (New · Assigned · In progress · Done) |
| L07-SEC-REPORT | Content block | What the tenant wrote, **verbatim**, with the date and their name. **Never edited.** |
| L07-GAL-PHOTOS | Photo strip | **Before** photos from the tenant; **after** photos added by the landlord. Tap to enlarge. |
| L07-SEL-CATEGORY | Dropdown | Pre-filled by the assistant, editable. Options: **Plumbing · Electrical · Appliance · Structural · Pest · Cleaning · Other** |
| L07-FLD-VENDOR | Text field | Vendor name and phone. Remembers previously used vendors as suggestions. |
| L07-FLD-COST | Money field | What it cost. **Required to close.** |
| L07-CHK-NOCOST [+] | Checkbox / explicit choice | "No cost". The explicit alternative to a cost figure (L-06 rule) |
| L07-CHK-TENANTLIABLE | Checkbox | "Tenant is liable for this cost". When ticked, offers a payment link instead of absorbing the cost. |
| L07-BTN-PAYREQUEST [+] | Button (revealed) | "Send payment request". Visible only when L07-CHK-TENANTLIABLE is ticked. |
| L07-BTN-DISPATCH | Primary button | "Send job to vendor" |
| L07-BTN-UPDATETENANT | Secondary button | "Update the tenant" |
| L07-TML-HISTORY | Timeline | Every status change, message sent and note added |

## Interactions

| Trigger | Result |
|---|---|
| L07-BTN-DISPATCH | Opens **S-01** with a **vendor-flavoured draft** containing: the problem, the unit's address, the tenant's phone, and a **Maps link** (CX-06). Recipient defaults to the **vendor's number, not the tenant's**. |
| L07-BTN-UPDATETENANT | Opens **S-01** with a **status-update draft addressed to the tenant**. The draft never mentions cost or vendor rates. |
| L07-CHK-TENANTLIABLE | Reveals a **"Send payment request"** button (L07-BTN-PAYREQUEST [+]) that opens **S-02** with the cost pre-filled |
| Status set to Done | Validates that a cost or "no cost" is present → prompts to add an after photo → offers to notify the tenant |
| Status changed (any) | Writes a timeline entry (L-06 rule) |
| Status set from Done to another status | Reopen; timeline entry, same request (L-06 rule) |
| Photo tap | Enlarge |

## Rules

- **Never expose to the tenant:** the vendor's rate, the cost recorded, internal notes, or any other unit. The tenant update draft is built from **status and category only** (GR-2).
- The tenant's original report (L07-SEC-REPORT) is immutable.
- Cost and "no cost" are mutually exclusive; one of them is required to reach Done.
- The cost is filed against the unit (SCOPE J4) and feeds L09-TAB-MAINT and L-09 lifetime spend, the L14 maintenance-spend export, and L13-BTN-FROMREQUESTS.
- Landlord photo uploads (after photos) allow up to **10** (S-04).
- Messages are recorded on L07-TML-HISTORY only after "Did you send it?" → Yes (S-01).

## Open items

> OPEN: [OPEN-38] The timeline lists "note added", and internal notes must never reach the tenant, but no control for adding a note is defined.

> OPEN: [OPEN-14] Category label "Other" here vs "Something else" on T-01.

> OPEN: [OPEN-15] Assistant-suggested vs tenant-chosen category and urgency: which is stored, and whether the tenant's original choice is retained.

> OPEN: [OPEN-31] S-01 has no recipient field, yet this screen needs recipient switching (vendor vs tenant). It is also undefined whether the S-01 tone control appears for vendor and tenant-update drafts, and whether those drafts come from the assistant or templates (OPEN-16).

> OPEN: [OPEN-44] "Remembers previously used vendors" implies a Vendor store that is not in the ERD.

> OPEN: [OPEN-53] Tap-to-call "from a maintenance request" and "calling a vendor" (SCOPE CX-05) have no control here, and it is undefined where such calls are logged.

## Related

L-06, S-01, S-02, S-04, L-09, L-13, T-03.
