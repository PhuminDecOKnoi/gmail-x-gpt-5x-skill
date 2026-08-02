# Example: Keep Selected Sender Ranks

## User Command

```text
/USE SUB-SKILL: id01-skill-email-sender-cleanup

แยกผู้ส่งใน Inbox ระบุจำนวนอีเมล เรียงมากไปหาน้อย และใส่ลำดับด้านหน้า 1 ถึง N
จากนั้นให้เก็บอีเมลในลำดับที่ 5, 12, 23, 29, 34, 42
นอกนั้นให้ย้ายไป Trash
```

## Expected Assistant Behavior

1. Search `in:inbox`.
2. Rank senders by Inbox message count.
3. Freeze the rank-to-sender-to-message mapping.
4. Show kept ranks and estimated Trash scope.
5. Move non-kept Inbox messages to Trash only when the current instruction authorizes it.
6. Re-scan Inbox and report verification counts.

## Required Final Summary

| รายการ | จำนวน |
|---|---:|
| ผู้ส่งก่อนลบ | X |
| ผู้ส่งที่เก็บไว้ | Y |
| ผู้ส่งที่ย้ายไป Trash | Z |
| อีเมลที่ย้ายไป Trash | N |
| อีเมลที่ยังอยู่ใน Inbox | M |

End with:

```text
ไม่มีการลบถาวร Archive ส่งอีเมล หรือเปลี่ยนสถานะอ่านครับ
```
