# Google Drive Best Practices Policy for GoG Agents

_Aligned to: **“Google Drive Best Practices with Julie McMurry”** (Gentle Intro to Google Drive 2026)_

## Purpose
Provide guardrails for agents using `gog` to interact with Google Drive, aligned with best‑practice guidance on ownership, sharing, and versioning.

## Core Principles (from the talk)
- **Use a work account** (avoid visitor access). Visitor sharing expires and creates permission ambiguity.
- **Prefer Shared Drives** over My Drive for collaborative work.
- **Share with teams, not individuals** (use Google Groups when possible).
- **Pre‑share by creating files inside the correct folder/drive** (avoid later moves).
- **Avoid copies**; use **shortcuts** for multi‑location visibility.
- **Use version history instead of file cloning**; deprecate with care instead of deleting.

## Policy Scope
- Applies to all automation/agents using `gog drive` and `gog docs` against Google Drive.
- Enforced at the agent/workflow level (not by Google).

## Allowed Actions (default)
- Read/list/search metadata: `drive ls`, `drive search`, `drive get`, `drive url`
- Download/export: `drive download`, `docs export`, `docs cat`
- Copy **only into approved shared drives/folders** (see below)

## Restricted Actions (require explicit human approval)
- `drive upload`, `drive move`, `drive rename`
- `drive share`, `drive unshare`
- `docs write`, `docs insert`, `docs update`, `docs edit`, `docs clear`
- Any creation of files **outside** approved shared drives/folders

## Prohibited Actions (unless explicitly approved in writing)
- Permanent deletes (`drive delete --permanent`)
- “Anyone with link” sharing
- Copying files to My Drive (except temporary personal scratch space)

## Sharing Rules
- Prefer **group-based** sharing (Google Groups) over individual emails.
- Avoid “visitor” access unless the owner approves a limited‑time guest.

## Location Rules (Ownership = Location)
- Create new files **inside** the target shared drive/folder.
- Avoid creating in My Drive and moving later.
- If a file must appear in multiple places, use **shortcuts**, not copies.

## Versioning Rules
- Use **version history** rather than creating “v2/v3” files.
- If a document is superseded, **deprecate** it (note the replacement) instead of deleting.

## Approved Locations
- Shared drive(s): `<TEAM_SHARED_DRIVE_ID>`
- Folders:
  - `<FOLDER_ID_1>` (e.g., `/Projects/MDSC/Incoming`)
  - `<FOLDER_ID_2>` (e.g., `/Projects/MDSC/Processed`)

## Required Logging
- Every write action must be logged with: account, command, target ID, and destination folder.

## Example Safe Commands
```
gog drive search "MDSC requirements" --account <email>
gog docs cat <docId> --account <email>
gog drive copy <fileId> "Copy - MDSC" --parent <folderId>
```

## Example Restricted Command (requires approval)
```
gog drive share <fileId> --email user@example.com --role writer
```
