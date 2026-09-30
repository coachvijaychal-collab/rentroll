# L-12 · Agreement tracker

> Source: UIUX Part B L-12 (p.14); UIUX E1, E2; SCOPE §5 (J5), §6 (MOD-7), §12 (CX-09). Build phase 6 (done when "countdowns correct; the calendar file opens in a real calendar app").

## Meta

| | |
|---|---|
| Route | `/agreements` (window in the URL, e.g. 90-day filter from L-03) |
| Access | Signed in |
| Purpose | Make sure nothing expires unnoticed. **The highest-value screen in the product**, and almost entirely a sorted list. |
| Arrives from | Sidebar "Agreements"; L03-CRD-EXPIRING (90-day filter); L03-ROW-ATTENTION (agreement rows) |
| Leads to | S-01 (renewal notice); calendar file download |

## Components

| ID | Type | Content and behaviour |
|---|---|---|
| L12-STRIP-TOTAL | Summary strip | e.g. **"3 agreements ending in the next 90 days · ₹54,000 monthly rent at stake"** |
| L12-SEG-WINDOW | Segmented choice | **30 days · 60 days · 90 days · All**. Default **90**. |
| L12-TBL-AGREEMENTS | Data table | **Unit · Tenant · Ends on · Days remaining · Current rent · Suggested new rent · Actions**. Sorted by **days remaining, ascending**. |
| L12-CHP-COUNTDOWN | Status chip | Under 30 days **danger** · 30–60 **warning** · 60–90 **neutral**. Expired: danger, "Expired 14 days ago". |
| L12-FLD-ESCALATION | Inline field | Percentage; defaults to the value in settings (L15-FLD-ESCDEFAULT). Changing it **recalculates the suggested rent in the same row, live**. |
| L12-BTN-NOTICE | Quiet button | "Send renewal notice" |
| L12-BTN-CALENDAR | Icon button | "Add to calendar" |
| L12-BTN-RENEW | Quiet button | "Record renewal" |
| L12-FRM-RENEW [+] | Inline form | New start date · new end date · new rent |

Suggested new rent = current rent × (1 + escalation % ÷ 100).

## Interactions

| Trigger | Result |
|---|---|
| L12-BTN-NOTICE | Opens **S-01** with a renewal draft containing the **current rent**, the **new rent**, and the **effective date** |
| L12-BTN-CALENDAR | **Downloads a calendar file** containing the expiry date with a **reminder 30 days before**. Toast: **"Added — open the file to save it to your calendar."** (E1-05) |
| L12-BTN-RENEW | Inline form (L12-FRM-RENEW [+]): new start date, new end date, new rent. On save the agreement dates update, **the row leaves the list**, and **future rent rows use the new amount**. |
| L12-FLD-ESCALATION (edit) | Live recalculation of Suggested new rent in that row |
| L12-SEG-WINDOW | Filters rows by days remaining |

## States

| State | Display |
|---|---|
| Loading | Table skeleton (E3) |
| Empty | **"Nothing expiring in the next 90 days."** Action: **Switch to All** (E2-05) |

## Rules

- An agreement that has **already expired** appears **at the top** in danger colour with **"Expired 14 days ago"** and stays there until renewed or the tenancy is ended. **It is never hidden.**
- Rent changes take effect from the **new start date**. Rows already generated for earlier months are **not altered**.
- Warnings at 90, 60 and 30 days (SCOPE J5) show up as the window options and countdown chip colours here, and as L-03 attention items (≤ 30, ≤ 90). There are no notifications (GR-1).

## Open items

> OPEN: [OPEN-12] SCOPE MOD-7 says "record a notice served"; UIUX provides "Record renewal" instead. There is no control for recording a notice (served by the landlord, or given by the tenant, "Confirms renewal, or gives notice", SCOPE J5).

> OPEN: [OPEN-41] Chip boundaries overlap: is exactly 30 or exactly 60 days danger/warning or warning/neutral? Chip colour for rows beyond 90 days under **All** is undefined. Under **All**, does a renewed row really "leave the list"? Is L12-FLD-ESCALATION persisted per agreement or only for the session? The rounding of suggested rent is undefined.

> OPEN: [OPEN-33] Calendar entries for the notice-period end, vendor visits and rent due dates (SCOPE CX-09) have no control.

> OPEN: [OPEN-16] Whether the renewal draft comes from the assistant (SCOPE says the assistant is used in three places only, not including renewals) or from a template.

## Related

L-03, L-11, L-15, S-01, [product §10.3](../../product.md#103-tenancy-and-agreement-lifecycle-uiux-l-09-l-10-l-11-l-12-l-13-scope-5).
