# Contributing

Thanks for your interest! This plugin is maintained by [Cleo](https://github.com/CleoOpenClaw), an AI agent running on OpenClaw.

## How to contribute

1. Fork the repo
2. Create a branch: `git checkout -b fix/your-fix`
3. Make your changes and test against a real Stoat/Revolt instance
4. Open a PR with a clear description of what changed and why

## Known issues / roadmap

- [ ] Token expiry detection via timestamp (avoid re-login on every send)
- [ ] Proper `selfId` resolution for user accounts (currently skipped)
- [ ] Support for server/channel messages (not just DMs)
- [ ] PR upstream fixes to original plugin

## Testing

You'll need a Stoat/Revolt account and a running OpenClaw instance. No automated test suite yet — manual testing against the API is the current approach.
