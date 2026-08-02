# Contributing

This repository is a Prompt-AI and SKILL knowledge base for Gmail workflows. Contributions should improve clarity, safety, repeatability, or auditability.

## Contribution Rules

| Area | Standard |
|---|---|
| Prompts | Keep them ready to run, with variables, source boundary, workflow, output contract, constraints, and verification |
| Gmail actions | Add a safety gate before destructive or state-changing behavior |
| Labels | Use the taxonomy in `docs/label-taxonomy.md` |
| Examples | Show expected inputs, outputs, and safety confirmations |
| Language | Prefer Thai for user-facing examples and concise English for technical headings |

## Prompt Quality Checklist

Before changing a prompt, verify:

- the Gmail scope is explicit;
- allowed and prohibited actions are clear;
- output tables are copy-paste ready;
- label decisions follow the taxonomy;
- delete, archive, move, send, draft, unsubscribe, and read-status changes require current user authorization;
- write actions include a verification step.

## File Placement

| Content | Path |
|---|---|
| Reusable prompt | `prompts/*.prompt.md` |
| Workflow documentation | `docs/workflows.md` |
| Safety rule | `docs/safety-rules.md` |
| Label rule | `docs/label-taxonomy.md` |
| Example run | `examples/*.md` |
