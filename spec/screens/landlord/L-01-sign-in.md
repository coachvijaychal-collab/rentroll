# L-01 · Sign in

> Source: UIUX Part B L-01 (p.6); UIUX E4; SCOPE §4. Build phase 1 ("Sign in, sign up, password reset" — done when all three flows work, plus the five-attempt delay).

## Meta

| | |
|---|---|
| Route | `/signin`, also `/signup` and `/reset` |
| Access | Public. A signed-in user hitting this route is redirected to **L-03**. |
| Purpose | Get the landlord in with the least friction. This screen is **not a marketing page**. |
| Arrives from | Direct visit; any landlord route while signed out (E4-06) |
| Leads to | **L-02** if no properties exist yet, otherwise **L-03**; after a redirect (E4-06), the originally intended screen |

## Components

| ID | Type | Content and behaviour |
|---|---|---|
| L01-FLD-EMAIL | Text field | Label "Email". Autofocus **on desktop only**. |
| L01-FLD-PASS | Text field | Label "Password". Show/hide toggle on the right. |
| L01-BTN-SIGNIN | Primary button | "Sign in". Full width. |
| L01-LNK-RESET | Link | "Forgot password" |
| L01-LNK-SIGNUP | Link | "Create an account" |

## Interactions

| Trigger | Result |
|---|---|
| L01-BTN-SIGNIN | Validate both fields are filled → button shows spinner → on success route to L-02 or L-03 → on failure show a **single** inline error above the form: **"Email or password is incorrect."** Never say which one is wrong. |
| Enter key in either field | Same as pressing L01-BTN-SIGNIN |
| L01-LNK-RESET | Route to `/reset`. Sending a reset always shows the **same confirmation whether or not the email exists**. |
| L01-LNK-SIGNUP | Route to `/signup` |

## States

| State | Display |
|---|---|
| Submitting | Spinner inside L01-BTN-SIGNIN; button non-interactive (A2) |
| Wrong credentials | "Email or password is incorrect." inline above the form |
| Throttled | After five failed attempts: a 30-second delay, explained plainly on screen |

## Rules

- Password minimum **8 characters** on sign-up, with strength shown as a **single word, not a bar**.
- After **five failed attempts**, add a **30-second delay** and say so plainly.
- Session persists for **30 days on a trusted device**.
- Sign-in method is email and password only (SCOPE §4).

## Open items

> OPEN: [OPEN-36] The source gives no components for `/signup` or `/reset`: which fields sign-up collects (name? phone?, see OPEN-11), whether the email is verified, what the reset confirmation says, and how the new password is set. It does not define a "trusted device", whether the five-attempt counter is per account or per device, or the exact throttle wording.

## Related

E4-06 (redirect and return), L-02, L-03, [foundations A2](../../foundations.md#a2--component-library).
