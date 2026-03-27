# openclaw-plugin-stoat 🦎

A [Stoat](https://stoat.chat) / [Revolt](https://revolt.chat) channel plugin for [OpenClaw](https://github.com/openclaw/openclaw) — WebSocket + REST hybrid with full bidirectional messaging.

> **Note:** This is a fork/rewrite of [robbyczgw-cla/openclaw-plugin-stoat](https://github.com/robbyczgw-cla/openclaw-plugin-stoat) with significant fixes for user account auth (as opposed to bot tokens).

## Features

- 🔌 **WebSocket Primary** — Real-time message delivery via Revolt's WebSocket API
- 🔄 **REST Polling Fallback** — Automatic polling when WebSocket disconnects
- 🔑 **Email/Password Auth** — Logs in automatically on startup, no pre-set token needed
- 🔁 **Auto Token Refresh** — Re-authenticates when session tokens expire
- 💬 **DM Support** — Direct messages with proper per-channel session routing
- 🖼️ **Image Support** — Inbound + outbound attachments via Revolt's Autumn file server
- ⌨️ **Typing Indicators** — Shows typing status before replies
- 💓 **Ping Keepalive** — Proactive 30s pings to prevent server-side disconnects

## Installation

```bash
mkdir -p ~/.openclaw/extensions/stoat
curl -s https://raw.githubusercontent.com/cleofamiliar/openclaw-plugin-stoat/main/index.js > ~/.openclaw/extensions/stoat/index.js
curl -s https://raw.githubusercontent.com/cleofamiliar/openclaw-plugin-stoat/main/package.json > ~/.openclaw/extensions/stoat/package.json
curl -s https://raw.githubusercontent.com/cleofamiliar/openclaw-plugin-stoat/main/openclaw.plugin.json > ~/.openclaw/extensions/stoat/openclaw.plugin.json

# Link the openclaw SDK
mkdir -p ~/.openclaw/extensions/stoat/node_modules
ln -sf $(npm root -g)/openclaw ~/.openclaw/extensions/stoat/node_modules/openclaw
```

## Configuration

Add to `~/.openclaw/openclaw.json`:

```json
{
  "channels": {
    "stoat": {
      "enabled": true,
      "email": "your-agent@example.com",
      "password": "your-password",
      "wsBase": "wss://events.stoat.chat",
      "apiBase": "https://api.stoat.chat",
      "autumnBase": "https://autumn.stoat.chat"
    }
  },
  "plugins": {
    "entries": {
      "stoat": { "enabled": true }
    }
  },
  "session": {
    "dmScope": "per-channel-peer"
  }
}
```

Then restart the gateway:

```bash
openclaw gateway restart
```

## Key Differences from Original

- **User account auth** instead of bot token — Stoat's API rejects `x-bot-token` header for user accounts; this plugin uses `x-session-token` only
- **Email/password login** on startup — no need to manually set/rotate session tokens
- **Automatic token refresh** — re-authenticates when the session expires mid-run
- **storePath routing fix** — inbound messages correctly route to the OpenClaw agent session
- **per-channel-peer sessions** — Stoat DMs get their own session scope, separate from TUI

## Self-Hosted Revolt

Works with self-hosted Revolt instances:

```json
{
  "channels": {
    "stoat": {
      "email": "agent@example.com",
      "password": "password",
      "apiBase": "https://your-revolt.example.com/api",
      "wsBase": "wss://your-revolt.example.com/ws",
      "autumnBase": "https://your-revolt.example.com/autumn"
    }
  }
}
```

## License

MIT
