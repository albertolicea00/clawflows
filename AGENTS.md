# AI Knowledge Base

> If you're an AI, read this first before starting any task.

## What this repo is

`clawflows` is a personal collection of **workflows (skills) for [OpenClaw](https://openclaw.ai)**.
It contains no application code — no build step, no dependencies, no runtime. Every unit of work
is a directory under `workflows/` holding Markdown instructions that OpenClaw executes at runtime.

Based on [clawflows](https://github.com/nikilster/clawflows) by @nikilster
([clawflows.com](https://clawflows.com/)) — consult that repo for upstream conventions before
inventing new ones here.

Users install from here with:

```bash
openclaw skills install albertolicea00/clawflows              # all workflows
openclaw skills install albertolicea00/clawflows/<workflow>   # one workflow
```

## Layout

```
workflows/<workflow-name>/
├── SKILL.md      # required — frontmatter + steps
├── scripts/      # optional — automation scripts
├── resources/    # optional — templates, configs, assets
└── references/   # optional — extra docs the agent may read
docs/             # repo-level documentation
tests/            # workflow test material
.github/          # issue + PR templates
```

`workflows/`, `docs/`, and `tests/` currently hold only `.gitkeep` — the repo is scaffolding
awaiting its first workflow.

## SKILL.md contract

```yaml
---
name: workflow-name
description: One-line summary of what the workflow automates
---
```

- `name` must equal the containing directory name.
- `description` under 80 characters.
- Body = the steps OpenClaw runs. Write them as imperative, reproducible instructions.

## Rules for agents working here

- Directory names are `kebab-case`.
- No hardcoded absolute paths, API keys, or user-specific values in any workflow.
- One workflow per directory; don't bundle unrelated automations.
- A workflow must be testable through OpenClaw before it is considered done.
- Update `CHANGELOG.md` only for core changes — see below.
- A new workflow goes through the templates: `new-workflow` issue first, then a PR — see
  "New workflow procedure" below.
- Follow `CONTRIBUTING.md` for the full add-a-workflow procedure and quality checklist;
  `.github/PULL_REQUEST_TEMPLATE.md` mirrors that checklist.

## New workflow procedure

Every new workflow goes through the templates. No workflow is added straight to `main` from a
loose commit.

1. **Open an issue** with `.github/ISSUE_TEMPLATE/new-workflow.md` (the 🆕 New Workflow template,
   label `new-workflow`). Fill in the name, description, trigger, the `SKILL.md` frontmatter
   block, and the steps preview before writing any files. The issue is where the workflow is
   agreed on; the PR is only where it is delivered.
2. **Write the workflow** on a branch, following the `SKILL.md` contract and layout above and the
   procedure in `CONTRIBUTING.md`.
3. **Test it through OpenClaw** — see "Verification" below.
4. **Open a PR** with `.github/PULL_REQUEST_TEMPLATE.md`, tick 🆕 New workflow under Type, link
   the issue (`Closes #<n>`), and complete the checklist and the Testing section with the real
   trigger prompt and expected vs actual output.
5. **Add the changelog entry** under `## [Unreleased]` → `### Added` — adding a workflow is a
   core change.

The same issue-then-PR flow applies to renaming, removing, or changing the behaviour of an
existing workflow; use the PR template's matching Type checkbox. Pure documentation or metadata
edits need no issue.

## Changelog policy

`CHANGELOG.md` tracks the **substance of the project**, not every commit. Most changes do not
belong in it. Ask: does this change what a user gets when they install from this repo?

**Goes in the changelog** — core changes:

- Adding a workflow.
- Removing or renaming a workflow.
- Modifying a workflow's behaviour, steps, inputs, or outputs.
- Changing the `SKILL.md` contract, the install commands, or the directory structure
  workflows must follow.
- Anything that breaks an existing install or changes how a workflow runs.

**Does not go in the changelog** — cosmetic or peripheral changes:

- README, docs, or comment edits.
- Typos, wording, formatting, image or banner swaps.
- Repo metadata: LICENSE, `.gitignore`, issue/PR templates, credits.
- Internal reorganisation with no user-visible effect.
- Edits to this file.

When in doubt, leave it out. A changelog padded with cosmetic entries hides the entries that
matter. The commit history already records everything else.

Format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/) — add entries under
`## [Unreleased]` in the matching `### Added` / `### Changed` / `### Removed` group.

## Commit attribution

Co-author trailers are **allowed**, and **mandatory for any AI agent** that produced or modified
the content of a commit. Add one trailer per contributing agent, as the last lines of the commit
message body, separated from the body by a blank line:

```
Co-authored-by: Claude Opus 5 (1M context) <noreply@anthropic.com>
```

Rules:

- Canonical casing is `Co-authored-by:` — match it exactly so GitHub links the attribution.
- Name the specific model and version you actually are, not a generic "AI".
- One trailer per agent; multiple agents on one commit means multiple trailers.
- The trailer is required even when a human reviewed and edited the output afterwards.
  Review does not erase authorship.
- The human author stays the commit `author`; the agent is only ever a co-author.

Known agent identities are listed in `credits`. If you are an agent not listed there, add
yourself to `credits` in the same commit.

## Verification

There is no test runner in this repo. "Testing" means running the workflow through OpenClaw
and recording the trigger prompt plus expected vs actual output in the PR description.
Do not claim a workflow is tested unless that run actually happened.

## Related files

| File | Purpose |
|---|---|
| `README.md` | Public-facing description and install instructions |
| `CONTRIBUTING.md` | How to add a workflow (personal reference, not open contribution) |
| `CHANGELOG.md` | History of core changes only (see "Changelog policy") |
| `SECURITY.md` | Security reporting policy |
| `CLAUDE.md` | Pointer to this file |
