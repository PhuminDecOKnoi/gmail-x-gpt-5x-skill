# Gmail X GPT 5.x SKILL

Professional Prompt-AI and reusable SKILL framework for Gmail triage, labeling, sender ranking, safe Inbox cleanup, and contract-related email review with GPT 5.x.

## Overview

This repository turns recurring Gmail operations into clear, auditable AI workflows. It is designed for use with GPT 5.x, Codex, GitHub Copilot, and connected Gmail tools.

Core principle:

> Search, classify, label, and verify first. Delete, move, send, archive, or change read status only when the current user instruction explicitly authorizes that exact action.

## What This Repo Solves

| Workflow | Purpose | Primary artifact |
|---|---|---|
| New message auto-labeling | Check new Inbox and Spam messages, then apply existing labels | [prompts/gmail-new-message-auto-labeler.prompt.md](prompts/gmail-new-message-auto-labeler.prompt.md) |
| Inbox manual labeling | Classify a selected Gmail scope using the standard label taxonomy | [prompts/gmail-inbox-labeler.prompt.md](prompts/gmail-inbox-labeler.prompt.md) |
| Ranked sender cleanup | Rank Inbox senders by count and keep only selected ranks after confirmation | [skills/id01-skill-email-sender-cleanup/SKILL.md](skills/id01-skill-email-sender-cleanup/SKILL.md) and [prompts/gmail-ranked-sender-cleanup.prompt.md](prompts/gmail-ranked-sender-cleanup.prompt.md) |
| Contract review | Find contract, agreement, invoice, receipt, and service-term messages | [prompts/gmail-contract-review.prompt.md](prompts/gmail-contract-review.prompt.md) |
| Operational control | Define safe actions, restricted actions, fallback, and verification rules | [docs/operations.md](docs/operations.md) |

## Standard Repository Structure

```text
.
├── README.md
├── SKILL.md
├── CONTRIBUTING.md
├── CHANGELOG.md
├── LICENSE
├── docs/
│   ├── label-taxonomy.md
│   ├── operations.md
│   ├── prompt-patterns.md
│   ├── repository-standard.md
│   ├── safety-rules.md
│   └── workflows.md
├── skills/
│   └── id01-skill-email-sender-cleanup/
│       ├── SKILL.md
│       ├── examples/
│       │   └── keep-ranks-run.md
│       └── references/
│           └── sender-ranking-standard.md
├── examples/
│   ├── keep-rank-run.md
│   └── new-message-auto-labeler-run.md
├── prompts/
│   ├── gmail-contract-review.prompt.md
│   ├── gmail-inbox-labeler.prompt.md
│   ├── gmail-new-message-auto-labeler.prompt.md
│   └── gmail-ranked-sender-cleanup.prompt.md
└── .github/
    └── copilot-instructions.md
```

## Quick Start

Use the repo in this order:

1. Read [SKILL.md](SKILL.md) for the governing workflow and action boundary.
2. Use [docs/label-taxonomy.md](docs/label-taxonomy.md) to classify messages.
3. Use the relevant sub-skill in [skills/](skills/) when the workflow needs stricter execution control.
4. Select the correct prompt from [prompts/](prompts/).
5. Check [docs/safety-rules.md](docs/safety-rules.md) before any Gmail write action.
6. Use [examples/](examples/) as copy-paste run patterns.

## Sub-Skill Registry

| ID | Sub-skill | Purpose | Main prompt |
|---|---|---|---|
| `id01` | [id01-skill-email-sender-cleanup](skills/id01-skill-email-sender-cleanup/SKILL.md) | Rank Inbox senders, keep selected ranks, and move non-kept Inbox messages to Trash with a frozen snapshot | [gmail-ranked-sender-cleanup.prompt.md](prompts/gmail-ranked-sender-cleanup.prompt.md) |

## Gmail Label Taxonomy

| Label | Intended use |
|---|---|
| `00_SPAM-Review-Red` | Gmail Spam or suspicious messages requiring review |
| `01_Work-GitHub` | GitHub, CodeRabbit, repo, PR, issue, CI, code, and development messages |
| `02_Personal-Self` | Messages from or clearly about Phumin Decoknoi or the authenticated user |
| `03_Finance-Bank` | Bank, loan, card, transfer, and financial alerts |
| `04_Bills-Utility` | Utility bills and services such as MEA, True, internet, mobile, and utilities |
| `05_Education-Learning` | Courses, universities, training, AIHR, Coursera, Alison, MUT, certificates |
| `06_HR-Professional` | HR, labour, governance, ESG, KPI Institute, UN Global Compact, professional communities |
| `07_Social-LinkedIn` | LinkedIn notifications, job alerts, and message digests |
| `08_AI-SaaS` | OpenAI, Anthropic, Notion, Perplexity, OpenRouter, SaaS, and AI tools |
| `09_Research-Academia` | Papers, Academia.edu, research, journals, academic alerts |
| `10_Shopping-Promo` | Shopping, ecommerce, deals, discounts, promotions, campaigns |
| `11_Travel-Booking` | Travel, hotel, flight, booking, itinerary alerts |
| `12_Receipt-Tax-Invoice` | Receipts, invoices, billing notices, tax invoices, payment documents |
| `13_Security-Account` | Login, password, OTP, verification, account security alerts |
| `99_Archive-LowPriority` | Low-priority messages only when no specific label fits |

## Operating Model

| Stage | Required behavior |
|---|---|
| Scope | Search only the Gmail scope requested by the user |
| Minimize | Read only metadata, snippets, and body context needed for classification |
| Classify | Apply one or more labels according to taxonomy |
| Protect | Treat delete, archive, move, send, draft, mark read/unread, unsubscribe, and settings changes as gated actions |
| Snapshot | For ranked cleanup, freeze rank-to-sender-to-message mapping before taking action |
| Verify | Re-check the affected scope and report final counts after write operations |

## Prompt-AI Pattern

All prompts follow this reusable structure:

```text
Role -> Objective -> Source Boundary -> Workflow -> Output Contract -> Constraints -> Verification
```

See [docs/prompt-patterns.md](docs/prompt-patterns.md) for the complete pattern standard.

## Version

Current version: `v1.2.0-sub-skill-id01`
