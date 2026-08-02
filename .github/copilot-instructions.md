# Copilot Instructions

This repository contains Prompt-AI and SKILL documentation for Gmail workflows with GPT 5.x.

## Language And Tone

- Use Thai for user-facing workflow examples unless a file is intentionally English-only.
- Keep English technical terms when they are standard Gmail, GitHub, or AI workflow terms.
- Write concise, professional, audit-ready documentation.

## Editing Standards

- Keep prompts reusable and copy-paste ready.
- Preserve Thai instructions when they reflect user workflow language.
- Prefer tables for label mappings, sender rankings, and verification summaries.
- Do not add destructive Gmail behavior without an explicit safety gate.
- For cleanup prompts, require a frozen ranked snapshot before moving messages to Trash.
- Use `Trash` wording instead of permanent delete unless the prompt explicitly covers permanent deletion.
- Keep the prompt pattern consistent: Role, Objective, Source Boundary, Workflow, Output Contract, Constraints, Verification.

## Repository Intent

The repository is not an app. It is a professional prompt and workflow knowledge base for:

- Gmail label automation;
- Inbox cleanup;
- sender ranking;
- contract-related email review;
- safe Gmail operations.

## File Placement

| Content type | Location |
|---|---|
| Reusable Gmail prompt | `prompts/*.prompt.md` |
| Operating rule or taxonomy | `docs/*.md` |
| Example run | `examples/*.md` |
| Workflow sub-skill | `skills/idNN-skill-domain-workflow/SKILL.md` |
| Skill behavior | `SKILL.md` |
| Repo overview | `README.md` |

## Quality Gate

Before changing a prompt, check:

- source boundary is clear;
- allowed and prohibited actions are explicit;
- output format is testable;
- destructive actions require current user authorization;
- verification step exists after write operations.
- documentation links are valid relative links.
