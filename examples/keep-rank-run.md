# Example: Keep Selected Sender Ranks

## User Command

```text
แยกผู้ส่งใน Inbox ระบุจำนวนอีเมล เรียงมากไปหาน้อย และใส่ลำดับ 1-N
เก็บอีเมลในลำดับที่ 5 12 23 29 34 42 นอกนั้นให้ลบทิ้ง
```

## Expected AI Behavior

1. Search `in:inbox`.
2. Count messages by sender email address.
3. Sort descending.
4. Show ranked table.
5. Freeze mapping.
6. Confirm the kept sender ranks.
7. Move all other Inbox messages to Trash, only if authorized.
8. Verify Inbox.

## Example Keep Mapping

| Rank | Sender | Email | Action |
|---:|---|---|---|
| 5 | GitHub | `noreply@github.com` | Keep |
| 12 | CodeRabbit | `noreply@coderabbit.ai` | Keep |
| 23 | MEA e-bill | `ebill@mea.or.th` | Keep |

## Final Summary Template

| รายการ | จำนวน |
|---|---:|
| ผู้ส่งก่อนลบ | X |
| ผู้ส่งที่เก็บไว้ | Y |
| ผู้ส่งที่ย้ายไป Trash | Z |
| อีเมลที่ย้ายไป Trash | N |
| อีเมลที่ยังอยู่ใน Inbox | M |

