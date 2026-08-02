# Gmail Label Taxonomy

This document defines the standard labels used by Gmail X GPT 5.x SKILL.

| Label | Category | Use when | Notes |
|---|---|---|---|
| `00_SPAM-Review-Red` | Spam review | Gmail places the message in Spam or it appears suspicious | Label color may need to be set manually in Gmail UI |
| `01_Work-GitHub` | Work and code | GitHub, CodeRabbit, repositories, pull requests, issues, CI, code review | Use with `08_AI-SaaS` if the message is both dev and AI tooling |
| `02_Personal-Self` | Personal identity | From or clearly about Phumin Decoknoi or the authenticated user | Use for self-sent records and personal account messages |
| `03_Finance-Bank` | Finance | Bank, loan, payment, financial alert, card, transfer | Combine with `12_Receipt-Tax-Invoice` for receipts |
| `04_Bills-Utility` | Utilities | MEA, True, internet, mobile, utility billing | Often combined with `12_Receipt-Tax-Invoice` |
| `05_Education-Learning` | Education | Courses, universities, training, AIHR, Coursera, Alison, MUT | Include certificates and enrollment messages |
| `06_HR-Professional` | Professional HR | HR, labour, governance, ESG, compliance, KPI Institute, UN Global Compact | Include professional newsletters and communities |
| `07_Social-LinkedIn` | LinkedIn and social | LinkedIn notifications, job alerts, message digests | Can overlap with `06_HR-Professional` |
| `08_AI-SaaS` | AI and SaaS | OpenAI, Anthropic, Notion, Perplexity, OpenRouter, SaaS tools | Include product updates and account notices |
| `09_Research-Academia` | Research | Papers, Academia.edu, journals, academic alerts | Use for study and research leads |
| `10_Shopping-Promo` | Shopping and promo | Ecommerce, deals, shopping, promotions, campaigns | Use for commercial promotional email |
| `11_Travel-Booking` | Travel | Travel, hotel, flight, booking alerts | Include confirmations and itinerary changes |
| `12_Receipt-Tax-Invoice` | Receipts and tax | Receipts, invoices, billing, tax invoices, payment documents | Combine with relevant domain label |
| `13_Security-Account` | Security | Login, OTP, password, verification, account security | High-priority review |
| `99_Archive-LowPriority` | Low priority | No specific label fits and message appears low priority | Do not use when a specific label applies |

## Multi-Label Rule

Apply multiple labels when a message clearly belongs to multiple categories.

Examples:

| Message type | Labels |
|---|---|
| MEA e-tax invoice | `04_Bills-Utility`, `12_Receipt-Tax-Invoice` |
| Bank receipt with login alert | `03_Finance-Bank`, `12_Receipt-Tax-Invoice`, `13_Security-Account` |
| LinkedIn HR job alert | `06_HR-Professional`, `07_Social-LinkedIn` |
| GitHub Copilot billing receipt | `01_Work-GitHub`, `08_AI-SaaS`, `12_Receipt-Tax-Invoice` |

