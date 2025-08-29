# macOS Setup Guide

This guide covers installing prerequisites and running the MCP Server for Splunk on macOS.

## 1) Clone the repository

```bash
git clone https://github.com/deslicer/mcp-for-splunk.git
cd mcp-for-splunk
# Checkout dev1666 branch in git, this branch has a prepared .env file for you.
git checkout dev1666
```

All setup scripts are in this repository under `scripts/`.

## 2) Check and install prerequisites (smart)

### 2.2 Check install (dry-run)

```bash
./scripts/smart-install.sh --dry-run
```

Review what would be installed, then run the installer to apply changes:

### 2.3 Install missing prerequisites

```bash
./scripts/smart-install.sh
```

### 2.4 Run the checker to confirm

```bash
./scripts/check-prerequisites.sh
```


## All checks pass ✅

- ***Return to: [Main Guide](../../set-up-your-mcp-server-for-splunk.md#2-prepare-your-environment)***


## Troubleshooting ⚠️

- If `uv` not found: `brew install uv`
- If Docker commands fail: ensure Docker Desktop is running
- Permission denied on scripts: `chmod +x ./scripts/*.sh`
