# L-08 · Unit register

> Source: UIUX Part B L-08 (p.13); UIUX E2; SCOPE §6 (MOD-5), §12 (CX-11). Build phase 2 (with L-09; done when "units can be created, listed and opened; tokens generated").

## Meta

| | |
|---|---|
| Route | `/units` |
| Access | Signed in |
| Purpose | The list of everything owned, and the way in to a unit's full history. |
| Arrives from | Sidebar "Units"; L03-CRD-OCCUPANCY (filtered to vacant); L-03 "No data at all" state button |
| Leads to | L-09 (row click); P-03 (door QR cards) |

## Components and interactions

| ID | Type | Content · what happens |
|---|---|---|
| L08-TBL-UNITS | Data table | Columns: **Unit · Property · Type · Rent · Current tenant · Status**. Row click → **L-09**. |
| L08-CHP-STATUS | Status chip | **Occupied** (success) · **Vacant** (neutral) · **Notice period** (warning) |
| L08-BTN-ADDUNIT | Primary button | "Add unit" → **inline form**: property, unit number, type, rent, deposit |
| L08-BTN-PRINTQR | Secondary button | "Print door QR codes" → **P-03**, one card per **selected** unit |
| L08-CHK-SELECT | Checkbox | Row selection; enables **bulk QR printing** and **bulk export** |

## States

| State | Display |
|---|---|
| Loading | Table skeleton (E3) |
| Empty | **"Your properties and units live here."** Action: **Add your first unit** (E2-04) |

## Rules

- Unit numbers are unique within a property (L-02 rule; applies to the Add unit form too).
- Each new unit gets a long, random reporting token (T-01) and can be printed as a door QR (P-03).
- Rent and deposit use the money field (₹, no decimals).

## Open items

> OPEN: [OPEN-20] No vacant filter is defined, but L03-CRD-OCCUPANCY routes here "filtered to vacant units".

> OPEN: [OPEN-09] The Add unit form requires a property, but no screen creates a property after L-02. The empty state "Your properties and units live here." / "Add your first unit" assumes one exists. Unit edit, archive and delete are not defined, though A2's example confirm button is "Delete unit".

> OPEN: [OPEN-51] "Bulk export" from selection is not defined: which export, which format, and whether it relates to the L-14 exports. The behaviour of L08-BTN-PRINTQR with no rows selected is not defined.

> OPEN: [OPEN-35] Unit type values are not enumerated.

## Related

L-09, P-03, L-02, L-14.
