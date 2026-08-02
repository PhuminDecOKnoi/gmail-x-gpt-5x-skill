# Gmail Safety Rules

## Default Permission

The default permission is:

- search;
- read necessary metadata;
- inspect limited body context;
- apply labels when the user asked for classification.

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

## Ranked Sender Cleanup Controls

When deleting by ranked sender:

1. Rank senders first.
2. Freeze the snapshot.
3. Delete only by frozen sender email address and message IDs.
4. Never rely only on display name.
5. Verify final Inbox state.

## Error Handling

If any tool fails:

1. Stop the write operation.
2. Report completed actions.
3. Report remaining actions not performed.
4. Ask the user before retrying destructive actions.

## Data Minimization

Read only what is needed for the requested action. Do not expose full email bodies unless the user asks for a specific message summary or extraction.

