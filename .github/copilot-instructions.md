# Copilot Instructions

This repository contains Prompt-AI and SKILL documentation for Gmail workflows with GPT 5.x.

## Editing Standards

- Keep prompts reusable and copy-paste ready.
- Preserve Thai instructions when they reflect user workflow language.
- Prefer tables for label mappings, sender rankings, and verification summaries.
- Do not add destructive Gmail behavior without an explicit safety gate.
- For cleanup prompts, require a frozen ranked snapshot before moving messages to Trash.
- Use `Trash` wording instead of permanent delete unless the prompt explicitly covers permanent deletion.

## Repository Intent

The repository is not an app. It is a professional prompt and workflow knowledge base for:

- Gmail label automation;
- Inbox cleanup;
- sender ranking;
- contract-related email review;
- safe Gmail operations.

## Quality Gate

Before changing a prompt, check:

- source boundary is clear;
- allowed and prohibited actions are explicit;
- output format is testable;
- destructive actions require current user authorization;
- verification step exists after write operations.

