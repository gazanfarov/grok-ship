<h1 align="center">Grok Ship</h1>
<p align="center">
  <a
    href="https://img.shields.io/badge/platform-Grok%20Bot-blue?style=flat-square"
    ><img
      alt="Platform"
      src="https://img.shields.io/badge/platform-Grok%20Bot-blue?style=flat-square"
  /></a>
  <a href="https://x.com/kunchenguid"
    ><img
      alt="X"
      src="https://img.shields.io/badge/X-@kunchenguid-black?style=flat-square"
  /></a>
  <a href="https://discord.gg/Wsy2NpnZDu"
    ><img
      alt="Discord"
      src="https://img.shields.io/discord/1439901831038763092?style=flat-square&label=discord"
  /></a>
</p>

<h3 align="center">Talk to one Firstmate. Ship with a crew.</h3>

## What it is

Grok Ship is an installer pack for Grok Bot.
It is not a standalone app, not a harness, and not a CLI.

You talk to a single agent - Firstmate.
It classifies work as scout or ship, writes it to a local sqlite backlog, and hands software tasks to per-project crewmates.
Those crewmates drive Cursor cloud agents.
A fresh adversarial review reads the pushed branch before any pull request is opened.

Bots never execute on your machine.
They run on the shared Grok Bot computer; project work runs on ephemeral Cursor cloud agents.

## Features

- **One Firstmate** - you talk only to Firstmate; it delegates, escalates real decisions, and reports outcomes.
- **Per-project crewmates** - each project or project area gets a persistent crewmate that drives Cursor cloud agents. Firstmate never launches a cloud agent itself.
- **Scout vs ship** - scout is investigation, diagnosis, planning, or audit, and the deliverable is a report, never a PR. Ship is authorized change. Promoting a scout flips the same task row rather than opening a duplicate.
- **Review before any PR** - after a ship cloud agent pushes a branch, a fresh adversarial-review subagent reads it through the project's forge CLI. No pull request until that pass is clean.
- **Local sqlite backlog** - chat is not the source of truth. Projects and tasks live in a sqlite database on the shared computer.
- **Captain merges** - no bot merges a pull request on its own. Merge only on the captain's explicit word, and never while checks are red.
- **Forge-agnostic** - detect GitHub, GitLab, Bitbucket, or Cursor Origin. Do not assume GitHub.

## Quick Start

Get this pack onto your Grok Bot shared computer, then tell any bot:

```
follow GROK_SHIP.md
```

The installer copies the pack, creates or reuses Firstmate, installs the three global workflows, creates the sqlite database, and hands you over to Firstmate.
Talk only to Firstmate from then on.

```
> look at my project xyz, then fix the flaky login test

# Firstmate files a ship task and hands it to the project crewmate.
# The crewmate drives a Cursor cloud agent; adversarial review
# runs before any pull request.

  PR ready, captain: https://github.com/you/xyz/pull/42

> merge it
```

## How It Works

```
            you (the captain)
                  │  chat: requests, decisions, "merge it"
                  ▼
 ┌─────────────────────────────────────┐
 │ Firstmate                           │
 │ sqlite backlog · scout vs ship      │
 └──┬──────────────┬───────────────┬───┘
    │ messages                     │
    ▼              ▼               ▼
 ┌────────┐   ┌────────┐      ┌────────┐
 │crewmate│   │crewmate│      │crewmate│   one per project
 └───┬────┘   └───┬────┘      └───┬────┘
     ▼            ▼               ▼
  Cursor cloud agents
     │
     ├─ ship: branch ► adversarial review ► PR ► captain merge
     │
     └─ scout: report, never a PR
```

You chat with Firstmate.
It writes a task row, delegates to the crewmate whose charter fits, and relays results as they land.
Software goes through a project crewmate and a Cursor cloud agent, never through Firstmate directly.
Scout reports land on the shared computer.
Ship work is reviewed on the pushed branch before a pull request is opened.

## Pack skills

This pack installs three global workflows:

| Skill | What it does |
| ----- | ------------ |
| [Lavish session](skills/lavish-session/SKILL.md) | Turns complex or visual responses into HTML artifacts the captain can annotate, using lavish-axi on the shared computer. |
| [Adversarial review](skills/adversarial-review/SKILL.md) | Reviews a pushed ship branch before any pull request. `auto-fix` goes back to the cloud agent; `ask-user` becomes a captain decision; `error` blocks the raise. |
| [Project management](skills/project-management/SKILL.md) | Local sqlite backlog for projects and tasks. Used at intake and whenever work is handed to a crewmate. |

The rest of the pack is [`GROK_SHIP.md`](GROK_SHIP.md) (installer), [`GROK_BOT_FIRSTMATE.md`](GROK_BOT_FIRSTMATE.md) (Firstmate charter), and [`GROK_BOT_CREWMATE.md`](GROK_BOT_CREWMATE.md) (per-project crewmate charter).

## License

MIT - see [LICENSE](LICENSE).
