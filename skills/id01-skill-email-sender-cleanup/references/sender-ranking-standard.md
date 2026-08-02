# Sender Ranking Standard

This reference defines the deterministic behavior for `id01-skill-email-sender-cleanup`.

## Ranking Algorithm

1. Search `in:inbox`.
2. Extract message ID, thread ID, sender display name, sender email address, subject, snippet, and labels.
3. Normalize the sender key by lowercase sender email address.
4. Count messages by normalized sender key.
5. Sort by message count descending.
6. If two senders have the same count, sort by sender email address ascending for stable ranking.
7. Assign rank numbers from `1` to `N`.

Do not merge two different email addresses only because the display name is similar.

## Frozen Snapshot Schema

Before cleanup, create an internal frozen mapping:

| Field | Meaning |
|---|---|
| `rank` | Stable rank for the current run |
| `sender_email` | Normalized sender email address |
| `sender_display_name` | Display name shown to the user |
| `message_ids` | Inbox message IDs controlled by the rank |
| `inbox_count` | Count before cleanup |
| `action` | `keep` or `move_to_trash` |

Use this snapshot for the whole cleanup. Do not recalculate ranks after the first move-to-Trash action.

## Action Matrix

| User intent | Allowed action |
|---|---|
| Rank senders only | Read and report only |
| Keep ranks but no delete authorization | Show keep mapping and ask confirmation |
| Keep ranks and current instruction clearly says delete the rest | Move non-kept Inbox messages to Trash |
| Permanent delete | Stop and require separate explicit confirmation |
| Archive instead of Trash | Stop and require separate explicit authorization |

## Pre-Cleanup Confirmation

Before moving messages to Trash, show:

| Rank | Sender | Email Address | Inbox Count | Action |
|---:|---|---|---:|---|

Then state:

- number of kept senders;
- number of senders that will move to Trash;
- estimated number of Inbox messages that will move to Trash;
- confirmation that messages outside Inbox are out of scope.

## Verification

After cleanup:

1. Re-scan `in:inbox`.
2. Confirm kept sender emails remain.
3. Confirm non-kept sender emails are absent from Inbox, or list exceptions.
4. Report total moved-to-Trash count.
5. Confirm no permanent deletion, archive, send, draft, unsubscribe, or read-status change occurred.

## Failure Handling

If any Gmail operation fails:

1. Stop immediately.
2. Report completed counts.
3. Report remaining unprocessed counts when known.
4. Do not retry destructive or state-changing actions without user confirmation.
