# Prompt-AI Pattern Standard

This repository uses a consistent Prompt-AI structure so Gmail workflows can be reused without reconstructing intent.

## Standard Pattern

```text
Role
Objective
User Input Variables
Source Boundary
Gmail Scope
Workflow
Output Contract
Hard Constraints
Verification
Fallback / Error Handling
```

## Section Requirements

| Section | Required content |
|---|---|
| Role | What the AI is responsible for |
| Objective | The concrete outcome of the run |
| User Input Variables | Scope, ranks, labels, time window, or other user-controlled values |
| Source Boundary | Gmail-only or approved source list |
| Gmail Scope | Query such as `in:inbox`, `in:spam`, or `newer_than:1h` |
| Workflow | Ordered observable steps |
| Output Contract | Exact tables, fields, language, and summary |
| Hard Constraints | Actions the AI must not perform |
| Verification | Checks before final response |
| Fallback | What to do when results are incomplete or tools fail |

## Gmail Prompt Rules

- Use sender email address as the stable identity.
- Use display name only as supporting context.
- Apply multiple labels when evidence supports multiple categories.
- Use `99_Archive-LowPriority` only when no specific label fits.
- Use Trash wording for deletion workflows.
- Treat permanent deletion as a separate workflow requiring separate confirmation.

## Copy-Paste Prompt Header

```text
/USE SKILL: gmail-x-gpt-5x-skill
/USE PROMPT: [path/to/prompt.md]

Task:
[ระบุงานที่ต้องการ]

Variables:
- Gmail scope: [...]
- Time window: [...]
- Keep ranks: [...]
- Allowed action: [...]

Output:
- Language: Thai
- Format: Tables plus concise summary
```
