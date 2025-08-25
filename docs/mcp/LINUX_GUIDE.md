# Linux Setup Guide

This guide covers installing prerequisites and running the MCP Server for Splunk on Linux.

## 1) Clone the repository

```bash
git clone https://github.com/deslicer/mcp-for-splunk.git
cd mcp-for-splunk
# Checkout dev1666 branch in git, this branch has a prepared .env file for you.
git checkout dev1666
```

All setup scripts are in this repository under `scripts/`.

## 2) Install prerequisites

### Ubuntu/Debian

```bash
sudo apt update
sudo apt install -y python3.11 python3.11-pip python3.11-venv git curl

# UV (installer)
curl -LsSf https://astral.sh/uv/install.sh | sh
export PATH="$HOME/.cargo/bin:$PATH"

# Optional (Node.js)
sudo apt install -y nodejs npm

# Optional (Docker Engine)
sudo apt install -y apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-compose-plugin
sudo usermod -aG docker $USER  # log out/in for group to apply
```

### RHEL/Fedora

```bash
sudo dnf install -y python3.11 python3.11-pip git curl

# UV (installer)
curl -LsSf https://astral.sh/uv/install.sh | sh
export PATH="$HOME/.cargo/bin:$PATH"

# Optional (Node.js)
sudo dnf install -y nodejs npm

# Docker
sudo dnf -y install dnf-plugins-core
sudo dnf config-manager --add-repo https://download.docker.com/linux/fedora/docker-ce.repo
sudo dnf install -y docker-ce docker-ce-cli containerd.io docker-compose-plugin
sudo systemctl enable --now docker
sudo usermod -aG docker $USER  # log out/in for group to apply
```

Verify installations:

```bash
python3 --version
uv --version
git --version
node --version  # if installed
docker --version  # if installed
docker compose version  # if installed
```

## 3) Validate prerequisites

From the `mcp-for-splunk` folder:

```bash
./scripts/check-prerequisites.sh --detailed
```

When all checks pass, continue to the next step in the main guide:

- Return to: [Main Guide](../../set-up-your-mcp-server-for-splunk.md#2-prepare-your-environment)

## Troubleshooting (Linux prerequisites)

- If `uv` not found: ensure `~/.cargo/bin` is in your PATH
- If Docker requires sudo: add your user to `docker` group and re-login
- Permission denied on scripts: `chmod +x ./scripts/*.sh`
