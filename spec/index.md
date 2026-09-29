# RentRoll — Specification index

This directory is the implementation specification for **RentRoll v1**. It is written so that several agents can build in parallel **without opening the original PDFs**. Start here, then read only the files your ticket touches.

## Source documents

| Tag | Document | Pages | MD5 |
|---|---|---|---|
| **[SCOPE]** | *RentRoll — Product Scope Document*, v1.0 ("scope, workflows and diagrams") | 17 | `7ea99aabc3a260b6d69e2b965af76a12` |
| **[UIUX]** | *RentRoll — UI/UX Specification*, v1.0 ("Screens, components and interactions") | 22 | `32196f2976fd6dc77bdd620e2e65a9e6` |

UIUX describes itself as "the build reference. Every screen, every component, every click", "companion to RentRoll Product Scope Document v1.0", and says to "treat as the source of truth for version one". **This spec does not use that sentence to settle conflicts silently.** Where SCOPE and UIUX disagree, the conflict is recorded as `OPEN` below, noting which way the source's own precedence points.

## How to use this spec

1. Read [cross-cutting.md](cross-cutting.md) **GR-1** and **GR-2** before touching anything. Any ticket that appears to breach either must be **escalated, not implemented** (GR-3).
2. Read [foundations.md](foundations.md) for tokens, components, navigation and responsive rules.
3. Read the screen file(s) for your ticket.
4. Check the screen file's **Open items**. An `> OPEN:` item is **unresolved**: build around it or ask. Never pick an interpretation silently.
5. Reference stable IDs (`L-04`, `L04-BTN-REMIND`, `GR-1`, `CX-03`, `E4-02`, `OPEN-07`) in commits, PRs, tickets and code comments.

Conventions:
- **Quoted text in bold** is exact UI copy: match it verbatim.
- IDs marked **`[+]`** were assigned by this spec for elements the source describes but does not name. All other IDs are verbatim from the source.
- `> OPEN: [OPEN-nn]` marks a contradiction or gap. The register below is authoritative; screen files repeat the relevant items in context.

## File map

| File | Contents |
|---|---|
| [product.md](product.md) | Product architecture: purpose, problem, principles (PR-1…6), users, modules (MOD-1…8), information architecture, journeys (J1–J6), user flows, system architecture, **data model** (ERD, entities, data flow), **lifecycles** (rent RENT-1…14, maintenance REQ-1…8, tenancy), scope (in / excluded / later), outcomes, success metrics (M-1…6) |
| [foundations.md](foundations.md) | A0 identifier scheme · A1 design tokens · A2 component library · A3 global navigation · A4 responsive rules |
| [cross-cutting.md](cross-cutting.md) | GR-1…4 global rules · assistant (AI-1…3) · the twelve connections (CX-01…12) · formats · E1 system messages · E2 empty states · E3 loading · E4 permission tests · E5 accessibility · print-view rules · interaction conventions |
| `screens/landlord/` | L-01 … L-15 |
| `screens/tenant/` | T-01 … T-05 |
| `screens/shared/` | S-01 … S-04 |
| `screens/print/` | P-01 … P-03 |

## Screen catalogue

15 landlord screens, 5 tenant screens, 4 shared components, 3 print views.

