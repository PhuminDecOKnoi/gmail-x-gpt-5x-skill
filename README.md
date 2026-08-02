# Gmail X GPT 5.x SKILL

Professional Prompt-AI and SKILL repository for Gmail triage, labeling, inbox cleanup, contract review, and safe automation with GPT 5.x.

## Purpose

This repository standardizes Gmail workflows for AI-assisted email operations. It is designed for use with GPT 5.x, GitHub Copilot, Codex, and connected Gmail tools.

The core principle is simple:

> Read, classify, label, and verify first. Delete, move, send, or modify only when the user gives explicit authorization.

## Core Use Cases

| Use case | Description | Primary file |
|---|---|---|
| New-message labeling | Check new Inbox messages and apply existing labels | [prompts/gmail-new-message-auto-labeler.prompt.md](prompts/gmail-new-message-auto-labeler.prompt.md) |
| Inbox sender ranking | Group Inbox by sender, count, rank, and optionally clean up | [prompts/gmail-ranked-sender-cleanup.prompt.md](prompts/gmail-ranked-sender-cleanup.prompt.md) |
| Manual triage | Classify messages using sender, subject, snippet, and body context | [prompts/gmail-inbox-labeler.prompt.md](prompts/gmail-inbox-labeler.prompt.md) |
| Contract review | Find messages related to contract, agreement, invoice, or service terms | [prompts/gmail-contract-review.prompt.md](prompts/gmail-contract-review.prompt.md) |
| Safety controls | Operational rules for Gmail actions | [docs/safety-rules.md](docs/safety-rules.md) |

## Repository Structure

```text
.
├── README.md
├── SKILL.md
├── prompts/
│   ├── gmail-inbox-labeler.prompt.md
│   ├── gmail-new-message-auto-labeler.prompt.md
│   ├── gmail-ranked-sender-cleanup.prompt.md
│   └── gmail-contract-review.prompt.md
├── docs/
│   ├── label-taxonomy.md
│   ├── workflows.md
│   └── safety-rules.md
├── examples/
│   └── keep-rank-run.md
└── .github/
    └── copilot-instructions.md
```

## Gmail Label Taxonomy

| Label | Intended use |
|---|---|
| `00_SPAM-Review-Red` | Gmail spam or suspicious messages requiring review |
| `01_Work-GitHub` | GitHub, CodeRabbit, repo, PR, issue, code, CI, and development messages |
| `02_Personal-Self` | Messages from or clearly about Phumin Decoknoi or the authenticated user |
| `03_Finance-Bank` | Bank, loan, payment, financial alerts, and financial service messages |
| `04_Bills-Utility` | Utility bills and services such as MEA and True |
| `05_Education-Learning` | Courses, universities, training, AIHR, Coursera, Alison, MUT |
| `06_HR-Professional` | HR, labour, governance, ESG, KPI Institute, UN Global Compact, professional communities |
| `07_Social-LinkedIn` | LinkedIn notifications, job alerts, and message digests |
| `08_AI-SaaS` | OpenAI, Anthropic, Notion, Perplexity, OpenRouter, SaaS and AI tools |
| `09_Research-Academia` | Papers, Academia.edu, research, journals, and academic alerts |
| `10_Shopping-Promo` | Shopping, ecommerce, promotions, sales, and marketing campaigns |
| `11_Travel-Booking` | Travel, hotel, flight, and booking alerts |
| `12_Receipt-Tax-Invoice` | Receipts, invoices, billing notices, tax invoices, and payment documents |
| `13_Security-Account` | Login, password, OTP, verification, and account security alerts |
| `99_Archive-LowPriority` | Low-priority messages when no specific label fits |

## Standard Operating Model

1. Search only the requested Gmail scope.
2. Read only the minimum context required for classification.
3. Apply existing labels according to the taxonomy.
4. Do not delete, archive, move, send, or mark read unless explicitly authorized.
5. For deletion workflows, freeze the sender-rank snapshot before taking action.
6. Verify final counts after any write action.

## Recommended Prompt

For recurring Gmail automation, start with:

[prompts/gmail-new-message-auto-labeler.prompt.md](prompts/gmail-new-message-auto-labeler.prompt.md)

For Inbox cleanup by ranked sender, use:

[prompts/gmail-ranked-sender-cleanup.prompt.md](prompts/gmail-ranked-sender-cleanup.prompt.md)

## Version

Current version: `v1.0.0-gmail-x-gpt-5x-skill`

