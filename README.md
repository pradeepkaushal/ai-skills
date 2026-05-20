# ai-skills

A collection of [Claude Code](https://claude.com/claude-code) skills.

Each top-level folder is a self-contained skill. A skill is a `SKILL.md` file
(YAML frontmatter + Markdown instructions) plus any bundled resources, that
Claude loads on demand when the request matches the skill's description.

## Skills

| Skill | What it does |
|-------|--------------|
| [`scmp-daily-digest`](./scmp-daily-digest) | Fetches the day's news from the South China Morning Post (scmp.com) across nine sections and builds a dated markdown digest, closing with two analysis sections written for an India-based tech reader: "China Moves India Hasn't Matched Yet" and "AI Monetization Opportunities for India". |

## Installing a skill

Claude Code loads personal skills from `~/.claude/skills/`. To use a skill from
this repo, symlink it into that directory:

```bash
ln -s "$(pwd)/scmp-daily-digest" ~/.claude/skills/scmp-daily-digest
```

With a symlink, this repo stays the single source of truth — edits here apply
the next time Claude Code loads the skill.

## Repo layout

```
ai-skills/
├── README.md
├── .gitignore
└── <skill-name>/
    ├── SKILL.md          # required: frontmatter + instructions
    └── evals/            # optional: test prompts & assertions
        └── evals.json
```
