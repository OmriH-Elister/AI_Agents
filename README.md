# AI_Agents

Agent and skill definitions for specialized security and systems administration workflows.

This repository is a content repo, not an application. It contains Markdown specifications with YAML front matter: Claude-style agent definitions, plus one Codex-style skill variant.

## Repository Layout

```text
.
├── network-sysadmin-optimizer/
│   └── network-sysadmin-optimizer.md
├── network-sysadmin-optimizer-codex/
│   ├── SKILL.md
│   ├── agents/
│   │   └── openai.yaml
│   └── references/
│       └── local-access.md
├── psych-pro/
│   └── psych-pro.md
├── soc-engineer/
│   └── homelab-soc-engineer.md
├── LICENSE
└── README.md
```

## Included Agents

### `network-sysadmin-optimizer`

Network maintenance agent for routine Windows and Linux host upkeep. The definition focuses on safe, structured operational work such as integrity checks, temporary file cleanup, package updates, and post-maintenance reporting.

Path: `network-sysadmin-optimizer/network-sysadmin-optimizer.md`

### `network-sysadmin-optimizer` (Codex variant)

The same capability expressed as a Codex skill rather than a Claude agent: a `SKILL.md` with a procedural body, an `agents/openai.yaml` describing how it surfaces in the Codex interface, and a `references/local-access.md` template for environment details that must stay out of the definition itself.

Path: `network-sysadmin-optimizer-codex/`

### `homelab-soc-engineer`

Home-lab SOC and defensive security agent for Wazuh-based alert triage, vulnerability review, host investigation, and incident-response style reporting across a LAN environment.

Path: `soc-engineer/homelab-soc-engineer.md`

### `psych-pro`

Comprehensive psychological analysis agent combining structured personality profiling with depth-psychological (Sherlock-Holmes-meets-Freud) unconscious pattern analysis. Orchestrates two skills — `psych-profiler` and `sherlock-freud-mind-modeler` — from the [LLM_Skills](https://github.com/OmriH-Elister/LLM_Skills) repo, both adapted from [Fabric](https://github.com/danielmiessler/fabric) patterns (see those skills' Attribution sections for credit and license details).

Path: `psych-pro/psych-pro.md`

## How To Use

Because this repo contains agent definitions rather than executable code, usage depends on your agent runner.

Typical workflow:

1. Clone this repository.
2. Pick the agent definition you want to use.
3. Copy or register the relevant `.md` file in your Claude or agent-tooling workspace.
4. Invoke the agent by the name declared in its front matter.

## Authoring Conventions

Two conventions currently coexist here.

Claude-style agent definitions use `<name>/<name>.md`:

- YAML front matter for agent metadata such as `name`, `description`, `model`, and related resources
- A plain-language system prompt body describing operating rules, workflows, and reporting expectations

Codex-style skills use `<name>/SKILL.md`:

- Minimal front matter, `name` and `description` only
- A procedural body under `## Overview` and `## Local Context`
- Environment specifics deferred to `references/`, never inlined into the definition

If you add new definitions, keep the directory name identical to the `name` in the front matter so the repo stays easy to browse and portable across runtimes.

## Security Note

These files are prompt artifacts and should be reviewed before reuse in any shared or public environment. Do not store real credentials, secrets, or environment-specific sensitive details in agent definitions unless the repository is explicitly private and governed appropriately.

## License

This project is licensed under the terms of the `LICENSE` file in the repository root.
