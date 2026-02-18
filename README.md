# 🦞 OpenClaw Runtime Directory

The `~/.openclaw` directory contains the local runtime, configuration, and secure state for the OpenClaw AI agent framework.

It powers AI agents, browser automation, gateway execution, scheduling, and device-based authentication — all in a local-first architecture.

---

## ✨ Overview

OpenClaw provides:

- 🤖 Multi-model AI agent orchestration  
- 🌐 Chrome automation via CDP relay  
- ⚙️ Local gateway server (`localhost:18789`)  
- 🔐 Secure device identity (Ed25519)  
- 📅 Scheduled task execution  
- 🧠 Persistent session storage  

This directory is generated during `openclaw setup`.

---

## 📂 Structure

```
~/.openclaw/
├── agents/            # Agent configs & sessions
├── browser/           # Chrome extension & profile
├── credentials/       # API keys (private)
├── identity/          # Device identity & keys
├── cron/              # Scheduled jobs
├── logs/              # Runtime logs
└── openclaw.json      # Main configuration
```

---

## ⚙️ Configuration

`openclaw.json` defines:

- Default AI model
- Workspace directory
- Concurrency limits
- Gateway mode (`local`)
- Port configuration (`18789`)
- Provider authentication settings

Backups are automatically maintained (`.bak` files).

---

## 🔐 Security

- Gateway binds to localhost only  
- Token-based authentication  
- Isolated browser profile  
- Credentials excluded from version control  

⚠️ Do **not** commit this directory.

---

## 🚀 Common Commands

```bash
openclaw setup
openclaw doctor
openclaw gateway start
openclaw agents status
```

---


## 📄 License

Licensed under the **MIT License**.  
See the `LICENSE` file for details.
