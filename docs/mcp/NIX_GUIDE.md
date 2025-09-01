# Unix (macOS & Linux) Setup Guide

This guide covers installing prerequisites and running the MCP Server for Splunk on macOS and Linux.

## 1) Clone the repository

```bash
mkdir ~/dev1666
cd ~/dev1666
git clone https://github.com/deslicer/mcp-for-splunk.git
cd mcp-for-splunk
# Checkout dev1666 branch in git, this branch has a prepared .env file for you.
git checkout dev1666
```

All setup scripts are in this repository under `scripts/`.

## 2) Check and install prerequisites (smart)

### 2.1 Check install (dry-run)

```bash
./scripts/smart-install.sh --dry-run
```

Review what would be installed, then run the installer to apply changes:

### 2.2 Install missing prerequisites

```bash
./scripts/smart-install.sh            # base: Python, uv, Git, Node.js
# ./scripts/smart-install.sh --all    # base + docker and docker compose
```

### 2.3 Run the checker to confirm

```bash
./scripts/check-prerequisites.sh --detailed
```

<details>
<summary>Manual checks</summary>
```bash
python3 --version
uv --version
git --version
node --version
docker --version       # if installed
docker compose version # if installed
```
</details>

## All checks pass ✅

- ***Return to: [Main Guide](../../set-up-your-mcp-server-for-splunk.md#2-prepare-your-environment)***

## Troubleshooting ⚠️

- If `uv` not found after install, ensure `~/.cargo/bin` is in your PATH
- If Docker requires sudo: add your user to `docker` group and re-login (Linux)
- If Docker commands fail on macOS: ensure Docker Desktop is running
- Permission denied on scripts: `chmod +x ./scripts/*.sh`
