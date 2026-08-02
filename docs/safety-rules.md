# Gmail Safety Rules

## Default Permission

The default permission is:

- search;
- read necessary metadata;
- inspect limited body context;
- apply labels when the user asked for classification.

Default permission does not include deleting, archiving, moving, sending, drafting, marking read/unread, unsubscribing, or changing Gmail settings.

## Actions Requiring Explicit Authorization

These actions require explicit user authorization in the current conversation:

| Action | Requirement |
|---|---|
| Move to Trash | User must clearly authorize deletion or Trash movement |
| Permanent delete | Requires separate explicit confirmation |
| Archive | Requires explicit authorization |
| Move out of Inbox | Requires explicit authorization |
| Send, reply, forward | Requires explicit authorization |
| Draft email | Requires explicit authorization |
| Mark read or unread | Requires explicit authorization |
| Unsubscribe | Requires explicit authorization |
| Change filters/settings/signature | Requires tool support and explicit authorization |

## Authorization Standard

Authorization must be current, specific, and tied to the action.

| Weak instruction | Required handling |
|---|---|
| "ดูให้หน่อย" | Search or summarize only |
| "จัดการให้หน่อย" | Ask what action is authorized before state-changing actions |
| "ลบทิ้ง" | Treat as move to Trash unless permanent delete is explicitly stated |
| "ลบถาวร" | Ask for separate confirmation before permanent deletion |

## Ranked Sender Cleanup Controls

When deleting by ranked sender:

1. Rank senders first.
2. Freeze the snapshot.
3. Delete only by frozen sender email address and message IDs.
4. Never rely only on display name.
5. Verify final Inbox state.

The frozen snapshot must contain:

| Field | Purpose |
|---|---|
| Rank | User-facing selection number |
| Sender email address | Stable sender identity |
| Sender display name | Human-readable review |
| Message IDs or thread IDs | Safe execution target |
| Message count | Verification baseline |

## Error Handling

If any tool fails:

1. Stop the write operation.
2. Report completed actions.
3. Report remaining actions not performed.
4. Ask the user before retrying destructive actions.

## Data Minimization

Read only what is needed for the requested action. Do not expose full email bodies unless the user asks for a specific message summary or extraction.

## Final Safety Statement

After any Gmail operation, state whether any of these occurred:

- delete or move to Trash;
- archive or move out of Inbox;
- send, reply, forward, or draft;
- mark read or unread;
- label application;
- settings or filter change.
