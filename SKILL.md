---
name: gmail-x-gpt-5x-skill
description: Gmail triage and cleanup skill for GPT 5.x. Use for classifying Inbox messages, applying Gmail labels, checking Spam, reviewing contract-related messages, and safely cleaning Inbox by ranked sender. Prioritizes non-destructive operations unless explicit user authorization is given.
version: 1.0.0
---

# Gmail X GPT 5.x SKILL

## Mission

Help the user manage Gmail with GPT 5.x using a professional, auditable, and safe workflow.

This skill supports:

- Inbox classification and labeling.
- New-message labeling.
- Gmail Spam review labeling.
- Sender ranking by Inbox count.
- Safe cleanup by keeping selected sender ranks and moving other Inbox messages to Trash.
- Contract, agreement, invoice, and service-term review.

## Safety Boundary

Default actions are read-only plus label application.

Do not perform any of these actions unless the user explicitly authorizes the exact action:

- delete or move to Trash;
- permanent delete;
- archive;
- move between folders or labels in a way that removes Inbox;
- send, reply, forward, or draft an email;
- mark read or unread;
- modify filters or account settings;
- unsubscribe.

Permanent deletion is outside the default scope and requires separate explicit confirmation.

## Standard Labels

Use the label taxonomy in [docs/label-taxonomy.md](docs/label-taxonomy.md).

If a message matches more than one label, apply all relevant specific labels. Avoid `99_Archive-LowPriority` when a more specific label fits.

For Gmail Spam, apply:

`00_SPAM-Review-Red`

The tool may not be able to set the visual label color. If so, create or apply the label name only and tell the user that Gmail UI must be used for visual color settings.

## Workflow A: New Inbox Labeling

Use when the user asks to check new messages since the previous run.

1. Search for new Inbox messages using the best available previous-run boundary.
2. If no durable previous-run state exists, use a conservative recent window such as `newer_than:1h`.
3. For each new message, inspect sender, subject, snippet, labels, and available body context.
4. Apply existing labels according to taxonomy.
5. Check Gmail Spam separately and apply `00_SPAM-Review-Red` to Spam messages.
6. Do not delete, archive, move, send, or mark read.
7. Return a summary table by label count.

## Workflow B: Inbox Sender Ranking

Use when the user asks to list senders in Inbox and count messages.

1. Search Gmail scope `in:inbox`.
2. Normalize sender identity primarily by email address.
3. Count Inbox messages per sender.
4. Sort senders by count descending.
5. Assign rank numbers from `1` to `N`.
6. Return a table with rank, sender name, sender email, message count, and sample subjects.

## Workflow C: Cleanup By Kept Sender Ranks

Use when the user says to keep ranks such as `X Y Z` and delete the rest.

1. Run Workflow B.
2. Freeze a ranked snapshot:
   - rank;
   - sender email address;
   - sender display name;
   - message IDs in Inbox.
3. Show the frozen keep mapping.
4. Confirm deletion scope unless the user's current instruction explicitly authorizes moving all non-kept Inbox messages to Trash.
5. Move only non-kept Inbox messages to Trash.
6. Do not permanently delete.
7. Re-scan Inbox and verify that only kept senders remain or explain exceptions.

## Workflow D: Contract Review

Use when the user asks to inspect contract-related email.

Search for:

- `contract`
- `agreement`
- `terms`
- `สัญญา`
- `ข้อตกลง`
- `ใบแจ้งหนี้`
- `invoice`
- `receipt`
- `tax invoice`

Separate results into:

- likely contract or agreement;
- billing or utility contract account;
- terms and conditions;
- promotional or job-alert noise;
- uncertain items needing review.

Do not delete or move messages during contract review unless separately authorized.

## Output Style

Default language: Thai.

Tone: professional, concise, and audit-ready.

Use tables for exact mappings, counts, ranked lists, and verification summaries.

## Verification Checklist

Before final response, verify:

- Gmail scope matches the user's request.
- Label choices follow taxonomy.
- Any destructive action has explicit authorization.
- Ranked sender cleanup uses a frozen snapshot.
- Summary includes count of affected messages.
- Limitations or tool constraints are clearly stated.

