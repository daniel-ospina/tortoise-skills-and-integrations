# Tortoise Skills & Integrations

The official agent skills for working with [Tortoise](https://github.com/daniel-ospina/tortoise) — the epistemic graph engine. Install them into your AI agent's skills directory to let it read, write, and reason over your Tortoise graph.

## Skills

| Skill | Type | What it does |
|---|---|---|
| `how-to-use-tortoise` | passive | Read and write the graph — points, operators, mitigations, NANDs, supersede, delete, annotate. Your agent loads it automatically when installed. |
| `tortoise-decide` | invoke | Make a decision with the graph — refine the decision, research options/criteria/findings, wire IMPL/NAND/mitigation edges, rank options by EP confidence. |
| `tortoise-file-finding` | invoke | Ingest a research finding — creates a Point, checks for existing related claims, surfaces connections. |

## Install

Install into your agent's skills directory with one command (project-scoped for Claude Code / Codex / Cursor; personal for Pi):

```bash
curl -fsSL https://app.premiselabs.co/install-tortoise-skills.sh | bash -s -- --harness claude
```

Replace `claude` with `codex`, `cursor`, or `pi` for other agents. Re-running the installer updates the skills in place.

### Manual install

Clone this repo (or download the folders) and copy each skill into your agent's skills directory:

- **Claude Code:** `~/.claude/skills/` (personal) or `.claude/skills/` (project)
- **Codex:** `~/.codex/skills/`
- **Cursor:** `.cursor/skills/` (project)
- **Pi:** `~/.pi/agent/skills/`

```
cp -r skills/how-to-use-tortoise ~/.claude/skills/
cp -r skills/tortoise-decide ~/.claude/skills/
cp -r skills/tortoise-file-finding ~/.claude/skills/
```

## Requirements

- A Tortoise API key (from [app.premiselabs.co](https://app.premiselabs.co)) — the skills talk to the Tortoise API and MCP server.
- The skills are plain `SKILL.md` files conforming to the [Agent Skills open standard](https://agentskills.my/specification/).

## License

[MIT](LICENSE) — free to use, modify, and redistribute. The skills are distributed from the Tortoise product site (`app.premiselabs.co`); this repo is the public source of truth.
