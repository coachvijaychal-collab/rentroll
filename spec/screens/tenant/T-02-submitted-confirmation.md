# T-02 · Submitted confirmation

> Source: UIUX Part C T-02 (p.16–17); UIUX E1-06; SCOPE §9. Build phase 3.

## Meta

| | |
|---|---|
| Route | **Not specified in source** (OPEN-18) |
| Access | Tenant link holder (same token as T-01); no sign-in |
| Purpose | Confirm the report was captured, give the request number, and get the tenant to **save the link**. |
| Arrives from | T-01 submit |
| Leads to | T-03 · share sheet / clipboard · T-01 (blank) |

## Components

| ID | Type | Content · what happens |
|---|---|---|
| T02-SEC-CONFIRM | Confirmation block | Tick icon · **"Reported. Your request number is R-0412."** · **"Your landlord has been notified."** |
| T02-SEC-SUMMARY | Summary block | What they reported, so they can see it was captured correctly |
| T02-BTN-TRACK | Primary button | **"Check the status"** → T-03 |
| T02-BTN-SAVE | Secondary button | **"Save this link"** → opens the device share sheet so they can bookmark or message it to themselves. On desktop, copies to the clipboard with a toast. |
| T02-BTN-ANOTHER | Quiet button | **"Report something else"** → back to T-01, blank |

## Design note (from source)

> T02-BTN-SAVE is more important than it looks. A tenant who loses the link phones the landlord instead. This is the one moment they are guaranteed to be looking at the screen, so **this is where we ask them to keep it.**

## Rules

- This is a full-screen confirmation (E1-06), not a toast.
- T02-SEC-SUMMARY shows only what the tenant submitted: category, description, photo(s), urgency, name, phone. No landlord-side data (GR-2).
- The request number is shown as the tenant-facing reference (`R-####`). E1's "never show an internal identifier" does not forbid it, because it is the public reference.
- Share and copy follow S-03 behaviour (share sheet, desktop copy fallback, copy called directly from the click).
- Buttons are 48px tall (tenant screens).

## Open items

> OPEN: [OPEN-04] "Your landlord has been notified." There is no notification channel in v1: nothing sends by itself (GR-1), L-06 is explicitly "no notification, just a visual", and there is no email or push. The source does not say how, or whether, the landlord is notified.

> OPEN: [OPEN-18] The route is not specified. It is undefined whether a reload shows T-02 again or returns to T-01.

## Related

T-01, T-03, S-03.
