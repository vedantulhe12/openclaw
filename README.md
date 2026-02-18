# OpenClaw Configuration Directory

This directory (`~/.openclaw`) contains user-level configuration, credentials, sessions, and runtime data for the OpenClaw AI agent framework.

## Overview

OpenClaw is an intelligent agent framework that enables AI-powered automation, browser control, task scheduling, and multi-model orchestration. This configuration directory manages:

- Agent configurations and sessions
- Authentication profiles and device identity
- Browser automation extensions
- Gateway server settings
- Cron jobs and scheduled tasks
- Shell completions and CLI integrations

## Directory Structure

```
~/.openclaw/
├── agents/                    # Agent configurations and sessions
│   └── main/
│       ├── agent/            # Agent-specific auth profiles
│       └── sessions/         # Session history (.jsonl files)
├── browser/                  # Browser automation components
│   ├── chrome-extension/     # Chrome extension for CDP relay
│   └── openclaw/             # Managed Chrome user data
├── completions/              # Shell completion scripts
│   ├── openclaw.bash
│   ├── openclaw.fish
│   ├── openclaw.ps1
│   └── openclaw.zsh
├── credentials/              # API keys and auth tokens
├── cron/                     # Scheduled job definitions
├── devices/                  # Device pairing data
├── identity/                 # Device identity and cryptographic keys
│   ├── device.json          # Device ID and Ed25519 keypair
│   └── device-auth.json     # Authentication state
├── logs/                     # Audit logs and config changes
├── openclaw.json            # Main configuration file
└── .gitignore               # Git ignore patterns
```

## Key Configuration Files

### `openclaw.json`

The primary configuration file containing:

- **Browser Settings**: Path to Chrome executable
- **Auth Profiles**: API key configurations for providers (OpenRouter, OpenAI, etc.)
- **Agent Defaults**: 
  - Primary model: `openai/gpt-4o-mini` (via OpenRouter)
  - Workspace location
  - Concurrency limits
  - Compaction mode
- **Gateway Settings**: 
  - Port: `18789`
  - Mode: `local`
  - Token-based authentication
  - Command restrictions
- **Hooks & Skills**: Internal monitoring and session memory

### `identity/device.json`

Device identity with Ed25519 cryptographic keypair for secure device authentication and pairing.

### `browser/chrome-extension/`

Chrome extension that enables OpenClaw to control browser tabs via Chrome DevTools Protocol (CDP):

- **Purpose**: Attach OpenClaw agents to existing Chrome tabs
- **Relay Server**: Connects to `http://127.0.0.1:18792`
- **Features**: Tab debugging, CDP event forwarding, remote browser automation

### `agents/main/sessions/`

Persistent conversation history stored as JSONL files. Each session tracks:

- Message history
- Tool invocations
- Skill usage
- Compaction state

## Features

### 🤖 Multi-Model AI Agent System

- **Primary Model**: OpenRouter integration with GPT-4o-mini
- **Fallback Support**: Configurable model fallbacks
- **Provider Support**: OpenAI, Anthropic, OpenRouter, and custom providers

### 🌐 Browser Automation

- Chrome extension for live tab control
- CDP relay server for remote debugging
- Session attachment/detachment
- Multi-tab management

### 🔐 Security & Authentication

- Device-based authentication with Ed25519 keypairs
- Token-based gateway access
- Device pairing system
- Credential isolation

### ⚙️ Gateway Server

Local API server for agent communication:
- **Default Port**: `18789`
- **Binding**: Loopback only (localhost)
- **Auth Mode**: Token-based
- **Command Restrictions**: Camera, calendar, contacts safeguards

### 📅 Cron Scheduling

Scheduled task execution via `cron/jobs.json` for periodic agent operations.

### 🛠️ Skills System

Modular skill architecture for specialized tasks:
- **healthcheck**: Security auditing and system hardening
- **skill-creator**: Create custom agent skills
- **weather**: Weather data integration

### 🐚 Shell Integration

Auto-completion support for:
- Bash
- Zsh
- Fish
- PowerShell

## Usage

### Setup & Configuration

```bash
# Initial setup
openclaw setup

# Configuration wizard
openclaw onboard

# Configure specific settings
openclaw configure

# Health check
openclaw doctor
```

### Agent Management

```bash
# View agent status
openclaw agents status

# View active sessions
openclaw sessions

# Agent dashboard
openclaw dashboard
```

### Browser Control

```bash
# Install browser extension
openclaw browser extension install

# Get extension path
openclaw browser extension path

# Start relay server (typically runs automatically)
openclaw gateway start
```

### Gateway Control

```bash
# Start gateway server
openclaw gateway start

# Check gateway status
openclaw gateway status

# View logs
openclaw logs gateway
```

## Environment Configuration

Key configuration options in `openclaw.json`:

| Setting | Value | Description |
|---------|-------|-------------|
| `gateway.port` | `18789` | API server port |
| `gateway.mode` | `local` | Local-only or network mode |
| `agents.defaults.workspace` | `/Users/vedant/openclaw_workspace` | Agent working directory |
| `agents.defaults.maxConcurrent` | `4` | Max parallel agent tasks |
| `browser.executablePath` | Chrome path | Browser binary location |

## Security Considerations

- **Credentials**: Stored in `credentials/` - excluded from version control
- **Identity Keys**: Device keypairs in `identity/` - keep secure
- **Gateway Token**: Unique per installation - rotate periodically
- **Browser Sessions**: Isolated user data directory
- **Command Restrictions**: Sensitive commands blocked by default

## Version Management

- **Current Version**: `2026.2.15`
- **Update Check**: Managed via `update-check.json`
- **Backup Files**: Auto-backup with `.bak` suffixes

## Backup & Recovery

Configuration backups are automatically created:
- `openclaw.json.bak` (most recent)
- `openclaw.json.bak.1` through `openclaw.json.bak.4` (rolling history)

To restore from backup:
```bash
cp openclaw.json.bak openclaw.json
openclaw doctor --repair
```

## Troubleshooting

### Gateway Won't Start
```bash
openclaw doctor --repair
openclaw gateway start
```

### Browser Extension Not Connecting
1. Check relay server status
2. Verify port `18792` is accessible
3. Reload extension in Chrome
4. Check extension console logs

### Session Issues
```bash
# Reset specific agent session
openclaw reset --scope sessions

# View logs
openclaw logs
```

## Related Commands

```bash
openclaw --help          # Full command reference
openclaw doctor          # System diagnostics
openclaw config get      # View current config
openclaw config set      # Update configuration
openclaw reset           # Reset components
```

## Development

### Shell Completion Installation

```bash
# Bash
echo 'source ~/.openclaw/completions/openclaw.bash' >> ~/.bashrc

# Zsh
echo 'source ~/.openclaw/completions/openclaw.zsh' >> ~/.zshrc

# Fish
cp ~/.openclaw/completions/openclaw.fish ~/.config/fish/completions/
```

## License & Credits

Part of the OpenClaw AI agent framework.

---

**Last Updated**: 2026-02-17  
**Version**: 2026.2.15  
**Device ID**: `c2f88afd004b5f23e524a2b4d7e2c2411d58a00e6d03c2cda17f6ccd163a1e5b`
