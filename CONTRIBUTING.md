# Contributing

> **Note:** This is not an open‑contribution project. This guide exists as a personal reference so I (and my AI agents) know how to keep things organized.

## Adding a New Workflow

1. **Create the directory**
   ```
   workflows/<workflow-name>/
   ```

2. **Write `SKILL.md`** with YAML frontmatter and step‑by‑step instructions:
   ```yaml
   ---
   name: workflow-name
   description: One‑line summary of what the workflow automates
   ---
   ```
   The body contains the steps OpenClaw will execute at runtime.

3. **Add supporting files** (optional):
   ```
   <workflow-name>/
   ├── SKILL.md
   ├── scripts/       # Automation scripts
   ├── resources/     # Templates, configs, assets
   └── references/    # Extra docs the agent can read
   ```

4. **Test the workflow** — run it through OpenClaw and verify it completes as expected.

5. **Open a PR** using the PR template and let the review checklist pass.

## Naming Conventions

- Directories: `kebab-case`
- `SKILL.md` frontmatter `name` must match the directory name
- Keep descriptions under 80 characters

## Quality Checklist

- [ ] `SKILL.md` has valid YAML frontmatter (`name` + `description`)
- [ ] Steps are clear and reproducible
- [ ] No hardcoded paths or user‑specific values
- [ ] Tested on OpenClaw
