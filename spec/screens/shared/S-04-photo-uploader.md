# S-04 · Photo uploader

> Source: UIUX Part D "S-03 · Share and copy menu · S-04 · Photo uploader" (p.19); UIUX A2, E1, E3, E5. Build phase 3 (done when "a 6MB photo uploads in under 5 seconds on a normal connection").

## Meta

| | |
|---|---|
| Type | Form component |
| Used by | T01-UPL-PHOTO (tenant, max 3); L06-BTN-NEW form; L07-GAL-PHOTOS after photos; L13-TBL-DEDUCTIONS photo; L15-UPL-LOGO; condition photos (OPEN-37) |
| Purpose | Capture photo evidence quickly on a phone (PR-5 "Evidence, always"). |

## Components

| ID | Type | Content · what happens |
|---|---|---|
| S04-ZONE | Drop zone | **Tap to choose or take a photo**; **drag and drop on desktop**. **Camera opens directly on mobile.** |
| S04-THUMB | Thumbnail | Shows **immediately from the local file** while the upload runs, with a **progress ring**. **Tap to enlarge, X to remove.** |
| S04-ERR | Inline error | **"That file is too large"** or **"That file type is not supported"**, shown **on the thumbnail, not as a popup** |

## Rules

- Images are **compressed on the device before upload**. A **6MB** phone photo should leave as roughly **400KB**.
- Maximum **3 photos on tenant screens**, **10 on landlord screens**.
- Upload **continues if the user scrolls**.
- Submitting while an upload is in progress **waits for it**, with the submit button showing **"Uploading photo…"**.
- If a submission fails, the photo is kept (T-01 "Submission failed").
- Thumbnails carry meaningful alternative text, not the file name (E5).
- Performance target: a 6MB photo uploads in under 5 seconds on a normal connection (Part F).

## Open items

> OPEN: [OPEN-37] The maximum file size, accepted file types (HEIC?), and the target compression dimensions/quality are not specified. Upload locations for move-in condition photos, agreements and ID proofs are not defined on any screen. The logo uploader's constraints are not defined.

> OPEN: [OPEN-50] S04-ERR text appears on tenant screens. It avoids the banned words ("error", "invalid", "failed"), but the source does not say what happens next, as E1 requires ("always say what happens next").

## Related

T-01, L-06, L-07, L-09, L-13, L-15.
