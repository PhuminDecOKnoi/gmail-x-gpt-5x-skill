# Repository Standard

This repository follows a documentation-first standard for AI operations.

## Required Files

| File | Purpose |
|---|---|
| `README.md` | Executive overview, use cases, file map, quick start |
| `SKILL.md` | Governing skill behavior, boundaries, workflows, verification |
| `CONTRIBUTING.md` | Editing and contribution rules |
| `CHANGELOG.md` | Version history |
| `LICENSE` | License |
| `.github/copilot-instructions.md` | GitHub Copilot and Codex editing guidance |

## Required Folders

| Folder | Purpose |
|---|---|
| `prompts/` | Ready-to-run Prompt-AI files |
| `docs/` | Taxonomy, safety, operations, workflow, and pattern standards |
| `examples/` | Example run commands and expected behavior |
| `skills/` | Modular sub-skills for workflows that need stricter execution control |

## Naming Rules

| Artifact | Naming pattern |
|---|---|
| Prompt | `gmail-[workflow-name].prompt.md` |
| Sub-skill | `idNN-skill-[domain]-[workflow]` |
| Documentation | lowercase kebab-case Markdown |
| Example | `[workflow-name]-run.md` |

## Sub-Skill Folder Standard

Use a sub-skill when a workflow requires operational guardrails that should not be repeated in every prompt.

```text
skills/
└── idNN-skill-[domain]-[workflow]/
    ├── SKILL.md
    ├── references/
    │   └── [workflow-standard].md
    └── examples/
        └── [workflow-run].md
```

Keep sub-skill `SKILL.md` concise. Put detailed algorithms, schemas, and confirmation rules in `references/`.

## Acceptance Criteria

A repo update is complete when:

- README links to all major workflows;
- `SKILL.md` defines action boundaries and verification;
- destructive actions have explicit safety gates;
- prompt files are copy-paste ready;
- sub-skills are registered in README and root `SKILL.md`;
- examples show realistic Thai user commands;
- Markdown links are valid.
