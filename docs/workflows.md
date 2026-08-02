# Gmail X GPT 5.x Workflows

## Workflow 1: New Message Labeling

Use this when checking messages since the previous automation run.

1. Search new Inbox messages.
2. Inspect sender, subject, snippet, and available body context.
3. Apply existing labels.
4. Check Spam and apply `00_SPAM-Review-Red`.
5. Return label counts.

No deletion, moving, archiving, sending, or read-status changes.

## Workflow 2: Inbox Sender Ranking

Use this when the user asks:

> แยกผู้ส่งใน Inbox ระบุจำนวนอีเมล เรียงมากไปหาน้อย และใส่ลำดับ 1 ถึง N

Steps:

1. Search `in:inbox`.
2. Normalize sender by email address.
3. Count messages.
4. Sort descending.
5. Number from `1` to `N`.
6. Show the table.

## Workflow 3: Keep Selected Ranks And Trash The Rest

Use this when the user says:

> เก็บอีเมลในลำดับที่ X Y Z นอกนั้นให้ลบทิ้ง

Steps:

1. Create a ranked sender list.
2. Freeze the rank-to-sender mapping.
3. Show selected kept senders.
4. Move messages from non-kept senders to Trash only after authorization.
5. Verify Inbox after action.

Important:

- Moving to Trash is not permanent deletion.
- Do not recalculate rank after deletion starts.
- Do not delete messages outside Inbox.

## Workflow 4: Contract Review

Use this when the user asks to inspect contract-related emails.

Steps:

1. Search keywords in Inbox.
2. If needed, search Trash too.
3. Separate true contract/agreement items from noise.
4. Report location and attachment status.
5. Do not move or delete unless separately authorized.

