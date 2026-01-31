# OPENCLAW QUICK INSTALL AND USE

## A quick, easy, good setup plan for a clean MacBook (official-docs only)

### 1) Install OpenClaw

If you already have Node/npm, the docs explicitly allow global npm install: ([OpenClaw][1])

```bash
npm install -g openclaw@latest
```

If you want the “installer script” that also handles Node 22+ checks and common gotchas, use the official installer: ([OpenClaw][5])

```bash
curl -fsSL https://openclaw.bot/install.sh | bash
```

### 2) Run onboarding and install the background service (launchd)

This is the documented “do this next” step on macOS: ([OpenClaw][1])

```bash
openclaw onboard --install-daemon
```

Notes from the official getting-started doc:

* it walks you through local vs remote gateway, provider auth, and installs the daemon/service. ([OpenClaw][1])

### 3) Verify it’s healthy

Official “after install” checks are: ([OpenClaw][2])

```bash
openclaw doctor
openclaw gateway status
openclaw gateway status --deep
```

### 4) (Optional but recommended on macOS) Install/Open the macOS Companion

If you want the most frictionless Mac experience (permissions, launchd control, mac-only tools), the official macOS Companion app is designed for that. ([OpenClaw][4])

---

[1]: https://docs.openclaw.ai/start/getting-started?utm_source=chatgpt.com "Getting started - OpenClaw"
[2]: https://docs.openclaw.ai/install/index?utm_source=chatgpt.com "Index - OpenClaw"
[3]: https://docs.openclaw.ai/gateway?utm_source=chatgpt.com "Index - OpenClaw"
[4]: https://docs.openclaw.ai/macos?utm_source=chatgpt.com "Macos - OpenClaw"
[5]: https://docs.openclaw.ai/install/installer?utm_source=chatgpt.com "Installer - OpenClaw"
