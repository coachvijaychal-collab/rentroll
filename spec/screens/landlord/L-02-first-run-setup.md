# L-02 · First-run setup

> Source: UIUX Part B L-02 (p.6–7); SCOPE §5 (J1 Setting up). Build phase 2 (done when "a new account reaches a populated dashboard without help").

## Meta

| | |
|---|---|
| Route | `/setup` |
| Access | Signed in, and **only while the account has no property**. Cannot be revisited afterwards. |
| Purpose | Get one property, one unit and the landlord's payment details in, so the dashboard is not empty on first sight. |
| Arrives from | L-01 (first sign-in, no properties) |
| Leads to | **L-03** |

## Layout

Three steps on **one scrolling page**, not a wizard with hidden steps. A progress line at the top shows all three at once. **Every step can be skipped except the first.**

Step grouping (inferred from the components; the source does not label the steps):

| Step [+] | Components | Skippable |
|---|---|---|
| 1 · Property | L02-FLD-PROPNAME, L02-FLD-PROPADDR, L02-FLD-UNITCOUNT | No |
| 2 · Units | L02-TBL-UNITS | Yes |
| 3 · Payment details | L02-FLD-UPI, L02-FLD-BIZNAME | Yes |

## Components

| ID | Type | Content and behaviour |
|---|---|---|
| L02-FLD-PROPNAME | Text field | "Property name", e.g. Kulkarni Apartments. **Required.** |
| L02-FLD-PROPADDR | Text area | "Address". **Required.** Used later by the Maps link (L09-BTN-MAP, vendor dispatch). |
| L02-FLD-UNITCOUNT | Text field | "How many units?" Numeric. Generates that many blank unit rows in L02-TBL-UNITS. |
| L02-TBL-UNITS | Editable table | Columns: unit number, type, monthly rent (money field), deposit (money field). Add row and remove row available. |
| L02-FLD-UPI | Text field | "Your UPI ID". Helper text: "This appears on payment links and QR codes sent to tenants." |
| L02-FLD-BIZNAME | Text field | "Name to show on receipts". Defaults to the account name. |
| L02-BTN-FINISH | Primary button | "Go to my dashboard" → L-03 |

## Rules

- Unit numbers must be **unique within a property**. Duplicates show an inline error on the offending row only.
- The UPI ID is validated for **shape** (`name@handle`) but **not verified**. Helper text says it can be added later.
- Skipping the UPI step is allowed. Payment features then show a **prompt to add it** rather than being hidden (see S-02, L-15).
- Each unit created here gets its own long, random reporting token and a printable QR (SCOPE J1, "Creates a link and a printable QR for every unit"; UIUX Part F phase 2, "tokens generated").
- Values saved here are the same values edited later in L-15 (UPI ID, receipt name).

## Open items

> OPEN: [OPEN-21] L-03's "No data at all" state is "only reachable if L-02 was skipped", yet here the first step cannot be skipped. The source does not say whether the whole of L-02 can be skipped or abandoned, or where a signed-in user with no property lands if they leave `/setup`. The step labels above are inferred. If the Units step is skipped, the "one unit" in PURPOSE is not guaranteed.

> OPEN: [OPEN-35] Allowed values for unit **type** are not defined.

> OPEN: [OPEN-09] L-02 is the only place a property is created in the whole spec.

## Related

L-03, L-08, L-15, S-02, P-03.
