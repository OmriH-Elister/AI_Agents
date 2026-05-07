# AI_Agents

Claude-oriented agent definitions for specialized security and systems administration workflows.

This repository is a content repo, not an application. It contains Markdown agent specifications with YAML front matter.

## Repository Layout

```text
.
├── network-sysadmin-optimizer/
│   └── network-sysadmin-optimizer.md
├── soc-engineer/
│   └── homelab-soc-engineer.md
└── README.md
```

## Included Agents

### `network-sysadmin-optimizer`

Network maintenance agent for routine Windows and Linux host upkeep. The definition focuses on safe, structured operational work such as integrity checks, temporary file cleanup, package updates, and post-maintenance reporting.

Path: `network-sysadmin-optimizer/network-sysadmin-optimizer.md`

### `homelab-soc-engineer`

Home-lab SOC and defensive security agent for Wazuh-based alert triage, vulnerability review, host investigation, and incident-response style reporting across a LAN environment.

Path: `soc-engineer/homelab-soc-engineer.md`

## How To Use

Because this repo contains agent definitions rather than executable code, usage depends on your agent runner.

Typical workflow:

1. Clone this repository.
2. Pick the agent definition you want to use.
3. Copy or register the relevant `.md` file in your Claude or agent-tooling workspace.
4. Invoke the agent by the name declared in its front matter.

## Authoring Conventions

The existing definitions follow a simple pattern:

- YAML front matter for agent metadata such as `name`, `description`, `model`, and related resources
- A plain-language system prompt body describing operating rules, workflows, and reporting expectations

If you add new agents, keep the directory structure consistent so the repo remains easy to browse and portable across runtimes.

## Security Note

These files are prompt artifacts and should be reviewed before reuse in any shared or public environment. Do not store real credentials, secrets, or environment-specific sensitive details in agent definitions unless the repository is explicitly private and governed appropriately.

## License

This project is licensed under the terms of the `LICENSE` file in the repository root.
