# OPENCLAW QUICK [INSTALL AND USE GUIDE](https://dazzaji.github.io/OpenClawGuide/)

____________

Here’s a clean, copy‑pasteable cold‑start for a Mac, using your Claude plan and the current native installer flow (not npm).

## 1. Basic macOS prep

Open Terminal (Spotlight → “Terminal”) and run:

```bash
# 1) Make sure Xcode CLT and Homebrew are ready (safe to re-run on any Mac)
xcode-select --install 2>/dev/null || echo "Xcode CLT already installed or install dialog shown"

# 2) Install Homebrew if missing (this is the official script)
which brew >/dev/null 2>&1 || /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

That’s expected on a fresh Mac—you don’t have Homebrew yet. Here’s the exact fix; just continue from where you are.

## 1. Install Homebrew (since it’s missing)

In Terminal, run:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```


Let it finish; it may ask for your Mac password (for /usr/local or /opt/homebrew).

### 1.1 Confirm Brew is working

In Terminal:

```bash
brew --version
```

If you see `Homebrew 5.8.12` (or similar), Brew itself is fine. [mac.install](https://mac.install.guide/homebrew/3)

### 1.2 Add Homebrew to PATH the *right* way

Run exactly these two commands (they will create `~/.zprofile` if missing and set things up correctly):

```bash
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv)"
```


Now verify that your PATH contains Homebrew and that `brew` still works:

```bash
echo $PATH
brew help
```


If both commands succeed (no “no such file or dir” messages), you’re good—go back to the Claude Code step:

```bash
curl -fsSL https://code.claude.com/install.sh | bash
```


## 1.3 Add Homebrew to your PATH (Apple Silicon default)

Still in Terminal, run:

```bash
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv)"
```


Now confirm:

```bash
brew --version
```


If that prints a version number, Homebrew is installed correctly and you can go back to the Claude Code steps (starting with the `curl https://code.claude.com/install.sh | bash` command).


On Apple Silicon, add Homebrew to PATH (if needed):

```bash
# Add Homebrew to PATH for zsh (Apple Silicon default prefix)
/opt/homebrew/bin/brew --version >/dev/null 2>&1 || echo "Homebrew may already be on PATH"
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv)"
```


## 2. Install Claude Code (native CLI)

Use the official install script (Anthropic has not removed it yet, but now also documents native/Homebrew as primary). Run:

```bash
# Official Claude Code installer for macOS / Linux / WSL
curl -fsSL https://code.claude.com/install.sh | bash
```


Then, ensure `claude` is on your PATH (the installer prints its export; on a fresh zsh Mac we fix it explicitly):

```bash
# Ensure ~/.claude/bin is on PATH for zsh logins
echo 'export PATH="$HOME/.claude/bin:$PATH"' >> ~/.zprofile
export PATH="$HOME/.claude/bin:$PATH"

# Confirm install
claude --version
```


If that prints a version, you’re good.

## 3. Link your Claude account

Run the sign‑in flow once so the CLI is bound to your Claude Max subscription (no API key):

```bash
# Start interactive login
claude
```


In the in‑terminal UI that appears:

- Choose “Sign in with Claude”.  
- Follow the browser link, log in with the Claude account that has Max.  
- Approve terminal access, then return to Terminal. [anthropic](https://www.anthropic.com/engineering/claude-code-best-practices)

When the REPL prompt like `claude>` appears, type `/exit` to return to shell:

```bash
/exit
```


From now on, `claude` uses that linked account and its Max limits, as long as you’re logged in there. [code.claude](https://code.claude.com/docs/en/setup)

## 4. Sanity‑check with simple usage

Make a test folder and run Claude Code there:

```bash
mkdir -p ~/code/hello-claude
cd ~/code/hello-claude

# Start Claude Code with confirmation prompts ON (safe mode)
claude
```


At the `claude>` prompt, try:

```text
Scan this empty project, then create a README.md explaining what this repo is for.
```


Let it propose changes; accept them when prompted. Confirm files:

```bash
ls
cat README.md
```


## 5. “All permissions dangerously” variant

Once you’re comfortable and in a **sandboxed** repo (no secrets), you can run with full access:

```bash
cd ~/code/your-project

# Full tools, no permission prompts (dangerous)
claude --dangerously-skip-permissions
```


At the `claude>` prompt, you can immediately give it a mission, or pre-seed with a first prompt:

```bash
claude --dangerously-skip-permissions "You are my repo agent. First, scan this project, summarize it, then propose a 3–5 item plan."
```


## 6. Optional: headless mode for scripts

For automations / CI without the REPL:

```bash
cd ~/code/your-project

# Simple headless prompt
claude -p "Generate a .gitignore for a Node.js project" > .gitignore

# Analyze a file from stdin
cat src/index.ts | claude -p "Find potential bugs and suggest fixes"
```


You now have Claude Code installed, authenticated to your Claude Max plan, and runnable both interactively and headless from a totally fresh Mac.

You can use Claude Code to guide you through OpenClaw and all the questions and ideas you will have.  


____________

# Now Install OpenClaw

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

_____________

## ENJOY ME IN MY HOMETOWN [GITHUB REPO](https://github.com/dazzaji/OpenClawGuide/blob/main/README.md)
