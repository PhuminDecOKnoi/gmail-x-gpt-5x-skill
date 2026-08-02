---
name: id01-skill-email-sender-cleanup
description: Gmail Inbox sender-ranking and cleanup sub-skill. Use when the user asks to group Inbox emails by sender, count messages, rank senders from highest to lowest, keep selected rank numbers, and move all other Inbox messages to Trash using a frozen ranked snapshot and explicit safety verification.
---

# ID01 Skill Email Sender Cleanup

## Mission

Turn the Prompt-AI workflow "Gmail Inbox Sender Cleanup By Ranked Sender" into a reusable sub-skill for safe Gmail cleanup.

Use this sub-skill for:

- listing Inbox senders by message count;
- ranking senders from `1` to `N`;
- keeping selected sender ranks;
- moving non-kept Inbox messages to Trash only when authorized;
- verifying the Inbox after cleanup.

## Trigger Phrases

Use this sub-skill when the user says or implies:

- "แยกผู้ส่งใน Inbox";
- "ระบุจำนวนอีเมล เรียงมากไปหาน้อย";
- "ใส่ลำดับ 1 ถึง N";
- "เก็บอีเมลในลำดับที่ X Y Z นอกนั้นลบ";
- "rank sender cleanup";
- "keep selected sender ranks".

## Source Boundary

Use only connected Gmail data:

- sender display name;
- sender email address;
- subject;
- snippet;
- labels;
- message IDs or thread IDs needed for safe execution.

Do not use external web search.

## Required Inputs

| Input | Required | Default |
|---|---|---|
| Gmail scope | Yes | `in:inbox` |
| Keep ranks | Required for cleanup only | Ask user if missing |
| Delete mode | Yes for cleanup | Move to Trash only |
| Confirmation | Required unless current instruction explicitly authorizes cleanup | Confirm frozen mapping before moving messages |

## Core Workflow

1. Search Gmail using `in:inbox` unless the user gives a narrower Inbox scope.
2. Normalize sender identity by sender email address first.
3. Count Inbox messages per sender.
4. Sort senders by count descending.
5. Assign rank numbers from `1` to `N`.
6. Display the ranked sender table.
7. If keep ranks are provided, freeze the rank-to-sender-to-message mapping before cleanup.
8. Show the keep mapping and estimated Trash scope.
9. Move only non-kept Inbox messages to Trash after authorization.
10. Re-scan Inbox and report verification counts.

## Safety Gates

- Never delete by display name alone.
- Never use rank numbers from a previous run unless the frozen snapshot is still available.
- Never permanently delete.
- Never archive, send, draft, unsubscribe, or mark read/unread during this workflow.
- Stop immediately if Gmail results are incomplete, paginated beyond tool limits, or any write action fails.

## Output Contract

Use Thai by default.

For ranking, return:

| ลำดับ | ผู้ส่ง | Email Address | จำนวนอีเมลใน Inbox | ตัวอย่างหัวเรื่อง |
|---:|---|---|---:|---|

For cleanup verification, return:

| รายการ | จำนวน |
|---|---:|
| ผู้ส่งก่อนลบ | X |
| ผู้ส่งที่เก็บไว้ | Y |
| ผู้ส่งที่ย้ายไป Trash | Z |
| อีเมลที่ย้ายไป Trash | N |
| อีเมลที่ยังอยู่ใน Inbox | M |

End with a safety statement confirming that no permanent deletion, archive, send, or read-status change occurred.

## References

- Read [references/sender-ranking-standard.md](references/sender-ranking-standard.md) when executing or revising the ranked sender algorithm.
- Use [examples/keep-ranks-run.md](examples/keep-ranks-run.md) for copy-paste run format.
- Keep the central prompt aligned with [../../prompts/gmail-ranked-sender-cleanup.prompt.md](../../prompts/gmail-ranked-sender-cleanup.prompt.md).
