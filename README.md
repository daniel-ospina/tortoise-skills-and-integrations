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
- **Codex:** `.agents/skills/` (project) — Codex's documented skill root ([#2329](https://github.com/daniel-ospina/tortoise/issues/2329)); the same path the official installer writes
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

## Where to edit what

Tortoise consumer artifacts live in **two** repositories. Editing the wrong one
is a drift, not a fork: the copy served at `app.premiselabs.co` is **derived**,
and a fail-closed parity gate in the Tortoise repo keeps the two byte-identical.

| Artifact | Authored in | How it reaches a customer |
|---|---|---|
| the three skills under `skills/` | **this repo** | mirrored byte-for-byte into [`daniel-ospina/tortoise`](https://github.com/daniel-ospina/tortoise) at `website/apps/dashboard/public/skills/` and served at `app.premiselabs.co/skills/<name>/SKILL.md`. The pin is `config/served-skills-upstream.yml` in that repo; `tools/served_skills_parity.py --sync` re-derives the mirror ([#4643](https://github.com/daniel-ospina/tortoise/issues/4643)) |
| `install-tortoise-skills.sh` | [`daniel-ospina/tortoise`](https://github.com/daniel-ospina/tortoise) → `website/apps/dashboard/public/install-tortoise-skills.sh` | install with the curl one-liner above. The copy in this repo is a stale leftover — its source of truth was deliberately moved out of here ([#3324](https://github.com/daniel-ospina/tortoise/issues/3324)); tracked by [#8747](https://github.com/daniel-ospina/tortoise/issues/8747) |
| `tortoise-onboarding` | `daniel-ospina/tortoise` → `tortoise/onboarding/SKILL.md` | served at `app.premiselabs.co/skills/tortoise-onboarding/SKILL.md`. It is a one-time setup flow delivered as instructions, **not** one of the three reusable capabilities, and never a skill this repo authors ([#4365](https://github.com/daniel-ospina/tortoise/issues/4365)) |

**To change a skill:** edit it here, then — in the Tortoise repo — run
`uv run python tools/served_skills_parity.py --sync` and commit the mirrored
skills together with the pin. A run that skips that step reds the parity gate
rather than serving the stale copy.

## License

[MIT](LICENSE) — free to use, modify, and redistribute. The skills are distributed from the Tortoise product site (`app.premiselabs.co`); this repo is the public source of truth for the three skills under `skills/`.
