# agent-gog-use-policy.md (sample)

## Purpose
Define guardrails for any agent using `gog drive` so access is safe, auditable, and aligned with team best practices.

## Scope
- Applies to all automated actions against Google Drive via `gog`.
- This is a **soft‑policy** enforced by the agent (not by Google).

## Allowed Actions (default)
- `drive ls`, `drive search`, `drive get`, `drive url`, `drive download`
- `docs cat`, `docs export`, `docs get`
- `drive copy` **only** into approved folders (see below)

## Restricted Actions (require explicit human approval)
- `drive upload`
- `drive move`
- `drive rename`
- `drive share` / `drive unshare`
- `drive delete` (trash or permanent)
- `docs write`, `docs insert`, `docs update`, `docs edit`, `docs clear`

## Prohibited Actions (unless specifically authorized in writing)
- Permanent deletes (`drive delete --permanent`)
- Sharing “anyone with link”
- Editing files outside approved folders

## Approved Locations
- Shared drive(s): `<TEAM_SHARED_DRIVE_ID>`
- Folders:
  - `<FOLDER_ID_1>` (e.g., `/Projects/MDSC/Incoming`)
  - `<FOLDER_ID_2>` (e.g., `/Projects/MDSC/Processed`)

## Execution Requirements
- Every action must include: account, command, and target file/folder ID.
- Agent must log actions to a running notes doc or channel.

## Safety Checks (before write actions)
- Confirm target folder is on approved list.
- Confirm file permissions (no external sharing).
- Confirm operation is reversible (unless explicitly approved).

## Example Allowed Commands
```
gog drive search "MDSC requirements" --account <email>
gog docs cat <docId> --account <email>
gog drive copy <fileId> "Copy - MDSC" --parent <folderId>
```

## Example Restricted Command (requires approval)
```
gog drive delete <fileId>
```
