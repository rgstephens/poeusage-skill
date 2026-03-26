# poeusage Skill

![Version](https://img.shields.io/github/v/tag/rgstephens/poeusage-skill?label=version&sort=semver)

A [ClawHub](https://clawhub.ai/rgstephens/poeusage-skill) skill for monitoring your Poe API point balance and usage history from the terminal using the `poeusage` CLI.

## Installation

```bash
brew tap rgstephens/tap
brew install poeusage
```

## Commands

| Command | Description |
|---------|-------------|
| `poeusage balance` | Fetch and display current point balance |
| `poeusage history` | Fetch usage history with filtering and pagination |
| `poeusage summary` | Aggregate usage and display cost breakdown |
| `poeusage completion <shell>` | Generate shell completion script |

## Global Flags

| Flag | Description |
|------|-------------|
| `--api-key` | Poe API key (default: `$POE_API_KEY`) |
| `--json` | Output raw JSON |
| `--plain` | Plain/CSV output |
| `--no-color` | Disable color output |
| `-q, --quiet` | Suppress non-essential output |
| `-v, --verbose` | Verbose output |
| `--timeout` | Request timeout in seconds (default: 30) |

## Examples

```bash
# Check current balance
poeusage balance
poeusage balance --plain        # outputs: 1500
poeusage balance --json         # outputs: {"current_point_balance":1500}

# View usage history
poeusage history
poeusage history --bot Claude-3.5-Sonnet --since 2024-01-01
poeusage history --format csv --limit 50

# Summarize usage by bot
poeusage summary --group-by bot
poeusage summary --group-by day --since 2024-01-01

# Shell completion
poeusage completion zsh > ~/.zsh/completions/_poeusage
```

## Configuration

Priority order: flags > env vars > config file > defaults

### Environment Variables

| Variable | Description |
|----------|-------------|
| `POE_API_KEY` | Poe API key |
| `NO_COLOR` | Disable color output |
| `POEUSAGE_TIMEOUT` | Request timeout in seconds |
| `POEUSAGE_PAGE_SIZE` | Page size for history requests |

### Config File

`~/.config/poeusage/config.toml`

```toml
# api_key = "..." # not recommended
timeout = 30
page_size = 100
```

## Exit Codes

| Code | Meaning |
|------|---------|
| `0` | Success |
| `1` | Runtime error (network/API error) |
| `2` | Invalid usage |
| `3` | Auth error (401) |

## Releases

See [GitHub Releases](https://github.com/rgstephens/poeusage-skill/releases) for changelog and version history.
