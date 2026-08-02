# Gmail X GPT 5.x Workflows

This document defines standard Gmail workflows for this repository.

## Workflow Map

| Workflow | Trigger phrase | Write action allowed by default | Primary prompt |
|---|---|---|---|
| New Message Labeling | "check new messages", "ตรวจเมลใหม่" | Apply labels only | `prompts/gmail-new-message-auto-labeler.prompt.md` |
| Inbox Sender Ranking | "แยกผู้ส่งใน Inbox", "rank sender" | None | `prompts/gmail-ranked-sender-cleanup.prompt.md` |
| Keep Selected Ranks | "เก็บลำดับ X Y Z นอกนั้นลบ" | Move non-kept Inbox messages to Trash after authorization | `skills/id01-skill-email-sender-cleanup/SKILL.md` and `prompts/gmail-ranked-sender-cleanup.prompt.md` |
| Contract Review | "contract", "agreement", "สัญญา", "invoice" | None | `prompts/gmail-contract-review.prompt.md` |

## Workflow 1: New Message Labeling

Use this when checking messages since the previous automation run.

1. Search new Inbox messages.
2. Inspect sender, subject, snippet, and available body context.
3. Apply existing labels.
4. Check Spam and apply `00_SPAM-Review-Red`.
5. Return label counts.

No deletion, moving, archiving, sending, or read-status changes.

Expected output:

| Label | จำนวน |
|---|---:|
| `01_Work-GitHub` | X |
| `00_SPAM-Review-Red` | Y |

End with a safety statement confirming no delete, move, archive, send, or read-status change.

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

Output contract:

| ลำดับ | ผู้ส่ง | Email Address | จำนวนอีเมลใน Inbox | ตัวอย่างหัวเรื่อง |
|---:|---|---|---:|---|

Rules:

- Normalize by sender email address first.
- Do not merge senders only because display names are similar.
- Do not delete or move messages in this workflow.

## Workflow 3: Keep Selected Ranks And Trash The Rest

Use this when the user says:

> เก็บอีเมลในลำดับที่ X Y Z นอกนั้นให้ลบทิ้ง

Use sub-skill:

`skills/id01-skill-email-sender-cleanup/SKILL.md`

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
- Do not use rank numbers from a previous run unless a frozen snapshot is still available.

Verification output:

| รายการ | จำนวน |
|---|---:|
| ผู้ส่งก่อนลบ | X |
| ผู้ส่งที่เก็บไว้ | Y |
| ผู้ส่งที่ย้ายไป Trash | Z |
| อีเมลที่ย้ายไป Trash | N |
| อีเมลที่ยังอยู่ใน Inbox | M |

## Workflow 4: Contract Review

Use this when the user asks to inspect contract-related emails.

Steps:

1. Search keywords in Inbox.
2. If needed, search Trash too.
3. Separate true contract/agreement items from noise.
4. Report location and attachment status.
5. Do not move or delete unless separately authorized.

Recommended grouping:

| Group | Meaning |
|---|---|
| Likely Contract / Agreement | Contract, agreement, terms, service terms, consent record |
| Billing / Utility Contract Account | Utility or service account record |
| Receipt / Tax Invoice | Billing document, receipt, invoice, tax invoice |
| Noise | Keyword appears but not a true contract record |
| Uncertain | Needs manual review |
