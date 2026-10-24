# claude-skills

Personal [Claude Code](https://code.claude.com) skills, packaged as a plugin marketplace.

## Install

```
/plugin marketplace add KarasIlia/claude-skills
/plugin install learning@karasilia-skills
```

## Plugins

### learning

| Skill | What it does |
|---|---|
| `grok` | Guided study session for a concept or mechanism: theory → practice tasks with self-checks → review, plus documentation and further reading. Domain references: iOS/Swift (Swift package with Swift Testing), systems analysis (requirements, UML/BPMN, OpenAPI, SQL with automatic checks). |

Invoke with `/learning:grok <topic>` or just ask to learn something, e.g. "хочу разобраться в actors".

## Structure

```
.claude-plugin/marketplace.json   # marketplace catalog
plugins/<plugin>/
├── .claude-plugin/plugin.json    # plugin manifest
└── skills/<skill>/SKILL.md       # skills (+ references/)
```

## Updating

After pushing changes, bump `version` in the plugin's `plugin.json`, then in Claude Code:

```
/plugin marketplace update karasilia-skills
```

## License

MIT
