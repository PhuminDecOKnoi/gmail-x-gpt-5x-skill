![Gmail X GPT 5.x SKILL title banner](assets/readme-title-banner.svg)

# Gmail X GPT 5.x SKILL

[![Version](https://img.shields.io/badge/version-v1.3.1--dark--flow-38bdf8)](#version)
[![Skill](https://img.shields.io/badge/skill-Gmail%20Workflow-34d399)](SKILL.md)
[![Safety](https://img.shields.io/badge/safety-confirm%20before%20destructive%20actions-facc15)](docs/safety-rules.md)
[![License](https://img.shields.io/badge/license-MIT-94a3b8)](LICENSE)

Professional Prompt-AI and reusable SKILL framework for Gmail triage, label governance, ranked sender cleanup, and contract-related email review with GPT 5.x.

## Executive Overview

This repository converts recurring Gmail operations into auditable AI workflows. It is designed for use with GPT 5.x, Codex, GitHub Copilot, and connected Gmail tools where mailbox actions must be scoped, explainable, reversible, and explicitly authorized.

Core operating principle:

> Search, classify, label, and verify first. Delete, move, send, archive, mark read, or change settings only when the current user instruction explicitly authorizes that exact action.

## What You Can Do

| Capability | Use when | Start here |
|---|---|---|
| New-message labeling | You want recent Inbox and Spam messages classified with existing labels | [gmail-new-message-auto-labeler.prompt.md](prompts/gmail-new-message-auto-labeler.prompt.md) |
| Manual Inbox labeling | You want a selected Gmail scope classified by a standard taxonomy | [gmail-inbox-labeler.prompt.md](prompts/gmail-inbox-labeler.prompt.md) |
| Ranked sender cleanup | You want to rank Inbox senders, keep selected ranks, and move the rest to Trash after confirmation | [id01-skill-email-sender-cleanup](skills/id01-skill-email-sender-cleanup/SKILL.md) |
| Contract review | You want contract, agreement, invoice, receipt, or service-term messages surfaced | [gmail-contract-review.prompt.md](prompts/gmail-contract-review.prompt.md) |
| Safety governance | You want to know which Gmail actions require explicit confirmation | [safety-rules.md](docs/safety-rules.md) |

## Quick Start

1. Read the governing skill: [SKILL.md](SKILL.md).
2. Select the workflow from [docs/workflows.md](docs/workflows.md).
3. Use the label standard in [docs/label-taxonomy.md](docs/label-taxonomy.md).
4. Run the matching prompt from [prompts/](prompts/).
5. For ranked cleanup, use [id01-skill-email-sender-cleanup](skills/id01-skill-email-sender-cleanup/SKILL.md) before taking action.
6. Verify the result using [docs/operations.md](docs/operations.md).

## Recommended Run Flow

![Recommended Run Flow dark tone diagram](assets/recommended-run-flow-dark.svg)

Use the flow this way:

| Stage | Required control |
|---|---|
| Define Gmail scope | Search only the mailbox scope requested by the user |
| Classify or rank | Use metadata, snippets, and body context only as needed |
| Freeze snapshot | Preserve rank-to-sender-to-message mapping before cleanup |
| Confirm gated action | Require exact current authorization for delete, Trash, archive, send, or read-status changes |
| Execute and verify | Re-scan the affected Gmail scope and report final counts |

## Repository Map

| Path | Purpose |
|---|---|
| [README.md](README.md) | Public front page and navigation hub |
| [SKILL.md](SKILL.md) | Root skill, boundaries, workflows, and verification checklist |
| [prompts/](prompts/) | Ready-to-run Prompt-AI files |
| [skills/](skills/) | Modular sub-skills for high-control workflows |
| [docs/](docs/) | Taxonomy, operations, safety rules, prompt patterns, and repository standard |
| [examples/](examples/) | Copy-paste run examples |
| [.github/copilot-instructions.md](.github/copilot-instructions.md) | GitHub Copilot and Codex contributor guidance |
| [assets/](assets/) | README title/banner images and visual assets |

## Sub-Skill Registry

| ID | Sub-skill | Purpose | Main prompt |
|---|---|---|---|
| `id01` | [id01-skill-email-sender-cleanup](skills/id01-skill-email-sender-cleanup/SKILL.md) | Rank Inbox senders, keep selected ranks, and move non-kept Inbox messages to Trash using a frozen snapshot | [gmail-ranked-sender-cleanup.prompt.md](prompts/gmail-ranked-sender-cleanup.prompt.md) |

## Prompt-AI Standard

Every prompt in this repository follows the same professional control pattern:

```text
Role -> Objective -> Source Boundary -> Workflow -> Output Contract -> Constraints -> Verification -> Fallback
```

For implementation details, see [docs/prompt-patterns.md](docs/prompt-patterns.md).

## Safety Gates

The default safe actions are search, inspect, classify, summarize, and label when the user requests classification or triage.

These actions are gated and require exact current authorization:

| Gated action | Required authorization |
|---|---|
| Move to Trash or delete | The user must authorize the exact scope and action |
| Permanent delete | Separate explicit confirmation is required |
| Archive or remove from Inbox | The user must authorize the exact target scope |
| Send, reply, forward, or draft | The user must authorize the recipient and action |
| Mark read or unread | The user must authorize the status change |
| Filters, settings, unsubscribe | The user must authorize the exact account-level change |

See [docs/safety-rules.md](docs/safety-rules.md) for the full safety standard.

## Label Taxonomy

The canonical labels are maintained in [docs/label-taxonomy.md](docs/label-taxonomy.md). Use specific labels before `99_Archive-LowPriority`, and apply `00_SPAM-Review-Red` for Spam review.

| Label family | Examples |
|---|---|
| Work and development | `01_Work-GitHub`, `08_AI-SaaS` |
| Personal and finance | `02_Personal-Self`, `03_Finance-Bank`, `12_Receipt-Tax-Invoice` |
| Learning and professional | `05_Education-Learning`, `06_HR-Professional`, `09_Research-Academia` |
| Security and low priority | `13_Security-Account`, `99_Archive-LowPriority` |

## Examples

| Example | What it demonstrates |
|---|---|
| [keep-rank-run.md](examples/keep-rank-run.md) | Ranked sender cleanup run pattern |
| [new-message-auto-labeler-run.md](examples/new-message-auto-labeler-run.md) | Recent Inbox and Spam labeling run pattern |
| [skills/id01.../examples/keep-ranks-run.md](skills/id01-skill-email-sender-cleanup/examples/keep-ranks-run.md) | Sub-skill controlled cleanup example |

## Version

Current version: `v1.3.1-dark-flow`

Latest update:

- Replaced the `Recommended Run Flow` Mermaid block with a controlled Dark Tone SVG diagram.
- Added a generated title banner at [assets/readme-title-banner.svg](assets/readme-title-banner.svg).
