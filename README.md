# FargoRate Skill

![Version](https://img.shields.io/github/v/tag/rgstephens/fargo-skill?label=version&sort=semver)

A [ClawHub](https://clawhub.ai/rgstephens/fargo-skill) skill for the [FargoRate](https://fargorate.com) billiards rating system. Look up players, calculate match odds, get recommended race lengths, and track rating changes over time.

## Installation

```bash
brew tap rgstephens/fargo
brew install fargo
```

## Commands

| Command | Description |
|---------|-------------|
| `fargo search <name or id>` | Search players by name or FargoRate ID |
| `fargo lookup <id>` | Look up a single player by ID |
| `fargo bulk <id...>` | Look up multiple players at once |
| `fargo odds <r1> <r2> <race1> <race2>` | Calculate match win odds |
| `fargo races <r1> <r2>` | Get recommended race lengths |
| `fargo top` | View top 10 ranked players |
| `fargo setup` | Configure the tool |
| `fargo group` | Manage named groups of player IDs |

## Global Flags

| Flag | Description |
|------|-------------|
| `--db [path]` | Save player data to a local SQLite database |
| `--changes` | Only output players whose rating changed (requires `--db`) |
| `--json` | Output raw JSON |

## Examples

```bash
fargo search "John Smith"
fargo odds 550 480 7 9
fargo races 550 480 --type 0
fargo top --ranking US --gender F
fargo --changes --db bulk --group monday-league
```

## Releases

See [GitHub Releases](https://github.com/rgstephens/fargo-skill/releases) for changelog and version history.

## ToDo

- Improve fargo skill cli description to help weaker bots

### Example CLI Use Issue

Prompt: give me a table of everyone in the monday group with their rating and robustness. 

```log
nanobot-gateway  | 2026-03-11 15:47:49.149 | INFO     | nanobot.agent.loop:_run_agent_loop:230 - Tool call: exec({"command": "fargo --db group show monday --json 2>&1"})
nanobot-gateway  | 2026-03-11 15:47:57.151 | INFO     | nanobot.agent.loop:_run_agent_loop:230 - Tool call: exec({"command": "fargo --db player show 1324244 --json 2>&1"})
nanobot-gateway  | 2026-03-11 15:48:01.494 | INFO     | nanobot.agent.loop:_run_agent_loop:230 - Tool call: exec({"command": "fargo --help 2>&1"})
nanobot-gateway  | 2026-03-11 15:48:03.670 | INFO     | nanobot.agent.loop:_run_agent_loop:230 - Tool call: exec({"command": "fargo bulk --help 2>&1"})
nanobot-gateway  | 2026-03-11 15:48:08.793 | INFO     | nanobot.agent.loop:_run_agent_loop:230 - Tool call: exec({"command": "fargo bulk --group monday --json --db /root/.nanobot/workspace/fargo.db 2>&1"})
nanobot-gateway  | 2026-03-11 15:48:16.989 | INFO     | nanobot.agent.loop:_run_agent_loop:230 - Tool call: exec({"command": "fargo bulk --group monday --db /root/.nanobot/workspace/fargo.db --json 2>&1"})
nanobot-gateway  | 2026-03-11 15:48:20.816 | INFO     | nanobot.agent.loop:_run_agent_loop:230 - Tool call: exec({"command": "fargo group show monday --db /root/.nanobot/workspace/fargo.db --json 2>&1"})
nanobot-gateway  | 2026-03-11 15:48:32.122 | INFO     | nanobot.agent.loop:_run_agent_loop:230 - Tool call: exec({"command": "fargo --db /root/.nanobot/workspace/fargo.db group show monday --json 2>&1"})
nanobot-gateway  | 2026-03-11 15:48:34.656 | INFO     | nanobot.agent.loop:_run_agent_loop:230 - Tool call: exec({"command": "fargo group show monday --db /root/.nanobot/workspace/fargo.db 2>&1"})
nanobot-gateway  | 2026-03-11 15:48:41.022 | INFO     | nanobot.agent.loop:_run_agent_loop:230 - Tool call: exec({"command": "fargo --db /root/.nanobot/workspace/fargo.db group show monday 2>&1"})
nanobot-gateway  | 2026-03-11 15:48:47.857 | INFO     | nanobot.agent.loop:_run_agent_loop:230 - Tool call: exec({"command": "fargo group show monday --db=/root/.nanobot/workspace/fargo.db 2>&1"})
nanobot-gateway  | 2026-03-11 15:48:51.980 | INFO     | nanobot.agent.loop:_run_agent_loop:230 - Tool call: exec({"command": "fargo bulk 1115327 1119367 1119369 1119371 1119377 1119383 1119384 1132833 1137501 1179210 1190373 1191948 1207397 1209675 1215491 1215492 1277009 1324244 1324636 1327664 1337835 1341511 )
```