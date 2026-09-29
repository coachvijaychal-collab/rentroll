# RentRoll — Product architecture

> Source: **[SCOPE]** *RentRoll — Product Scope Document v1.0* (all 18 sections, Diagrams 1–8), plus the parts of **[UIUX]** *RentRoll — UI/UX Specification v1.0* that define product-level behaviour.
> Every section below cites where it came from. `> OPEN:` blocks mark contradictions or gaps that this spec does **not** resolve; the full list is in [index.md § Open items](index.md#open-items).

---

## 1. Product summary

| Field | Value |
|---|---|
| Product | A web app for landlords and tenants |
| Purpose | Make renting organised, transparent and tension-free |
| Built for | Landlords with 5 to 50 units; PG and co-living operators |
| Users | Landlord (signs in) and tenant (opens a link) |
| Market | Small landlords in India (UPI, WhatsApp, ₹, +91) |
| Version | 1.0 |

RentRoll keeps a rental business in one place. The landlord signs in and sees everything — who has paid, what is broken, which agreement is about to expire. The tenant does not sign in at all: they open one link, saved once, and use it to report a problem or check its status. *(SCOPE §1)*

Most small landlords in India run their properties on a diary, a spreadsheet and a WhatsApp group. That works until it doesn't. Rent goes uncollected because nobody is certain who has paid. An agreement expires without anyone noticing, and months pass at the old rent. A deposit argument at move-out is settled by whoever remembers more confidently, because nobody has a photo. None of these are dramatic failures. **They are quiet leaks, and they repeat every month.** *(SCOPE §1)*

### 1.1 The four ideas *(SCOPE §1)*

| ID | Idea | Meaning |
|---|---|---|
| IDEA-1 | One record for every unit | Rent history, photos, repairs and documents live together, for years. |
| IDEA-2 | Dates that watch themselves | Rent due dates and agreement expiry are tracked by the app, not by memory. |
| IDEA-3 | A link for the tenant | No account, no password, no app to install. One page they can use in two minutes. |
| IDEA-4 | Everything ready to send | Reminders, receipts and notices are drafted for the landlord to review and send in one tap. |

Outcome the landlord feels: **they stop carrying the rental business in their head.**

### 1.2 The problem *(SCOPE §2)*

**Landlord today**

| Pain | Description |
|---|---|
| Uncertainty about money | Rent arrives by UPI to a personal number; the notification is buried. On the 12th they are not sure who has paid. |
| Avoiding the awkward message | They do not chase on day three because it feels rude, wait until day twenty-five, then send something sharper than meant. |
| Dates that slip past | Nothing announces an expiry. An agreement that lapsed in November is discovered in March; four months of escalation are gone. |
| Interruptions | Maintenance arrives as phone calls at inconvenient hours; half are forgotten by next morning. |
| Arguments without evidence | At move-out nobody has a photo of move-in condition; deposit returned in full because arguing is not worth it. |
| March panic | The accountant reconstructs a year of rental income from bank statements because no receipts were issued. |

**Tenant today**

- No receipt — a problem when they need proof of rent paid.
- No idea whether their repair request was noted, or when someone is coming.
- Uncertainty about the exact amount and where to send it.
- At move-out, a deposit deduction with no explanation attached.

**Insight:** both sides want the same thing — a clear record. The landlord wants to know what is owed; the tenant wants proof of what they paid and what they reported. One shared record solves both and removes most of the tension.

---

## 2. Vision and design principles *(SCOPE §3)*

Vision: *A rental business should feel like a tidy folder, not a memory test.*

| ID | Principle | What it means in the product |
|---|---|---|
| PR-1 | The tenant never signs up | A tenant who must create an account to report a leaking tap will call instead. One saved link, no password, works on any phone. |
| PR-2 | Nothing sends by itself | Every message is drafted by the app and sent by the landlord. A firm reminder sent automatically to someone who paid yesterday damages a relationship permanently. → enforced as **GR-1** ([cross-cutting.md](cross-cutting.md#gr-1)) |
| PR-3 | Money stays private | The tenant's pages never show rent figures, repair costs or anything about other units. → enforced as **GR-2** ([cross-cutting.md](cross-cutting.md#gr-2)) |
| PR-4 | Dates are the product | Rent due and agreement expiry are the two things the app watches so the landlord does not have to. |
| PR-5 | Evidence, always | Photos at move-in, photos on every repair, a written reason on every deduction. This is what makes settlement calm. |
| PR-6 | One tap to act | Wherever the app shows a problem, the action to fix it is on the same screen. |

---

## 3. Users *(SCOPE §4)*

| | Landlord | Tenant |
|---|---|---|
| How they get in | Signs in with email and password | Opens a saved link. No account. |
| How often | A few times a week; more around the 1st to 10th | A few times a year, when something breaks |
| On what | Laptop mostly, phone sometimes | Phone, almost always |
| What they see | Everything — all units, all money, all history | Only their own unit, and no money |
| What they want | To know nothing is slipping | To be heard, and to have proof |

A third party, the **vendor** (plumber, electrician etc.), never uses the app. They receive jobs by message from the landlord (SCOPE §14, Diagram 7; UIUX L-07).

Structural facts: one landlord has many properties; each property has many units; each unit has one current tenant and a history of past tenants. **Every tenant gets their own unit link.**

> OPEN: [OPEN-01] "Every tenant gets their own unit link" (SCOPE §4) conflicts with "one unguessable token per unit" (UIUX T-01) and with "a former tenant's link stops working when the tenancy ends" (UIUX T-01, E4). See [index.md](index.md#open-01).

Access for a caretaker or assistant is **not** in v1 (see §11.3).

---

## 4. Modules *(SCOPE §6)*

Eight modules. The first four are what the landlord uses most weeks; the last four prevent the expensive mistakes.

| ID | Module | What it shows | What the landlord can do from it | Screens |
|---|---|---|---|---|
| MOD-1 | Portfolio dashboard | Occupied against vacant, collected this month, dues outstanding, agreements expiring soon, income over time | Jump straight to whatever is red. The "is anything wrong" screen. | L-03 |
| MOD-2 | Rent due board | A grid of month against unit — paid, pending, or overdue by so many days | Send the drafted reminder, share a payment link, mark payment received, issue and send the receipt | L-04, L-05, P-01 |
| MOD-3 | Tenant request portal (the tenant's page) | To the tenant: a simple form and the status of what they reported | Nothing — this page belongs to the tenant. No rent, no costs, no other units. | T-01 … T-05 |
| MOD-4 | Maintenance board | Every request by status, with photos, the vendor assigned and what it cost | Assign a vendor with the address, update the tenant, record the cost against the unit | L-06, L-07 |
| MOD-5 | Unit register | Every unit, its rent, its deposit, its condition photos and its full repair history | Add units, print the door QR, review what a unit has cost over the years | L-08, L-09, P-03 |
| MOD-6 | Tenant record | Contact details, agreement dates, rent paid to date, deposit held, documents | Call, message, share the unit link, attach the agreement | L-10, L-11 |
| MOD-7 | Agreement tracker | Everything expiring in 90, 60 and 30 days, with the renewal value calculated | Send a renewal notice, add the date to a calendar, record a notice served | L-12 |
| MOD-8 | Deposit and settlement | Deposit held, each deduction with its reason and photo, the balance due back | Build the settlement statement, print it, send it to the tenant | L-13, P-02 |

Supporting screens that are not modules: L-01 Sign in, L-02 First-run setup, L-14 Documents & exports, L-15 Settings.

> OPEN: [OPEN-22] MOD-2 is described as "a grid of month against unit" and Wireframe B shows the drafted reminder inline below the table. UIUX L-04 specifies a single-month table with a month stepper, and reminders open the S-01 modal. The UIUX cover says it is "the source of truth for version one", which favours L-04, but the source does not state that it overrides SCOPE.

> OPEN: [OPEN-12] MOD-7 lists "record a notice served". UIUX L-12 has "Record renewal" instead, and no screen defines how a notice (landlord → tenant or tenant → landlord) is recorded.

> OPEN: [OPEN-23] SCOPE §16 says "Landlord workspace: all eight modules, with sign-in", but MOD-3 is the tenant portal (no sign-in), and the IA's eight landlord sections include Documents & exports, which is not a module.

**Deliberately not in the product** *(SCOPE §6)*: listing vacant flats, tenant background checks, accounting software integration, and anything that sends a message without the landlord reading it first.

---

## 5. Information architecture *(SCOPE §8, Diagram 5; UIUX Screen map, A3)*

Two separate worlds sharing one set of records. Everything on the left needs a sign-in; everything on the right needs only a link. **The tenant side has no path to any money screen.**

```
RentRoll
├── Landlord workspace (requires sign-in)            ├── Tenant link (one link per unit, no sign-in)
│   ├── Portfolio dashboard ........ L-03 (hub)      │   ├── Report a problem ............ T-01 (+ T-02 confirmation)
│   ├── Rent due board ............. L-04, L-05      │   ├── Track what I reported ....... T-03
│   ├── Maintenance board .......... L-06, L-07      │   ├── My unit and contact details . T-04
│   ├── Agreement tracker .......... L-12            │   └── My receipts ................. T-05
│   ├── Unit register .............. L-08, L-09      │
│   ├── Tenant records ............. L-10, L-11      │
│   ├── Deposit & settlement ....... L-13            │
│   ├── Documents & exports ........ L-14            │
│   └── (Settings L-15; Sign in L-01; First-run L-02)│
└── Both sides read and write the same shared records
```

Sidebar order (UIUX A3): Dashboard, Rent, Maintenance, Units, Tenants, Agreements, Deposits, Documents; Settings and account at the bottom.

The dashboard is the only hub; every other landlord screen is also reachable from the sidebar (UIUX Screen map).

> OPEN: [OPEN-18] The IA shows **four** tenant pages. UIUX has **five** tenant screens (T-02 is the confirmation), and UIUX A3 says "the tenant's own **three** pages". Only T-01's route is specified, and no screen links to T-04 or T-05.

---

## 6. User journeys *(SCOPE §5, Diagram 1)*

Read left to right. "The app does" is what happens without anyone asking.

| Stage | Landlord does | Tenant does | The app does | Result | Screens |
|---|---|---|---|---|---|
| J1 Setting up | Adds properties and units. Enters rent, deposit and his UPI ID. | Not involved yet | Creates a link and a printable QR for every unit. | Everything is in one place. | L-02, L-08, L-15, P-03 |
| J2 Move-in | Adds the tenant, agreement dates, and photos of the flat's condition. | Gets a welcome message with their unit link. Saves it. Sees the QR too. | Stores the photos. Starts counting down to agreement expiry. | Both sides agree on the starting point. | L-09 (Add tenant), S-04, S-01, S-03 |
| J3 Every month | Glances at dues. Sends the drafted reminder. Marks payment received. | Taps the pay link, amount already filled. Receives a numbered receipt. | Creates the month's rent rows, drafts reminders, issues the receipt. | No chasing and no guessing. | L-03, L-04, L-05, S-01, S-02, P-01 |
| J4 Something breaks | Assigns a vendor, sends him the address, records what it cost. | Opens the link, reports the problem with a photo. Checks status later. | Sorts the request, keeps its status, files the cost against the unit. | No late-night calls. Nothing forgotten. | T-01, T-02, T-03, L-06, L-07 |
| J5 Renewal | Reviews what is expiring. Sends the renewal notice with new rent. | Confirms renewal, or gives notice. Knows the new rent in advance. | Warns at 90, 60 and 30 days. Works out the escalated rent. | No agreement ever lapses again. | L-03, L-12, S-01 |
| J6 Move-out | Notes deductions with a reason and a photo for each one. | Receives a written settlement showing every deduction and its photo. | Builds the statement from the deposit ledger and the repair history. | A calm settlement instead of a row. | L-11, L-13, P-02, S-01 |

> OPEN: [OPEN-10] J2 requires a tenant form (agreement dates, deposit, condition photos) and a welcome message carrying the unit link. UIUX only says "L09-BTN-ADDTENANT … Opens the tenant form". It defines no fields, no condition-photo upload point, and no welcome-message entry into S-01.

---

## 7. User flows *(SCOPE §9, Diagram 2)*

### 7.1 Tenant (no sign-in) — "three screens deep"
1. Opens the saved unit link → **T-01**
2. Reports a problem: category → description → photo → urgency → **T-02** (confirmation with a request number)
3. Returns to the same link later to check status (**T-03**) or find a receipt (**T-05**)
4. Also arrives by message (sent by the landlord via S-01): rent reminder with a payment link, receipt, and status updates.

### 7.2 Landlord (signs in)
Signs in (L-01) → **Portfolio dashboard (L-03)**, "what needs attention today", which routes to whichever board holds today's problem. Every board carries its own actions:

| Board | Actions in the flow |
|---|---|
| Rent due board (L-04) | Send reminder · Share payment link · Mark paid → receipt · Print or export |
| Maintenance board (L-06) | Assign a vendor · Send him the address · Record the cost · Update the tenant |
| Agreement tracker (L-12) | Send renewal notice · Add date to calendar · Settle a deposit · Print the statement |
| Units & tenants (L-08…L-11) | Add a unit or tenant · Upload condition photos · Share the unit link · Print the door QR |

Note: Diagram 2 groups "Settle a deposit / Print the statement" under the Agreement tracker. In UIUX these live on L-13, reached from the sidebar and from L11-BTN-ENDTENANCY.

---

## 8. System architecture *(SCOPE §13, Diagram 6)*

```
WHO USES IT        Landlord workspace (signed in, sees everything)   |   Tenant link (no sign-in, one unit only)
                                      │                                               │
THE PRODUCT        ┌──────────────┬───┴───────────────────┬───────────────────────────┘
                   │ The records  │ The rules and dates   │ The assistant
                   │ units, tenants, rent, requests,      │ monthly rent rows, due dates,   │ drafts reminders, sorts requests,
                   │ documents and photos                 │ expiry countdowns, escalation   │ writes settlement statements
HOW IT REACHES     The twelve connections (CX-01…CX-12): pay · QR · WhatsApp · email · call · maps · copy · share · calendar · print · unit QR · export
PEOPLE
APPS THEY          Payment apps (tenant's phone) | WhatsApp & phone | Email & calendar | Printer & files
ALREADY HAVE
```

Constraint: **nothing new to install, nothing to configure, no third-party account required by either user.** The connections hand off to apps people already have (details in [cross-cutting.md § Connections](cross-cutting.md#connections)).

Core services implied:

| Core part | Responsibilities | Detailed in |
|---|---|---|
| Records | Persist landlords, properties, units, tenants/tenancies, rent entries, reminders, requests, documents, photos | §9 below |
| Rules & dates | Create rent rows on the 1st; compute due / overdue / escalation level; agreement expiry countdowns (90/60/30); escalated-rent calculation | §10 below, L-04, L-12 |
| Assistant | Drafts reminders, suggests request category/urgency, writes settlement statements — never sends | [cross-cutting.md § Assistant](cross-cutting.md#assistant) |

---

## 9. Data model *(SCOPE §14 Diagram 7, §15 Diagram 8; attributes also drawn from UIUX screens)*

### 9.1 Entity relationship (Diagram 8, as drawn)

```
LANDLORD 1──* PROPERTY 1──* UNIT 1──* TENANT 1──* DOCUMENT
                             │  \
                             │   1──* REQUEST
                             1──* RENT ENTRY 1──* REMINDER
```

Rule: **a unit keeps its history when tenants change.** Rent entries, requests and photos stay with the unit, not the person.

> OPEN: [OPEN-13] The ERD draws the DOCUMENT relation from **TENANT**, while Diagram 8's caption says "Rent entries, requests and documents attach to the **unit**". DOCUMENT also has a "what it belongs to" attribute (polymorphic), which UIUX L-14 repeats.

### 9.2 Entities and attributes

Attributes marked **ERD** come from Diagram 8. Attributes marked **UI** are required by a screen in UIUX (cited) but missing from the ERD.

**LANDLORD**
| Attribute | Origin |
|---|---|
| name | ERD |
| phone, email | ERD |
| UPI ID (shape `name@handle`, not verified) | ERD; UI L02-FLD-UPI, L15-FLD-UPI |
| business name for receipts ("Name to show on receipts"; defaults to account name) | ERD; UI L02-FLD-BIZNAME, L15-FLD-RECEIPTNAME |
| logo (optional, print views) | UI L15-UPL-LOGO |
| default rent escalation % | UI L15-FLD-ESCDEFAULT |
| reminder ladder days (gentle/direct/formal; default 3/10/20) | UI L15-TBL-LADDER |
| accountant's email | UI L15-FLD-CAEMAIL |
| password (min 8 chars) | UI L-01 |

> OPEN: [OPEN-11] No screen collects the landlord's name or phone, yet T01-BTN-CALL, T04-BTN-CALL, T04-BTN-MESSAGE and P-03 all depend on the landlord's phone.

**PROPERTY**
| Attribute | Origin |
|---|---|
| name (e.g. "Kulkarni Apartments") | ERD; UI L02-FLD-PROPNAME |
| address (used by Maps links) | ERD; UI L02-FLD-PROPADDR |
| number of units | ERD; UI L02-FLD-UNITCOUNT |

> OPEN: [OPEN-09] Properties can only be created in L-02 (once). No screen creates or edits a second property, but L04-SEL-PROPERTY and L06-SEG-FILTER assume there can be several.

**UNIT**
| Attribute | Origin |
|---|---|
| unit number (unique within a property) | ERD; UI L-02 rule |
| type | ERD; UI L02-TBL-UNITS, L08-TBL-UNITS |
| rent (monthly) | ERD |
| deposit amount | ERD |
| occupied or vacant (UI also shows "Notice period") | ERD; UI L08-CHP-STATUS |
| its own reporting link (long random token) | ERD; UI T-01 |

> OPEN: [OPEN-35] Unit **type** values are never enumerated. PG/co-living operators (the target market) may need bed- or room-level units.

**TENANT** (functions as a *tenancy*: one row per person-in-unit period)
| Attribute | Origin |
|---|---|
| name, phone | ERD |
| email (optional) | UI L11-SEC-CONTACT, S01-BTN-EMAIL |
| agreement start, end | ERD |
| rent under the agreement | UI L11-SEC-AGREEMENT, L12-TBL-AGREEMENTS |
| deposit paid | ERD |
| deposit date received; agreement reference | UI L13-SEC-DEPOSIT |
| notice status | ERD; UI L10-SEG-FILTER (Current · On notice · Past) |

**RENT ENTRY** (one row per unit per month — "Rent ledger")
| Attribute | Origin |
|---|---|
| month | ERD |
| amount due, amount paid | ERD |
| due date, paid on | ERD |
| payment reference | ERD |
| receipt number (format `RR-0847`) | ERD; UI L-04 |
| pro-rata flag / edit history (old → new value on timeline) | UI L-04, L05-BTN-EDIT |

> OPEN: [OPEN-45] The ERD attaches rent entries only to UNIT. L-11 ("every rent entry for this tenant"), L09-TAB-RENT ("every tenant, ever") and T-05 need each entry attributed to a tenancy.

> OPEN: [OPEN-07] The ERD stores a single amount paid, paid-on and receipt number per entry. UIUX allows part payment ("a receipt is issued for the amount actually received"), which implies more than one payment and receipt per entry.

**REMINDER** (also stores logged calls)
| Attribute | Origin |
|---|---|
| level: gentle, direct, formal | ERD |
| sent on | ERD |
| how it was sent (WhatsApp, copy, email, call) | ERD; UI L05-TML-REMINDERS |
| call notes if phoned; call outcome (promised to pay / no answer / disputed / other) | ERD; UI L05-BTN-LOGCALL |

**REQUEST** (maintenance)
| Attribute | Origin |
|---|---|
| request number (format `R-0412`) | UI T-02 |
| category, description | ERD |
| urgency (Low · Normal · Urgent), status | ERD; UI T-01, L-06 |
| reporter name and phone; "reported by" (e.g. phone call) | UI T01-FLD-NAME/PHONE, L06-BTN-NEW |
| vendor assigned (name, phone) | ERD; UI L07-FLD-VENDOR |
| cost, or explicit "no cost"; tenant-liable flag | ERD; UI L07-FLD-COST, L-06 rules, L07-CHK-TENANTLIABLE |
| before and after photos | ERD; UI L07-GAL-PHOTOS |
| history timeline (status changes, messages sent, notes) | UI L07-TML-HISTORY |

**DOCUMENT**
| Attribute | Origin |
|---|---|
| type: agreement, ID proof, photo, receipt, statement | ERD |
| what it belongs to | ERD; UI L14-TBL-DOCS |
| uploaded on | UI L14-TBL-DOCS |

> OPEN: [OPEN-44] Several stores are implied by the screens but missing from the ERD: **Vendor** ("Maintenance requests and vendors" store; L07 "remembers previously used vendors"), **Deposit ledger and deductions** (Diagram 7; L13-TBL-DEDUCTIONS: description · reason · amount · photo), **Settlement statement** (read-only once settled; corrections reference the original), and **message/timeline events** for non-rent messages (vendor dispatch, tenant updates, renewal notices).

### 9.3 Data flow (Diagram 7)

| # | Process | Input from | Writes to |
|---|---|---|---|
| DF-1 | Record units, tenants and condition photos | Landlord | Units, properties and tenants; Photos, agreements and receipts |
| DF-2 | Receive and sort a reported problem | Tenant | Maintenance requests and vendors |
| DF-3 | Assign, resolve and record the cost | Vendor (via landlord) | Maintenance requests and vendors; Photos, agreements and receipts |
| DF-4 | Remind, receipt and settle | — (landlord-initiated) | Rent ledger (one row per unit per month); Reminder and call history; Deposit ledger and deductions |

Reminders, receipts and status updates go back out to the landlord and the tenant, always drawn from the same records.

---

## 10. Lifecycles and rules

### 10.1 Rent lifecycle *(SCOPE §10, Diagram 3; UIUX L-04, L-05, L-15, S-01)*

"The one rule set worth writing down precisely." **Every reminder is drafted by the app and sent by the landlord; the app never sends on its own.**

```
1st of the month ── a rent row is created per unit
        │
  Paid by the due date? ──Yes──▶ Landlord marks it paid; receipt is numbered, printed or sent
        │No
  Day 3 · gentle nudge (drafted, landlord reviews and sends)
        │
  Paid now? ──Yes──▶ Marked paid · receipt issued; reminder history is kept on the record
        │No
  Day 10 · direct reminder (states the amount and the date)
        │
  Paid now? ──Yes──▶ Marked paid · receipt issued; the month closes on the board
        │No
  Day 20 · formal notice (quotes the agreement clause)
        │
  Landlord calls the tenant; the call is logged on the record
```

| Rule ID | Rule | Source |
|---|---|---|
| RENT-1 | Rent rows are created on the 1st, one per unit with a tenant for that month. Vacant units do not appear for months in which they had no tenant. | SCOPE §10; UIUX L-04 |
| RENT-2 | If the 1st-of-month job did not run, L-04 shows the banner "This month's rent rows have not been created" with a button to create them now. | UIUX L-04, E1 |
| RENT-3 | Escalation ladder: **Gentle** at day 3, **Direct** at day 10, **Formal** at day 20. Days are editable in L-15; the three levels are fixed. | SCOPE §10, §11; UIUX L15-TBL-LADDER |
| RENT-4 | Tones: gentle / warm nudge (day 3); direct, states the amount and the date (day 10); formal, quotes the agreement clause (day 20). | SCOPE §10, §11 |
| RENT-5 | Reminder tone in S-01 is pre-selected by days overdue. | UIUX S01-SEG-TONE, L04-BTN-REMIND, L05-BTN-REMIND |
| RENT-6 | A reminder is recorded only when the landlord confirms "Yes" to "Did you send it?". | UIUX S-01 |
| RENT-7 | Marking paid is always a separate, deliberate landlord act. Nothing (including S-02) claims payment was received. No gateway in v1. | UIUX S-02; SCOPE §16 |
| RENT-8 | Mark paid → a receipt number is generated (`RR-####`) → toast with Undo. | UIUX L04-BTN-MARKPAID |
| RENT-9 | Part payment: the row shows "Part paid — ₹4,000 pending" and stays in the Pending filter; the receipt is for the amount actually received. | UIUX L-04 |
| RENT-10 | Mid-month move-in: the first month's row uses a pro-rata amount with a "pro-rata" note; the landlord can edit it before marking paid. Edits go on the timeline (old → new). | UIUX L-04, L05-BTN-EDIT |
| RENT-11 | Marking paid twice is impossible; the button is replaced the moment state changes. | UIUX L-04 |
| RENT-12 | Status display: Paid (success) · Due (neutral) · *n* days late (warning at 1–9, danger at 10+). | UIUX L04-CHP-STATUS, A1 |
| RENT-13 | Renewal rent changes take effect from the new start date; rows already generated for earlier months are not altered. | UIUX L-12 |
| RENT-14 | Whatever happens is written to the record, so the history is complete either way (reminders, calls, edits, payments). | SCOPE §10 |

> OPEN: [OPEN-05] The source never defines the **due date**: is it the 1st, or configurable per unit or agreement? Nor does it say whether ladder "day 3/10/20" means day of the month or days past the due date. S-01 and L-04 say the tone is chosen by "days overdue", while SCOPE §2 and §18 talk about "day three" versus "day twenty-five", which reads as day-of-month. It is also undefined which tone S-01 pre-selects when Remind is pressed before day 3 or on a row that is Due but not late.

> OPEN: [OPEN-29] The chip colour thresholds (1–9 warning, 10+ danger) and L-03's "10+ days" ordering are fixed numbers, but the ladder days are editable. Should the thresholds follow the ladder?

> OPEN: [OPEN-30] "Formal notice quotes the agreement clause", but no agreement clause text is stored anywhere; the agreement exists only as an uploaded file.

> OPEN: [OPEN-27] The pro-rata formula is unspecified, mid-month move-out is not covered, and it is unclear whether the "Outstanding" figure on L-03 includes arrears from earlier months.

### 10.2 Maintenance request lifecycle *(UIUX L-06, L-07, T-01, T-03)*

| Landlord status (L-06 columns) | Tenant-facing label (T03-CHP-STATUS) |
|---|---|
| New | Received |
| Assigned | Assigned |
| In progress | In progress |
| Done | Done |

| Rule ID | Rule | Source |
|---|---|---|
| REQ-1 | Created by the tenant on T-01, or by the landlord via L06-BTN-NEW ("reported by", default "phone call"). | UIUX T-01, L-06 |
| REQ-2 | On creation the assistant suggests category and urgency in the background; creation never waits on it. | UIUX T-01; SCOPE §11 |
| REQ-3 | Status changes by dragging between L-06 columns or via the L-07 header dropdown; each change writes a timeline entry and offers (via toast) to notify the tenant. Declining is allowed. | UIUX L-06, L-07 |
| REQ-4 | Moving to Done requires a cost figure or an explicit "no cost"; prompts to add an after photo; offers to notify the tenant. | UIUX L-06, L-07 |
| REQ-5 | A request can be reopened from Done; this writes a timeline entry and does not create a new request. | UIUX L-06 |
| REQ-6 | Cards in New older than 48 h get a warning-colour left border; older than 7 days, danger colour. Visual only, no notification. | UIUX L-06 |
| REQ-7 | If the tenant is liable, the cost can be requested via S-02 instead of being absorbed. | UIUX L07-CHK-TENANTLIABLE; SCOPE §12 CX-01 |
| REQ-8 | The tenant never sees vendor rate, cost, internal notes or other units. Tenant updates are built from status and category only. | UIUX L-07 |

> OPEN: [OPEN-14] L-03 uses "status is not **closed**", but no status is called "closed" (Done is the terminal status). T-01's category label is "Something else" while L-07's is "Other".

### 10.3 Tenancy and agreement lifecycle *(UIUX L-09, L-10, L-11, L-12, L-13; SCOPE §5)*

1. **Move-in:** landlord adds a tenant to a vacant unit (L09-BTN-ADDTENANT), with agreement dates and condition photos. *(See OPEN-10.)*
2. **Current:** agreement countdown shown when within 90 days (L11-SEC-AGREEMENT). Warnings at 90, 60 and 30 days (L-12 windows, L-03 attention items at ≤30 and ≤90).
3. **Renewal:** L12-BTN-NOTICE drafts a renewal notice (current rent, new rent = current × (1 + escalation %), effective date). L12-BTN-RENEW records the new start date, end date and rent.
4. **Expired, not renewed:** stays at the top of L-12 in danger colour ("Expired 14 days ago") until renewed or the tenancy is ended. Never hidden.
5. **On notice:** tenant status "On notice" (L-10) / unit status "Notice period" (L-08). *(How it is set is OPEN-12.)*
6. **End tenancy:** L11-BTN-ENDTENANCY → confirm → L-13 with this tenant selected.
7. **Settled:** L13-BTN-CLOSE → tenancy closes, unit becomes vacant, statement filed under documents and becomes read-only. The former tenant's link stops working (T-01, E4).

---

## 11. Scope *(SCOPE §16)*

### 11.1 Included in version one

| Area | What is included |
|---|---|
| Landlord workspace | All eight modules, with sign-in |
| Tenant pages | Report a problem, track it, see unit details and receipts — no sign-in |
| Money tracking | Rent recorded per unit per month, receipts issued and numbered, deposit ledger |
| Dates | Rent due dates and agreement expiry, with warnings at 90, 60 and 30 days |
| Photos and documents | Condition photos, repair photos, agreements, ID proofs |
| Assistant | Reminder drafting, request sorting, settlement statements |
| Connections | All twelve, available from day one |

Also out of v1 (UIUX A3): **global search** — filters on each board cover the need. And (UIUX E3): **anything expected to take over 10 seconds**; if a feature needs that long, it is scoped wrong.

### 11.2 Deliberately excluded (principles, not backlog)

| Excluded | Why |
|---|---|
| Automatic sending | Every message is approved by the landlord. A principle, not a limitation to be removed later. |
| Listing vacant units publicly | A different product with a different business model. |
| Tenant background or credit checks | Not meaningfully available to individual landlords in India. |
| Accounting software integration | A spreadsheet export serves the accountant and avoids a fragile dependency. |
| Society or apartment-complex management | Different buyer, different problem. |
| A separate tenant mobile app | The whole point is that the tenant installs nothing. |

### 11.3 Considered for later (once in real use)

| Possible addition | Why it is not in v1 |
|---|---|
| Collecting rent through a payment gateway, with the rent row updating on its own | Requires merchant registration; money settles a day later instead of instantly. Worth it for operators with many small payments; a step backwards for a landlord with fourteen flats. |
| Sending messages automatically over WhatsApp's business service | Requires business verification, a dedicated phone number, and approval of each message format. Adds a monthly cost that only makes sense across many landlords. |
| Automatic monthly rent reminders without review | Would break the approval principle. Revisit only if landlords in real use ask for it. |
| Separate access for a caretaker or assistant | Most landlords in this range work alone. Add it when a customer with staff asks. |

---

## 12. Outcomes *(SCOPE §17)*

| Today | With RentRoll — landlord | With RentRoll — tenant |
|---|---|---|
| Not sure who has paid this month | One screen, one glance, twelve green and two red | Gets a numbered receipt every time, without asking |
| Avoids sending the awkward reminder | The right words are already written for day three, ten and twenty | Receives a fair reminder early instead of an angry one late |
| Agreement lapses unnoticed | Warned at 90, 60 and 30 days, with the new rent already calculated | Knows well in advance what is changing and when |
| Repairs reported by phone at odd hours | Requests arrive in a list with photos, in order of urgency | Reports in two minutes with a photo and can check the status |
| Deposit argument at move-out | Move-in photos, every repair and every cost, held for years | Receives a written statement explaining each deduction |
| Accountant rebuilds the year from bank statements | One export, one file, done in March in a minute | Has receipts on hand for their own proof of rent |
| Everything lives in the landlord's head | Everything lives in one place, and can be handed over | Knows there is a record, which is most of the trust |

The one sentence: *the landlord stops carrying the business in his head, and the tenant stops wondering whether anyone heard them. Both come from the same thing — a shared, written record.*

---

## 13. Success metrics *(SCOPE §18)*

| ID | What we look at | Why it tells us the product is working | Data it needs |
|---|---|---|---|
| M-1 | Rent rows marked paid within the month | The core promise. If collection does not improve, nothing else matters. | Rent entry paid-on vs month |
| M-2 | Days from due date to payment | Should fall once reminders go out on day three instead of day twenty-five. | Rent entry due date, paid-on |
| M-3 | Requests raised through the tenant link rather than by phone | Shows tenants have accepted the link — the biggest adoption risk. | Request "reported by" (T-01 vs L06-BTN-NEW) |
| M-4 | Agreements renewed before expiry, not after | The clearest money-saving outcome; easy to demonstrate to a prospect. | Renewal recorded date vs agreement end |
| M-5 | Units with move-in photos attached | If low, the settlement feature is decorative. Watch from week one. | Condition photos per tenancy |
| M-6 | Landlords still signing in after three months | Whether the product replaced the diary or joined it. | Sign-in events |

> OPEN: [OPEN-47] No instrumentation or analytics requirement is specified for these metrics. M-6 needs sign-in events to be retained.
