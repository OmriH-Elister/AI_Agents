---
name: network-sysadmin-optimizer
description: Perform routine system maintenance and performance optimization on Windows and Linux hosts over the network. Use when Codex needs to clean temporary files, run integrity checks, inspect disk health, apply OS updates, handle routine monthly maintenance passes, or produce a host-by-host maintenance summary for one or more servers or workstations.
---

# Network Sysadmin Optimizer

## Overview

Perform cautious, repeatable maintenance on remote Windows and Linux hosts. Verify identity, OS, risk, and access first; then run the OS-specific routine, stop on critical errors, and end with a structured summary of completed work, findings, and follow-up actions.

## Local Context

- Read `references/local-access.md` before connecting if credentials, preferred remoting tools, host inventory, or environment conventions are not already in the task context.
- Treat secrets as external inputs. Load passwords or tokens from a secure source at runtime, store them in shell variables when needed, and never copy them into reports, transcripts, or new skill files.
- Confirm whether the user wants a single-host task, a shortlist of hosts, or a network-wide maintenance sweep. Do not broaden scope without approval.

## Workflow

1. Clarify scope and risk
- Capture the target hosts, maintenance window, and whether reboots are allowed.
- Ask whether any host is production or serving live users if that is not already clear.
- Confirm whether discovery or scanning is allowed before attempting to enumerate additional hosts.

2. Rebuild connection context
- Confirm hostname and IP address for each target.
- Verify connectivity and authenticate with the least risky supported remoting method for that host.
- Identify the OS and version before choosing commands.

3. Run pre-maintenance checks
- Check for active users, critical processes, or obvious signs that cleanup or updates could be disruptive.
- If the host appears production, confirm it is safe to continue before doing anything that could cause downtime.
- Start a per-host action log with timestamps, commands, outputs, and decisions.

4. Execute the Windows routine when the host is Windows
- Run `sfc /scannow`.
- Run `chkdsk C:` and schedule it for reboot if the volume is locked; tell the user if a reboot is required.
- Run `chkntfs C:` and flag anomalies.
- Check disk media type first. Run `defrag C:` only when the volume is not on SSD media.
- Clear user temp files from `$env:TEMP`.
- Clear system temp files from `$env:SYSTEMROOT\\Temp`.
- Run `DISM /Online /Cleanup-Image /RestoreHealth`.
- Empty the Recycle Bin with `Clear-RecycleBin -Force`.

5. Apply Windows guardrails
- Stop and report before continuing if `sfc` or `chkdsk` reports critical corruption.
- Do not delete outside standard temp locations or the Recycle Bin unless the user explicitly approves it.
- Escalate immediately if DISM cannot repair the image.
- Keep all work in an elevated administrative context.

6. Execute the Linux routine when the host is Linux
- Treat Debian and Ubuntu systems as the default path unless detection shows otherwise.
- Check whether important processes are using `/tmp` before deleting temp files.
- Clear temporary files from `/tmp` only after that safety check.
- Run `apt update`, `apt upgrade -y`, `apt full-upgrade -y`, `apt autoclean`, and `apt autoremove -y` with appropriate privilege escalation.

7. Apply Linux guardrails
- If the distribution is not Debian or Ubuntu, identify the package manager and either adapt safely or stop and ask the user how to proceed.
- Report held packages, dependency conflicts, or package manager locks instead of hiding them.
- If a kernel update or another change requires reboot, tell the user and confirm before scheduling or executing it.

8. Finish with a per-host report
- Report host, OS, tasks completed, issues found, actions required, and final status.
- For multi-host work, include connectivity failures and hosts skipped for safety reasons.
- Call out any follow-up items such as reboot requirements, corruption findings, failed updates, or unresolved package issues.

## Reporting Format

Use this structure for each host:

- `Host`: hostname or IP
- `OS`: detected OS and version
- `Tasks Completed`: concise list
- `Issues Found`: errors, warnings, or anomalies
- `Actions Required`: reboot, follow-up, escalation, or none
- `Status`: completed, completed with warnings, failed, or deferred

## Guardrails

- Ask before disruptive actions, including reboots, service restarts, broad host discovery, or maintenance on confirmed production systems.
- Never expose passwords, tokens, or copied commands that contain secrets.
- Never suppress errors silently. Capture them, summarize them, and decide explicitly whether it is safe to continue.
- Do not modify network devices, firewall policy, routing, user accounts, permissions, or security settings as part of routine maintenance unless the user explicitly expands scope.
- If a host cannot be reached, record the failure and continue only if that matches the approved scope.

## Reference

- `references/local-access.md`
