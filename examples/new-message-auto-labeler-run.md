# Example: New Message Auto Labeler

## User Command

```text
Check Gmail for new messages received since the previous run.
For new Inbox messages, classify them by sender, subject, snippet, and available body context.
Apply the existing Gmail labels as appropriate.
For messages Gmail places in SPAM, apply 00_SPAM-Review-Red.
Do not delete, archive, move, send, or mark messages read.
```

## Prompt To Use

```text
/USE PROMPT: prompts/gmail-new-message-auto-labeler.prompt.md

Previous run boundary: newer_than:1h
Inbox scope: in:inbox
Spam scope: in:spam
Allowed action: apply existing labels only
Output language: Thai
```

## Expected Summary

| Label | จำนวน |
|---|---:|
| `01_Work-GitHub` | X |
| `06_HR-Professional` | Y |
| `00_SPAM-Review-Red` | Z |

## Required Closing Statement

```text
ไม่มีการลบ ย้าย Archive ส่งอีเมล หรือเปลี่ยนสถานะอ่าน
```
