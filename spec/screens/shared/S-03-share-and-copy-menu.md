# S-03 · Share and copy menu

> Source: UIUX Part D "S-03 · Share and copy menu · S-04 · Photo uploader" (p.19); UIUX E1-03; SCOPE §12 (CX-07, CX-08). Build phase 5 ("Share and copy across all screens"; done when "desktop fallback verified; no broken share icons").

## Meta

| | |
|---|---|
| Type | Icon-button pair, reused everywhere something can be shared or copied |
| Used by | L09-BTN-COPYLINK, L09-BTN-SHARELINK, T02-BTN-SAVE, S01-BTN-COPY, S02-BTN-COPYLINK, contact-block copy buttons (L-05, L-11), document share (L-11, L-14) |
| Purpose | One consistent, reliable way to share or copy, with a desktop fallback. |

## Components

| ID | Type | Content · what happens |
|---|---|---|
| S03-BTN-SHARE | Icon button | Uses the **device share sheet** where available; **falls back to copy with a toast** on desktop. **Never shows a broken share icon.** |
| S03-BTN-COPY | Icon button | Copies, then the **icon changes to a tick for 2 seconds**. Must be called **directly from the click, never after an `await`**. |

## Rules

- Copy toast: **"Copied."** (E1-03, 2 seconds).
- Feature-detect share support before rendering. If unsupported, render the copy behaviour, never a dead icon.
- Icon buttons: 32×32 (48×48 on tenant screens), tooltip plus accessible label (A2, E5).
- The clipboard write must be inside the user-gesture handler, because browsers reject clipboard writes after an async gap.

## Related

L-09, L-11, L-14, T-02, S-01, S-02.
