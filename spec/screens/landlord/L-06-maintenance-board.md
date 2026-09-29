# L-06 · Maintenance board

> Source: UIUX Part B L-06 (p.11); UIUX E2; SCOPE §6 (MOD-4), §17. Build phase 3 (done when there is a "full lifecycle from New to Done, with cost captured").

## Meta

| | |
|---|---|
| Route | `/maintenance` |
| Access | Signed in |
| Purpose | See every reported problem, **in order of urgency**, and move it along. |
| Arrives from | Sidebar "Maintenance" |
| Leads to | L-07 detail panel |

## Layout

**Desktop:** four status columns as a board of cards: **New · Assigned · In progress · Done**.
**Mobile:** a single list with a status filter, because horizontal-scrolling boards are unusable on a phone.

## Components

| ID | Type | Content and behaviour |
|---|---|---|
| L06-COL-NEW | Board column | "New". Header shows the count. Highest-priority column, **always leftmost**. |
| L06-COL-ASSIGNED [+] | Board column | "Assigned". Header shows the count. |
| L06-COL-INPROGRESS [+] | Board column | "In progress". Header shows the count. |
| L06-COL-DONE [+] | Board column | "Done". Header shows the count. |
| L06-CRD-REQUEST | Card | Unit number · category · first line of the description · urgency chip · photo thumbnail if present · age in days |
| L06-CHP-URGENCY | Status chip | **Urgent** (danger) · **Normal** (neutral) · **Low** (muted) |
| L06-SEG-FILTER | Segmented choice | **All · Urgent · Unassigned · This property** |
| L06-SEG-STATUS [+] | Segmented choice / filter (mobile only) | Status filter replacing columns on mobile: New · Assigned · In progress · Done |
| L06-BTN-NEW | Primary button | "Log a request", for problems reported by phone or in person |

## Interactions

| Trigger | Result |
|---|---|
| L06-CRD-REQUEST (click) | Opens **L-07** |
| Drag a card between columns | Changes the status, writes a timeline entry, and shows a **toast offering to notify the tenant**. Declining the toast leaves the tenant uninformed, which is allowed. |
| L06-BTN-NEW | Opens **the same form as T-01**, with an added **unit selector** and a **"reported by"** field defaulting to **"phone call"** |
| L06-SEG-FILTER | Filters the board |

## States

| State | Display |
|---|---|
| Loading | Skeleton columns and cards (E3) |
| Empty | **"No open requests. Tenants report problems through their unit link."** Action: **Print door QR codes** (→ P-03) (E2-03) |

## Rules

- Cards in **New** older than **48 hours** gain a subtle left border in **warning** colour; older than **7 days**, **danger** colour. No notification, just a visual.
- Moving a card to **Done** requires either a cost figure or an explicit **"no cost"**. This is what keeps the per-unit spend meaningful.
- A request can be **reopened from Done**. Doing so writes a timeline entry rather than creating a new request.
- The notify-tenant offer opens S-01 (GR-1), and its draft is tenant-safe: status and category only (GR-2, L-07).
- Drag-and-drop must have a keyboard-operable equivalent (E5); the L-07 status dropdown serves.
- The form behind L06-BTN-NEW uses the T-01 fields (category, description, photo, urgency, name, phone) plus the unit selector and "reported by". Landlord screens allow up to **10 photos** (S-04).

## Open items

> OPEN: [OPEN-48] The "This property" filter has no defined property selection. The ordering of cards within a column is not defined; PURPOSE says "in order of urgency", SCOPE §17 says "in order of urgency", and L-03 lists open requests "oldest first".

> OPEN: [OPEN-38] When a card is dragged to Done, the source does not say how the required cost or "no cost" is captured (a prompt? L-07 opens?). It also does not say whether a tenant-liable cost counts toward the unit's maintenance spend.

> OPEN: [OPEN-14] The column is "New" here and the tenant chip is "Received" (T-03); the mapping is taken as New ↔ Received. L-03 refers to a "closed" status that does not exist.

> OPEN: [OPEN-25] Urgency "Low (muted)": `muted` is a text-colour token, not a status colour.

> OPEN: [OPEN-15] Whether the assistant's suggested urgency or the tenant's chosen urgency drives the urgency chip.

> OPEN: [OPEN-52] "Reported by" options beyond "phone call" (e.g. in person) are not enumerated.

## Related

L-07, T-01, S-01, S-04, P-03, [product §10.2](../../product.md#102-maintenance-request-lifecycle-uiux-l-06-l-07-t-01-t-03).