| ID | Name | Route | Build phase | File |
|---|---|---|---|---|
| L-01 | Sign in (+ sign up, reset) | `/signin`, `/signup`, `/reset` | 1 | [L-01](screens/landlord/L-01-sign-in.md) |
| L-02 | First-run setup | `/setup` | 2 | [L-02](screens/landlord/L-02-first-run-setup.md) |
| L-03 | Portfolio dashboard (the hub) | `/` | 6 | [L-03](screens/landlord/L-03-portfolio-dashboard.md) |
| L-04 | Rent due board | `/rent?month=YYYY-MM&status=…` | 4 | [L-04](screens/landlord/L-04-rent-due-board.md) |
| L-05 | Rent detail panel | `/rent/:entryId` (panel over L-04) | 4 | [L-05](screens/landlord/L-05-rent-detail-panel.md) |
| L-06 | Maintenance board | `/maintenance` | 3 | [L-06](screens/landlord/L-06-maintenance-board.md) |
| L-07 | Request detail panel | `/maintenance/:requestId` | 3 | [L-07](screens/landlord/L-07-request-detail-panel.md) |
| L-08 | Unit register | `/units` | 2 | [L-08](screens/landlord/L-08-unit-register.md) |
| L-09 | Unit detail (full page) | `/units/:unitId` | 2 | [L-09](screens/landlord/L-09-unit-detail.md) |
| L-10 | Tenant list | `/tenants` | 2 | [L-10](screens/landlord/L-10-tenant-list.md) |
| L-11 | Tenant detail | `/tenants/:tenantId` | 2 | [L-11](screens/landlord/L-11-tenant-detail.md) |
| L-12 | Agreement tracker | `/agreements` | 6 | [L-12](screens/landlord/L-12-agreement-tracker.md) |
| L-13 | Deposit and settlement | `/deposits`, `/deposits/:tenantId` | 7 | [L-13](screens/landlord/L-13-deposit-and-settlement.md) |
| L-14 | Documents and exports | *unspecified* (OPEN-39) | 7 | [L-14](screens/landlord/L-14-documents-and-exports.md) |
| L-15 | Settings | *unspecified* (OPEN-39) | 7 | [L-15](screens/landlord/L-15-settings.md) |
| T-01 | Report a problem (the entry point) | `/u/:unitToken` | 3 | [T-01](screens/tenant/T-01-report-a-problem.md) |
| T-02 | Submitted confirmation | *unspecified* (OPEN-18) | 3 | [T-02](screens/tenant/T-02-submitted-confirmation.md) |
| T-03 | My reports and their status | *unspecified* (OPEN-18) | 6 | [T-03](screens/tenant/T-03-my-reports.md) |
| T-04 | My unit and landlord contact | *unspecified* (OPEN-18) | 6 | [T-04](screens/tenant/T-04-my-unit.md) |
| T-05 | My receipts | *unspecified* (OPEN-18) | 6 | [T-05](screens/tenant/T-05-my-receipts.md) |
| S-01 | Message composer | modal | 5 | [S-01](screens/shared/S-01-message-composer.md) |
| S-02 | Payment sheet | sheet | 5 | [S-02](screens/shared/S-02-payment-sheet.md) |
| S-03 | Share and copy menu | component | 5 | [S-03](screens/shared/S-03-share-and-copy-menu.md) |
| S-04 | Photo uploader | component | 3 | [S-04](screens/shared/S-04-photo-uploader.md) |
| P-01 | Rent receipt | *unspecified* (OPEN-39) | 4 | [P-01](screens/print/P-01-rent-receipt.md) |
| P-02 | Settlement statement | *unspecified* (OPEN-39) | 7 | [P-02](screens/print/P-02-settlement-statement.md) |
| P-03 | Door QR card | *unspecified* (OPEN-39) | 7 | [P-03](screens/print/P-03-door-qr-card.md) |

## Build order *(UIUX Part F)*

Suggested order; each row is a ticket. The source claims "nothing in a later phase blocks anything in an earlier one" (but see OPEN-46).

