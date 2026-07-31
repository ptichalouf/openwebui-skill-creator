# Skill Creator — Workspace Skills for Open WebUI

An [Open WebUI](https://github.com/open-webui/open-webui) **Tool** that interviews
you, drafts a Workspace **Skill** (`SKILL.md`, Claude-style), and **persists**
it via `POST /api/v1/skills/create` — private by default.

Pair with **[Model Creator](https://github.com/ianustec/openwebui-model-creator)**
to bind skills onto Workspace Models.

> License: MIT · Author: [IANUSTEC](https://ianustec.com) · Requires Open WebUI `>= 0.10.0`

## Features

- **Saves for real** — does not only paste `SKILL.md` in chat; calls the Skills
  API with the user’s session token.
- **Claude-style workflow**: interview → draft → validate → create.
- **Pushy descriptions**: WHAT + WHEN (trigger phrases) for reliable skill
  selection.
- **Private by default** — empty `access_grants` (owner-only).
- **SKILL.md or JSON** input with YAML frontmatter.
- **Single-file** — paste into Workspace → Tools.

## Requirements

- Open WebUI `>= 0.10.0` (Workspace Skills API)
- Permission to create workspace skills (or admin)
- Python deps (auto-installed from frontmatter): `httpx`, `pydantic`, `PyYAML`

## Installation

### Option A — Open WebUI community
1. Open the tool page on the Open WebUI community site.
2. Click **Get** / **Import**.

### Option B — manual
1. **Workspace → Tools → +**
2. Paste [`skill_creator.py`](skill_creator.py)
3. Save and enable the tool on a model/chat

## Usage

The model should:

1. Interview: what the skill enables, when it should trigger, expected output.
2. Draft `SKILL.md` with `name` + `description` (and body instructions).
3. Optionally call `validate_skill`.
4. Call `create_skill(content)` to persist.

### Example SKILL.md

See [`examples/code-review.md`](examples/code-review.md).

```markdown
---
name: code-review-guidelines
description: Step-by-step code review checklist. Use whenever the user asks
  for a code review, PR feedback, or to check a diff — even if they do not
  say "skill" or "guidelines".
---

# Code Review Guidelines

1. Check correctness and edge cases
2. Verify tests and error handling
3. Flag security and performance risks
4. Suggest a clear next action
```

### Tools exposed

| Function | Purpose |
|----------|---------|
| `create_skill` | Parse, validate, persist |
| `update_skill` | Update an existing skill by id |
| `validate_skill` | Validate without saving |

### Valves

| Valve | Default | Meaning |
|-------|---------|---------|
| `default_private` | `true` | Empty `access_grants` |
| `default_active` | `true` | `is_active=true` |
| `allow_update_if_exists` | `true` | Update when id is taken |
| `owui_api_base` | `""` | Override API base (else `request.base_url`) |

## Related

- [Model Creator](https://github.com/ianustec/openwebui-model-creator)
- [Generate Documents](https://github.com/ianustec/openwebui-generate-documents)
- [Generate Slides](https://github.com/ianustec/openwebui-generate-slides)
- [Generate Spreadsheets](https://github.com/ianustec/openwebui-generate-spreadsheets)

## License

MIT — see [LICENSE](LICENSE).
