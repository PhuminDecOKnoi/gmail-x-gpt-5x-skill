# Changelog

## v1.3.2 - 2026-08-02

Expanded the README into a repository-level Skill Hub.

Improved:

- Added a detailed Skill Index linking the root skill and sub-skill `SKILL.md` files.
- Added related skill file mapping for prompts, references, examples, docs, and repository governance.
- Added a Skill Selection Guide that maps user requests to the correct skill, prompt, and safety rule.
- Added copy-paste invocation patterns for Prompt-AI / SKILL runs.
- Added detailed `id01` usage guidance for ranked sender cleanup.

## v1.3.1 - 2026-08-02

Improved the README workflow visual.

Added:

- `assets/recommended-run-flow-dark.svg`.

Improved:

- Replaced the `Recommended Run Flow` Mermaid block in `README.md` with a controlled Dark Tone SVG diagram for consistent GitHub rendering.

## v1.3.0 - 2026-08-02

Rebuilt the repository front page and added visual title assets.

Added:

- `assets/readme-title-banner.svg`.

Improved:

- README executive overview, navigation, quick start, workflow map, safety gates, repository map, and examples section.
- README top-of-file title banner for stronger GitHub presentation.

## v1.2.0 - 2026-08-02

Added the first modular sub-skill for ranked sender cleanup.

Added:

- `skills/id01-skill-email-sender-cleanup/SKILL.md`.
- `skills/id01-skill-email-sender-cleanup/references/sender-ranking-standard.md`.
- `skills/id01-skill-email-sender-cleanup/examples/keep-ranks-run.md`.

Improved:

- README sub-skill registry and repository tree.
- Root `SKILL.md` sub-skill registry.
- Workflow, operations, repository standard, prompt-pattern, and Copilot guidance for sub-skill controlled Gmail cleanup.
- `prompts/gmail-ranked-sender-cleanup.prompt.md` with governing sub-skill reference.

## v1.1.0 - 2026-08-02

Standardized repository structure and content.

Added:

- `CONTRIBUTING.md`.
- `docs/operations.md`.
- `docs/prompt-patterns.md`.
- `docs/repository-standard.md`.
- `examples/new-message-auto-labeler-run.md`.

Improved:

- README structure, quick start, file map, and operating model.
- `SKILL.md` with skill boundary, prompt pattern, fallback, and verification rules.
- Workflow documentation with trigger phrases, output contracts, and verification tables.
- Safety rules with authorization standard and final safety statement.
- Prompt files with user input variables, source boundary, verification, and output contracts.
- Copilot instructions with file placement and prompt consistency rules.

## v1.0.0 - 2026-08-02

Initial Gmail X GPT 5.x SKILL repository.

Added:

- `SKILL.md` for Gmail triage and cleanup workflow.
- New-message labeling prompt.
- Inbox sender ranking and cleanup prompt.
- Inbox labeler prompt.
- Contract and agreement review prompt.
- Label taxonomy.
- Safety rules.
- Workflow documentation.
- GitHub Copilot instructions.