| Phase | Ref | Ticket | Done when |
|---|---|---|---|
| 1 | A1, A2 | Design tokens and component library | Every component in A2 exists in isolation with all its states |
| 1 | A3, A4 | App shell, navigation, responsive rules | Sidebar, bottom bar and breakpoints behave as specified |
| 1 | L-01 | Sign in, sign up, password reset | All three flows, plus the five-attempt delay |
| 2 | L-08, L-09 | Unit register and unit detail | Units can be created, listed and opened; tokens generated |
| 2 | L-10, L-11 | Tenant list and detail | A tenant can be attached to a unit with agreement dates |
| 2 | L-02 | First-run setup | A new account reaches a populated dashboard without help |
| 3 | T-01, T-02 | Tenant report form and confirmation | A request submitted from a phone appears in the database |
| 3 | S-04 | Photo uploader with compression | A 6MB photo uploads in under 5 seconds on a normal connection |
| 3 | L-06, L-07 | Maintenance board and request detail | Full lifecycle from New to Done, with cost captured |
| 4 | L-04 | Rent due board | Rows generated monthly; filters, statuses and mark-paid all work |
| 4 | L-05 | Rent detail panel with reminder history | Timeline shows every reminder and logged call |
| 4 | P-01 | Rent receipt print view | Prints cleanly to A4 with the landlord's branding |
| 5 | S-01 | Message composer with the three tones | Draft arrives, is editable, and the send-confirmation step records correctly |
| 5 | S-02 | Payment sheet, link and QR | A phone opens the payment app with the right amount; desktop shows the QR |
| 5 | S-03 | Share and copy across all screens | Desktop fallback verified; no broken share icons |
| 6 | L-03 | Portfolio dashboard | All four cards route correctly; Needs attention sorted as specified |
| 6 | L-12 | Agreement tracker with calendar file | Countdowns correct; the calendar file opens in a real calendar app |
| 6 | T-03, T-04, T-05 | Tenant status, unit and receipt pages | Verified against every test in E4 |
| 7 | L-13, P-02 | Deposit settlement and its statement | Deductions pull from repair history with photos attached |
| 7 | L-14, L-15 | Exports, documents and settings | All four CSVs open correctly in Excel with the rupee symbol intact |
| 7 | P-03 | Door QR cards | Four to a page, scannable from print |
| 8 | E1–E3 | Message, empty and loading state pass | Every state in the tables above exists and matches the wording |
| 8 | E4 | Permission boundary testing | All seven tests pass |
| 8 | E5 | Accessibility pass | Keyboard-only run through every screen completes |

Note on order (from source): the tenant form is built in phase 3, before the rent board, deliberately. It is the screen most likely to be judged by a real user, it is the smallest, and having real requests in the system makes every later screen easier to build against.

---

<a id="open-items"></a>
## Open items

Contradictions and gaps found while converting the sources. **None is resolved in this spec.** Severity: **H** blocks the schema, security or a global rule; **M** blocks a screen's behaviour; **L** is copy, cosmetic or minor.

<a id="open-01"></a>

