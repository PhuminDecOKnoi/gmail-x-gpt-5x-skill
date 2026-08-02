---
name: gmail-x-gpt-5x-skill
description: Gmail triage and cleanup skill for GPT 5.x. Use for classifying Inbox messages, applying Gmail labels, checking Spam, reviewing contract-related messages, and safely cleaning Inbox by ranked sender. Prioritizes non-destructive operations unless explicit user authorization is given.
---

# Gmail X GPT 5.x SKILL

## Mission

Help the user manage Gmail with GPT 5.x through a professional, auditable, and safe operating model.

This skill supports:

- Inbox classification and labeling.
- New-message labeling.
- Gmail Spam review labeling.
- Sender ranking by Inbox count.
- Safe cleanup by keeping selected sender ranks and moving other Inbox messages to Trash.
- Contract, agreement, invoice, and service-term review.

## Skill Boundary

This is a Gmail workflow and Prompt-AI skill. It is not a Gmail settings manager, email marketing tool, or permanent deletion playbook.

Use only connected Gmail data unless the user explicitly asks for external research. Do not infer private facts from outside the mailbox.

## Safety Boundary

Default actions are read-only plus label application when the user asks for classification or triage.

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

## Standard Prompt Pattern

Every prompt in this repository should include:

1. Role.
2. Objective.
3. User input or variables.
4. Source boundary.
5. Workflow.
6. Output contract.
7. Hard constraints.
8. Verification.
9. Fallback or error handling for incomplete Gmail results.

## Sub-Skill Registry

Use sub-skills when a workflow needs more precise operational control than a prompt alone.

| ID | Sub-skill | Use when |
|---|---|---|
| `id01` | [skills/id01-skill-email-sender-cleanup/SKILL.md](skills/id01-skill-email-sender-cleanup/SKILL.md) | The user asks to rank Inbox senders, keep selected rank numbers, and move all other Inbox messages to Trash |

## Standard Labels

Use the label taxonomy in [docs/label-taxonomy.md](docs/label-taxonomy.md).

If a message matches more than one label, apply all relevant specific labels. Avoid `99_Archive-LowPriority` when a more specific label fits.

For Gmail Spam, apply:

`00_SPAM-Review-Red`

The tool may not be able to set the visual label color. If so, create or apply the label name only and tell the user that Gmail UI must be used for visual color settings.

## Workflow A: New Inbox Labeling

Use when the user asks to check new messages since the previous run or asks for automatic classification of recent Inbox messages.

1. Search for new Inbox messages using the best available previous-run boundary.
2. If no durable previous-run state exists, use a conservative recent window such as `newer_than:1h`.
3. For each new message, inspect sender, subject, snippet, labels, and available body context.
4. Apply existing labels according to taxonomy.
5. Check Gmail Spam separately and apply `00_SPAM-Review-Red` to Spam messages.
6. Do not delete, archive, move, send, or mark read.
7. Return a summary table by label count.

Minimum output:

| Field | Requirement |
|---|---|
| Inbox new messages | Count searched and count labeled |
| Spam messages | Count searched and count labeled |
| Label summary | Count by label |
| Safety statement | Confirm no delete, move, archive, send, or read-status change |

## Workflow B: Inbox Sender Ranking

Use when the user asks to list senders in Inbox and count messages.

1. Search Gmail scope `in:inbox`.
2. Normalize sender identity primarily by email address.
3. Count Inbox messages per sender.
4. Sort senders by count descending.
5. Assign rank numbers from `1` to `N`.
6. Return a table with rank, sender name, sender email, message count, and sample subjects.

Rank numbers are valid only for the current frozen run. Do not reuse rank numbers across different runs.

## Workflow C: Cleanup By Kept Sender Ranks

Use when the user says to keep ranks such as `X Y Z` and delete the rest.

Apply sub-skill `id01-skill-email-sender-cleanup` for this workflow.

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

If the user only asks to "list" or "rank", stop after Workflow B. If the user asks to "delete the rest" but does not provide kept ranks, ask for the ranks before taking action.

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

## Fallback Rules

If a Gmail search or write operation fails:

1. Stop the operation.
2. Report what was completed.
3. Report what was not completed.
4. Ask before retrying any destructive or state-changing action.

If message results are incomplete or paginated, report the limitation before drawing final conclusions.

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
