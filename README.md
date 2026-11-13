# Schedule Planning Skills

Agent skills for planning study and work time on a calendar. Each skill is a folder with a `SKILL.md` file, in the same format as [Anthropic's Agent Skills](https://github.com/anthropics/skills), so they work in Claude and in any app that reads that format.

| Skill | What it does |
|---|---|
| [successive-relearning](skills/successive-relearning/SKILL.md) | Spaced retrieval-practice study blocks, with same-day relearn blocks and a dose set by course difficulty. |
| [deadline-backplanner](skills/deadline-backplanner/SKILL.md) | Plans backwards from a due date: 3–6 dated milestone tasks, a buffer before the deadline, and work sessions for the big steps. |

## Use them

**Claude Code**

```
/plugin marketplace add Cel3brimbor/schedule-planning-skills
/plugin install schedule-planning-skills@schedule-planning-skills
```

Or copy a skill folder into `~/.claude/skills/` (all projects) or `.claude/skills/` (one project).

**Claude.ai and the Claude app**

Zip one skill folder (for example `successive-relearning/`) and upload it in **Settings → Capabilities → Skills**.

**Your own agent**

Load `skills/*/SKILL.md`. The YAML front matter has `name` and `description`; show those to the model so it can decide when a skill applies, and give it the body when the skill is used. Skills refer to an `ask_user` tool for questions. Map that to whatever question tool your agent has.

## Skill format

```
skills/
  <skill-name>/
    SKILL.md        # required: front matter + instructions
```

`SKILL.md` front matter:

```yaml
---
name: skill-name        # lowercase letters, digits and hyphens; same as the folder
description: What it does and when to use it, in one paragraph (max 1024 characters).
license: MIT
---
```

Keep each skill short. Write it for the model: what to do, in order, and when to stop and ask the user.

## Contributing

Open a pull request with one skill per folder. Skills are instructions only: no scripts, links to fetch, or requests for tools beyond reading and writing the calendar and asking the user.

## License

MIT. See [LICENSE](LICENSE).
