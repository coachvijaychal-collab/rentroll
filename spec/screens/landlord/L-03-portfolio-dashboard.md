# L-03 · Portfolio dashboard

> Source: UIUX Part B L-03 (p.8); SCOPE §6 (MOD-1), §7 Wireframe A, §9. Build phase 6 (done when "all four cards route correctly; Needs attention sorted as specified").

## Meta

| | |
|---|---|
| Route | `/` |
| Access | Signed in |
| Purpose | Answer one question in **five seconds**: *is anything wrong today?* Everything on this screen is either a number or a problem with a fix button next to it. |
| Arrives from | L-01, L-02, sidebar "Dashboard". The landlord always starts here (SCOPE §9). |
| Leads to | L-04, L-06, L-12, and directly into S-01 (also L-05, L-07, L-08 via cards/rows) |

## Layout

Top to bottom: **page header → four stat cards in a row → income chart → Needs attention list. Nothing else.** Resist adding a second chart.

On mobile (< 640px) the stat cards go two per row (A4).

## Components

| ID | Type | Content and behaviour |
|---|---|---|
| L03-CRD-OCCUPANCY | Stat card | Label "Occupied". Value "12 / 14". Sub-line "2 vacant". |
| L03-CRD-COLLECTED | Stat card | Label "Collected this month". Value in ₹. Sub-line compares to last month. |
| L03-CRD-DUES | Stat card | Label "Outstanding". Value in ₹, **danger** colour when above zero. Sub-line "across 2 units". |
| L03-CRD-EXPIRING | Stat card | Label "Agreements expiring". Value = count within 90 days. **Warning** colour when above zero. |
| L03-CHT-INCOME | Bar chart | Rent collected per month, last six months. Hover shows the exact figure. No legend, no axis clutter. |
| L03-LST-ATTENTION | List | Merged and sorted list of everything needing action; see *Needs attention* below. |
| L03-ROW-ATTENTION | List row | Icon · unit number · one-line description · status chip · one action button |
| L03-BTN-REMIND [+] | Quiet button (row action) | "Remind" on rent rows |
| L03-BTN-OPEN [+] | Quiet button (row action) | "Open" |

The whole stat card is the click target, not just the number (A2).

## Interactions

| Trigger | Result |
|---|---|
| L03-CRD-DUES | Route to **L-04** with the **Overdue** filter already applied (`/rent?status=overdue`) |
| L03-CRD-EXPIRING | Route to **L-12** with the **90-day** filter applied |
| L03-CRD-OCCUPANCY | Route to **L-08** filtered to **vacant** units |
| L03-CRD-COLLECTED | Route to **L-04** for the current month, no filter |
| L03-ROW-ATTENTION | Route to the relevant detail: rent rows → **L-05**, requests → **L-07**, agreements → **L-12** |
| Row action "Remind" (L03-BTN-REMIND [+]) | Opens **S-01** directly, without navigating away. Closing S-01 returns to the dashboard with the row refreshed. |
| Row action "Open" (L03-BTN-OPEN [+]) | Opens the relevant detail panel **over the dashboard** |

## Needs attention: what appears and in what order

| Order | Item | Condition |
|---|---|---|
| 1 | Urgent maintenance request | Urgency = urgent and status is not closed |
| 2 | Rent overdue 10+ days | Unpaid and past due by 10 or more days |
| 3 | Agreement expiring within 30 days | Agreement end date − today ≤ 30 |
| 4 | Rent overdue 1–9 days | Unpaid and past due |
| 5 | Open maintenance request | Any other open request, **oldest first** |
| 6 | Agreement expiring within 90 days | Agreement end date − today ≤ 90 |

Interpretation note: the conditions overlap (an item matching order 2 also matches order 4; one matching order 3 also matches order 6). Each item appears once, in its highest-priority group; the group labels ("1–9 days", "any **other** open request") imply this.

Wireframe A (SCOPE §7) examples: "4C · rent 18 days overdue — Remind", "3B · agreement ends in 22 days", "1B · geyser leaking, urgent — Open", "2A · rent 5 days overdue — Remind".

## States

| State | Display |
|---|---|
| Loading | Skeleton shapes in place of the four cards and six list rows. **Never a full-page spinner.** |
| Nothing wrong | The Needs attention card shows **"Nothing needs your attention today."** with a tick icon. A deliberate **reward** state, not an empty state. |
| No data at all | Only reachable if L-02 was skipped. Shows **"Add your first property to see your dashboard"** with a button to **L-08**. |
| Load failure | Card-level: each card shows a retry link. One failed card does not blank the page. |

## Open items

> OPEN: [OPEN-19] Row click "routes" to L-05/L-07/L-12, while the "Open" action "opens the relevant detail panel **over the dashboard**". These two behaviours differ, and L-12 has no detail panel. Each row has "one action button", but Wireframe A shows no action on the agreement row, and the action for agreement and open-request rows is unspecified. The URL while a panel is open over L-03 is also unspecified.

> OPEN: [OPEN-20] L-08 defines no vacant filter, but L03-CRD-OCCUPANCY routes there "filtered to vacant units".

> OPEN: [OPEN-14] "Status is not closed": there is no "closed" status (L-06 uses New · Assigned · In progress · Done). "Open request" presumably means any status other than Done.

> OPEN: [OPEN-41] It is unspecified whether already-expired agreements count in L03-CRD-EXPIRING and in attention order 3. They satisfy "end date − today ≤ 30" literally.

> OPEN: [OPEN-27] It is unspecified whether "Outstanding" and the rent attention rows cover only the current month or all unpaid months (arrears).

> OPEN: [OPEN-23] Wireframe A labels the card "DUES" and shows compact values ("2.1L", "36k"); UIUX labels it "Outstanding". The compact money format is not specified (OPEN-43). Wireframes are "arrangement and priority only — not colour, styling or final wording", so the UIUX labels are the ones used here.

## Related

L-04, L-05, L-06, L-07, L-08, L-12, S-01, [product §10](../../product.md#10-lifecycles-and-rules).