| ID | Sev | Summary | Conflict / gap (sources) | Affects |
|---|---|---|---|---|
| OPEN-01 | H | **Tenant link: per unit or per tenancy?** | UIUX T-01 "one unguessable token per unit"; ERD UNIT "its own reporting link" vs SCOPE §4 "every tenant gets their own unit link"; T-01/E4-02 "a former tenant's link stops working when the tenancy ends". Door QR stickers (P-03, CX-11) would need reprinting on every tenancy change if tokens rotate. | T-01, P-03, L-09, E4, schema |
| OPEN-02 | H | **Money on tenant-facing surfaces** | GR-2 (UIUX p.2), SCOPE §4 "no money", §8 "no path to any money screen", E4-04 "contains no rent amount" vs UIUX T-05 "receipts do show amounts" and P-01 opened from T-05. Unclear whether "tenant-facing" covers messages and prints the landlord sends (day-10 reminder states the amount; P-02 deductions incl. repair costs; tenant-liable payment request). | T-05, P-01, P-02, S-01, S-02, E4 |
| OPEN-03 | H | **Public QR placement exposes tenant data** | SCOPE CX-11 puts the unit QR "inside the flat door" and "on a notice board in the building"; anyone scanning gets T-01 pre-filled name and phone, T-03 reports, T-04 agreement dates, T-05 receipts. | T-01, T-03–T-05, P-03, security |
| OPEN-04 | M | **"Your landlord has been notified."** | T-02 claims a notification, but v1 has no notification channel (GR-1; L-06 "no notification, just a visual"; no email or push defined). | T-02, L-06 |
| OPEN-05 | H | **Rent due date and ladder reference point** | The due date is never defined (fixed 1st? per unit/agreement?). Ladder "day 3/10/20" may be day-of-month (SCOPE §2, §18 "day three … day twenty-five") or days overdue (UIUX S-01, L-04 "days overdue"). The tone for Remind before day 3 or on a Due row is undefined. | L-04, L-05, L-15, S-01, M-2, schema |
| OPEN-06 | L | **S-01 example level mismatch** | UIUX S01-CHP-CONTEXT "18 days overdue · Level 3 of 3" vs default ladder (day 20 = level 3; 18 days = Direct, level 2). Wireframe B "firm tone" is not one of the three levels. | S-01 |
| OPEN-07 | H | **Part payments data model** | UIUX L-04 part payment ("receipt for amount actually received", row stays Pending) vs ERD single amount paid / paid on / receipt number per entry, and "marking paid twice is impossible". How is the remainder paid and receipted? | L-04, L-05, P-01, schema |
| OPEN-08 | M | **Undo window and receipt numbering** | L-04 Undo "for 10 seconds" vs A2 toast "4 seconds". Receipt number fate on Undo (reused or burned); numbering scope (per landlord or global) and padding; same for `R-` request numbers. | L-04, P-01, T-02 |
| OPEN-09 | H | **No property/unit management after setup** | Properties are created only in L-02 (once), yet multi-property is assumed (L04-SEL-PROPERTY, L06 "This property", L08 add-unit "property" field). No edit, archive or delete for properties or units (A2's example "Delete unit"). | L-02, L-08, L-09 |
| OPEN-10 | H | **Tenant creation / move-in flow undefined** | L09-BTN-ADDTENANT "opens the tenant form" with no fields. SCOPE J2 needs agreement dates, deposit, condition photos, and a welcome message with the unit link (CX-03). Move-in date drives pro-rata. | L-09, L-10, L-13 (E2 "Add tenant"), S-01, schema |
| OPEN-11 | M | **Landlord profile and account** | ERD LANDLORD has name, phone, email; no screen collects name or phone (needed by T01-BTN-CALL, T-04, P-03). Sign-up fields undefined; "account" in the sidebar has no screen. | L-01, L-15, T-01, T-04, P-03 |
| OPEN-12 | M | **Notice status: how is it set?** | SCOPE MOD-7 "record a notice served" vs UIUX L-12 "Record renewal". Tenant "gives notice" (J5). L-10 "On notice" and L-08 "Notice period" are displayed, but no control sets them. | L-08, L-10, L-11, L-12 |
| OPEN-13 | M | **Document ownership** | ERD draws TENANT 1:* DOCUMENT; the Diagram 8 caption says documents attach to the **unit**; DOCUMENT has "what it belongs to" (polymorphic). | L-09, L-11, L-14, schema |
| OPEN-14 | L | **Request status and category vocab** | L-03 "status is not **closed**", but no Closed status exists (New/Assigned/In progress/Done); T-03 "Received" vs L-06 "New"; T-01 "Something else" vs L-07 "Other". | L-03, L-06, L-07, T-01, T-03 |
| OPEN-15 | M | **Assistant suggestion vs tenant choice** | T-01 "assistant assigns a suggested category and urgency"; L07-SEL-CATEGORY "pre-filled by the assistant". It is not said which value is stored or shown (e.g. tenant chose Urgent, assistant suggests Normal), or whether the original is kept. | T-01, L-06, L-07, L-03 order 1 |
| OPEN-16 | M | **Assistant scope** | SCOPE §11 "used in three places only" (reminders, request sorting, settlement) vs S-01, which requests a draft on every open, incl. vendor dispatch, tenant update and renewal notice. | S-01, L-07, L-12 |
| OPEN-17 | M | **T-03 "landlord's latest update"** | No tenant-visible update field exists. If it is the S-01 message text, free-form landlord edits could leak costs, contrary to "tenant-safe wording only". | T-03, L-07 |
| OPEN-18 | M | **Tenant routes and navigation** | Only T-01 has a route. Nothing links to T-04 or T-05. SCOPE IA: four tenant pages; UIUX: five tenant screens; A3: "the tenant's own **three** pages". | T-01–T-05, A3 |
| OPEN-19 | L | **Dashboard row click vs "Open"** | L03-ROW-ATTENTION "route to the relevant detail" vs row action "Open": "opens the relevant detail panel over the dashboard". L-12 has no panel. The action for agreement and open-request rows is unspecified. The URL of panels opened over L-03 is unspecified. | L-03, L-05, L-07 |
| OPEN-20 | L | **L-08 vacant filter** | L03-CRD-OCCUPANCY routes to "L-08 filtered to vacant units", but L-08 defines no filter. | L-03, L-08 |
| OPEN-21 | L | **L-02 skippability** | L-03 "No data at all … only reachable if L-02 was skipped" vs L-02 "every step can be skipped except the first". Step labels are not given. | L-02, L-03 |
| OPEN-22 | L | **Rent board shape** | SCOPE MOD-2 "a grid of month against unit", and Wireframe B's inline draft with Send / Pay link / Mark paid, vs UIUX L-04 single-month table + S-01 modal + S-02 sheet. UIUX's self-declared precedence favours L-04. | L-04 |
| OPEN-23 | L | **Counts and labels** | UIUX cover "14 landlord screens · 5 tenant · 6 shared components" vs screen map "fifteen … four shared … three print". SCOPE §16 "all eight modules, with sign-in" includes the tenant portal (MOD-3). Wireframe labels differ ("DUES" vs "Outstanding"; T-01 header), though wireframes are "not final wording". | index, L-03, T-01 |
| OPEN-24 | M | **Token contrast fails E5** | E5 requires 4.5:1 incl. chips on tints. Computed: `muted` text 3.49:1; warning chip 3.31:1; neutral chip 2.65:1; success chip 4.26:1 on canvas. | A1, E5, all chips |
| OPEN-25 | L | **Chip shape and urgency colour** | A2 status chip "rounded pill" vs A1 `radius-sm` 6px "buttons, inputs, chips". L06 urgency "Low (muted)" uses a text token as a status colour. | A1, A2, L-06 |
| OPEN-26 | L | **Detail-panel backdrop on desktop** | A2 "closes … on backdrop click" vs A4 >1024px "opens alongside rather than over content". | A2, A4, L-05, L-07 |
| OPEN-27 | M | **Pro-rata, move-out, arrears** | The pro-rata formula is unspecified; mid-month move-out is not covered; it is unclear whether L-03 "Outstanding" and rent attention rows include earlier months' arrears. | L-03, L-04, schema |
| OPEN-28 | L | **Pending vs Overdue filters** | Membership of L04 "Pending" and "Overdue" is undefined, especially for a part-paid row that is past due ("remains in the Pending filter"). | L-04 |
| OPEN-29 | L | **Fixed thresholds vs editable ladder** | The chip thresholds (1–9 warning / 10+ danger) and L-03 "10+ days" are fixed; the L15 ladder days are editable. | L-03, L-04, L-15 |
| OPEN-30 | L | **"Quotes the agreement clause"** | The day-20 formal notice quotes an agreement clause (SCOPE §10), but no clause text is stored; the agreement exists only as a file. | S-01, schema |
| OPEN-31 | M | **S-01 gaps** | No recipient selector (L-07 needs vendor vs tenant); tone segment for non-rent drafts?; does "Email instead" also confirm "Did you send it?"; is "the email composer" (L-11, L-14) S-01 or `mailto:`?; what is recorded for non-rent sends (E1-02 "tenant's history" vs L07 timeline); "Opened from" list omits L-06 and S-02; contact-block "message" buttons: S-01 or direct? | S-01, L-05, L-07, L-11, L-14 |
| OPEN-32 | L | **S-02 "works on the tenant's phone"** | S-02 is opened only from landlord screens; the intended user and device of S02-BTN-PAY are unclear. | S-02 |
| OPEN-33 | M | **Connection uses with no screen** | SCOPE §12 uses not placed in UIUX: deposit-at-move-in payment; late fee (undefined concept); sending receipts; welcome message; monthly statement to a "property owner"; prospective-tenant Maps; copy UPI ID / receipt number; share receipt or vacancy with a broker; calendar for notice end, vendor visit, rent due; "monthly statement" and "one-page agreement summary" prints; share unit link from tenant record (MOD-6). | cross-cutting CX, L-11, S-01, S-02 |
| OPEN-34 | L | **L-09 figure period** | L09-TAB-OVERVIEW "lifetime figures" vs the design note "earned ₹2.1 lakh and cost ₹34,000 **last year**". | L-09 |
| OPEN-35 | M | **Unit types** | Unit "type" is never enumerated; PG and co-living operators (target market) may need room- or bed-level units. | L-02, L-08, schema |
| OPEN-36 | L | **Sign-up and reset details** | No components for `/signup`, `/reset`; email verification; "trusted device" undefined; five-attempt counter scope (account or device); throttle copy. | L-01 |
| OPEN-37 | M | **Uploads: limits and locations** | S-04 max file size, types and compression target are not given. No upload control for move-in condition photos, agreements or ID proofs (L-09, L-11, L-14 list them). Logo constraints. | S-04, L-09, L-11, L-14, L-15 |
| OPEN-38 | L | **Request notes and cost details** | L07 timeline "note added", but no add-note control; drag-to-Done cost capture UX; whether a tenant-liable cost counts in maintenance spend (L-09, L-14 export). | L-06, L-07, L-09 |
| OPEN-39 | L | **Unspecified routes** | L-14, L-15, P-01, P-02, P-03. P-01 is also reachable by tenants (T-05) and needs token-scoped access. | L-14, L-15, P-01–P-03 |
| OPEN-40 | L | **Responsive details and typeface** | Which three columns per table at 640–1024px; which "key fields" on mobile cards; the typeface is not named. | A1, A4, all tables |
| OPEN-41 | L | **Agreement windows** | Chip boundary at exactly 30 / 60 days; chip for >90 days under "All"; whether expired agreements count in L03-CRD-EXPIRING; whether a renewed row leaves the list under "All"; whether L12-FLD-ESCALATION persists; rounding of suggested rent. | L-03, L-12 |
| OPEN-42 | L | **Settlement edge cases** | How a correction statement is created after the tenancy closed; whether refund paid out or amount owed is recorded; End tenancy with no deposit; where the AI-3 statement text appears (P-02, S-01, or both). | L-13, P-02 |
| OPEN-43 | M | **Locale and formats** | Indian vs international digit grouping; compact money ("2.1L", "36k", "₹2.1 lakh"); "amount in words" style; timezone for the 1st-of-month job and day counts; UI language(s); escalation % decimals; export column definitions; FY label vs date range. | A2, L-03, L-14, L-15, P-01 |
| OPEN-44 | M | **Entities implied but missing from ERD** | Vendor (store named in Diagram 7; L07 remembers vendors); deposit ledger and deductions; settlement statement (versions, references); message/timeline events for non-rent sends; deposit "date received" and "agreement reference". | schema, L-07, L-13 |
| OPEN-45 | H | **Rent entry ↔ tenancy link** | The ERD attaches rent entries to UNIT only, yet L-11 "every rent entry for this tenant", L09-TAB-RENT "every tenant, ever", and T-05 (current-tenancy scope?) need per-tenancy attribution. | L-09, L-11, T-05, schema |
| OPEN-46 | L | **Build-order dependencies** | "Nothing in a later phase blocks anything in an earlier one" vs L-04 Remind (phase 4) → S-01 (phase 5); L-11 End tenancy (phase 2) → L-13 (phase 7); L-02 (phase 2) → L-03 (phase 6). | Part F |
| OPEN-47 | L | **Metrics instrumentation** | SCOPE §18 metrics (M-1…M-6) have no instrumentation or retention requirement (e.g. sign-in events for M-6). | product |
| OPEN-48 | L | **Maintenance board ordering and property filter** | Card order within a column ("in order of urgency" vs L-03 "oldest first"); what "This property" refers to. | L-06 |
| OPEN-49 | L | **L-05 paid-state details** | The L05-BTN-MARKPAID form is not specified; button visibility once the entry is paid. | L-05 |
| OPEN-50 | L | **Copy inconsistencies** | T-01 offline text vs E1-08; rate-limit message copy missing; S04-ERR doesn't "say what happens next" (E1 rule). | T-01, S-04, E1 |
| OPEN-51 | L | **L-08 bulk actions** | "Bulk export" from selected rows is undefined; Print QR with no selection is undefined. | L-08 |
| OPEN-52 | L | **"Reported by" options** | L06-BTN-NEW "reported by" defaults to "phone call"; other values are not enumerated. | L-06, M-3 |
| OPEN-53 | L | **Call logging outside rent** | CX-05 "offers to log the call" for maintenance, vendor and tenant-record calls; only L-05 defines a log form and storage. | L-07, L-11 |
| OPEN-54 | L | **Missing defaults and empty states** | L-10 default filter and empty state; L-14 empty state. | L-10, L-14 |
| OPEN-55 | L | **UPI link format** | The UPI deep-link and QR payload parameters (payee, amount, note) are not specified. | S-02, P-01 |
| OPEN-56 | L | **QR on a receipt** | P-01 prints a "payment QR" on a receipt for a payment already made; what amount it encodes is unspecified. | P-01 |

---

## Source traceability

Every section of both source documents, and where it now lives.

### [SCOPE] Product Scope Document

| Source section | Spec home |
|---|---|
| Cover (product, purpose, built for, users) | [product.md §1](product.md#1-product-summary) |
| §1 Executive summary (four ideas) | product.md §1, §1.1 |
| §2 The problem we are solving | product.md §1.2 |
| §3 Product vision and design principles | product.md §2 (PR-1…6); cross-cutting.md GR-1, GR-2 |
| §4 Who uses the product | product.md §3 |
| §5 User journey map (Diagram 1) | product.md §6 (J1–J6) |
| §6 What the product does — eight modules | product.md §4 (MOD-1…8) |
| §7 Screen wireframes (Diagram 4) | L-03, L-04, T-01 (wireframe notes); OPEN-22, OPEN-23 |
| §8 Information architecture (Diagram 5) | product.md §5; foundations.md A3 |
| §9 User flow diagram (Diagram 2) | product.md §7 |
| §10 Rent lifecycle flowchart (Diagram 3) | product.md §10.1 (RENT-1…14); L-04, L-05, S-01 |
| §11 Where the assistant helps | cross-cutting.md § Assistant (AI-1…3) |
| §12 The twelve connections | cross-cutting.md § Connections (CX-01…12) |
| §13 System architecture (Diagram 6) | product.md §8 |
| §14 Data flow diagram (Diagram 7) | product.md §9.3 (DF-1…4) |
| §15 Entity relationship diagram (Diagram 8) | product.md §9.1–9.2; cross-cutting.md GR-4 |
| §16 Scope — included, excluded, later | product.md §11 |
| §17 How this makes life easier | product.md §12 |
| §18 How we will measure success | product.md §13 (M-1…6) |

### [UIUX] UI/UX Specification

| Source section | Spec home |
|---|---|
| Cover and "How to read this document" (ID scheme, section structure, two global rules) | foundations.md A0; cross-cutting.md GR-1…3; this index |
| A1 Design tokens | foundations.md A1 |
| A2 Component library | foundations.md A2 |
| A3 Global navigation | foundations.md A3 |
| A4 Responsive rules | foundations.md A4 |
| Screen map | this index § Screen catalogue; product.md §5 |
| Part B L-01 … L-15 | `screens/landlord/L-01…L-15` |
| Part C design brief, T-01 … T-05 | `screens/tenant/T-01…T-05` (brief in T-01) |
| Part D S-01 … S-04 | `screens/shared/S-01…S-04` |
| Part D Print views P-01 … P-03 (+ common print rules) | `screens/print/P-01…P-03`; cross-cutting.md § Print views |
| E1 Every message the system shows | cross-cutting.md E1 (E1-01…11) |
| E2 Empty states | cross-cutting.md E2 (E2-01…08) + each screen's States |
| E3 Loading | cross-cutting.md E3 |
| E4 Permissions — boundary tests | cross-cutting.md E4 (E4-01…07) |
| E5 Accessibility floor | cross-cutting.md E5 |
| Part F Build tracker (+ note on order) | this index § Build order |

Mechanical checks run at conversion time: every source element ID (`Lnn-…`, `Tnn-…`, `Snn-…`, `L14-BTN-EXPORT-*`), every screen ID, and every quoted UI string in [UIUX] appears somewhere under `spec/`.
