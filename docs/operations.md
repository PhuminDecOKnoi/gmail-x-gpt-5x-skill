# Gmail Operations Standard

This document defines the operational standard for running Gmail X GPT 5.x SKILL.

## Operation Classes

| Class | Examples | Default permission |
|---|---|---|
| Read | Search messages, inspect sender, subject, snippet, labels | Allowed when requested |
| Label | Apply existing Gmail labels | Allowed when user asks for classification or triage |
| State change | Move to Trash, archive, move out of Inbox, mark read/unread | Explicit authorization required |
| Communication | Send, reply, forward, draft | Explicit authorization required |
| Settings | Filters, signature, account settings, unsubscribe | Tool support and explicit authorization required |

## Standard Run Sequence

1. Confirm user intent and Gmail scope.
2. Search only the requested scope.
3. Inspect minimum required context.
4. Classify or rank according to the selected workflow.
5. Apply the relevant sub-skill when the workflow requires stricter control.
6. Apply labels only when allowed.
7. Ask for confirmation before state-changing actions unless already explicitly authorized.
8. Execute authorized write actions.
9. Verify and report results.

## Sub-Skill Controlled Operations

| Operation | Sub-skill | Special control |
|---|---|---|
| Ranked sender cleanup | `skills/id01-skill-email-sender-cleanup/SKILL.md` | Freeze rank-to-sender-to-message mapping before moving non-kept Inbox messages to Trash |

## Previous-Run Boundary

For recurring checks, use a durable previous-run marker when available. If no durable marker exists, use a conservative window such as:

```text
newer_than:1h
```

State the window used in the final response.

## Verification Report

After any operation, return:

| Field | Required |
|---|---|
| Gmail scope | Query or location searched |
| Messages found | Total count |
| Labels applied | Count by label |
| State changes | Confirm whether any occurred |
| Exceptions | Tool errors, incomplete pages, ambiguous messages |

## Prohibited By Default

Do not permanently delete messages, alter Gmail settings, create filters, unsubscribe, or send messages unless the user asks for that exact action and the tool supports it.
