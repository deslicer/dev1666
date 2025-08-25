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

## 2) Install prerequisites

Install Homebrew (if you don't have it):

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Install required tools:

```bash
brew install python@3.11 uv git
# Optional (for MCP Inspector)
brew install node
# Optional (Docker mode)
brew install --cask docker
```

Verify installations:

```bash
python3 --version
uv --version
git --version
node --version  # if installed
docker --version  # if installed
```

## 3) Validate prerequisites

From the `mcp-for-splunk` folder:

```bash
./scripts/check-prerequisites.sh --detailed
```

When all checks pass, continue to the next step in the main guide:

- Return to: [Main Guide](../../set-up-your-mcp-server-for-splunk.md#2-prepare-your-environment)

## Troubleshooting (macOS prerequisites)

- If `uv` not found: `brew install uv`
- If Docker commands fail: ensure Docker Desktop is running
- Permission denied on scripts: `chmod +x ./scripts/*.sh`
