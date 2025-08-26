# Linux Setup Guide for AI Sidekick for Splunk

This guide covers setting up the AI Sidekick for Splunk on Linux systems (Ubuntu, Debian, RHEL, Fedora, CentOS, etc.).

## Prerequisites

- Linux distribution (Ubuntu 18.04+, Debian 10+, RHEL 8+, Fedora 30+, etc.)
- Terminal access with sudo privileges
- Internet connection for downloading dependencies
- Access to a Splunk instance (local or remote)

## 1) Clone the Repository

```bash
git clone https://github.com/deslicer/ai-sidekick-for-splunk.git
cd ai-sidekick-for-splunk
```

## 2) Install Prerequisites

### Required Software

| Software | Version | Installation Method | Notes |
|----------|---------|-------------------|-------|
| **Python** | 3.11+ | Package manager or source | Required for AI Sidekick |
| **Git** | Latest | Package manager | For cloning repositories |
| **curl/wget** | Latest | Usually pre-installed | For downloading packages |

### Optional Software

| Software | Purpose | Installation |
|----------|---------|--------------|
| **Node.js** | MCP Inspector testing | Package manager |
| **Docker** | Container deployment | Package manager |

### Distribution-Specific Installation

#### Ubuntu/Debian

```bash
# Update package lists
sudo apt update

# Install prerequisites
sudo apt install -y python3 python3-pip python3-venv git curl wget build-essential

# Install UV package manager
curl -LsSf https://astral.sh/uv/install.sh | sh
source ~/.bashrc

# Optional: Install Node.js
sudo apt install -y nodejs npm

# Optional: Install Docker
sudo apt install -y docker.io docker-compose
sudo systemctl enable docker
sudo usermod -aG docker $USER

# Verify installations
python3 --version && uv --version && git --version
```

#### RHEL/Fedora/CentOS

```bash
# For RHEL/CentOS 8+
sudo dnf update
sudo dnf install -y python3 python3-pip git curl wget gcc gcc-c++ make

# For older RHEL/CentOS 7
sudo yum update
sudo yum install -y python3 python3-pip git curl wget gcc gcc-c++ make

# Install UV package manager
curl -LsSf https://astral.sh/uv/install.sh | sh
source ~/.bashrc

# Optional: Install Node.js
sudo dnf install -y nodejs npm  # or yum for CentOS 7

# Optional: Install Docker
sudo dnf install -y docker docker-compose  # or yum for CentOS 7
sudo systemctl enable docker
sudo usermod -aG docker $USER

# Verify installations
python3 --version && uv --version && git --version
```

#### Arch Linux

```bash
# Update system
sudo pacman -Syu

# Install prerequisites
sudo pacman -S python python-pip git curl wget base-devel

# Install UV package manager
curl -LsSf https://astral.sh/uv/install.sh | sh
source ~/.bashrc

# Optional: Install Node.js
sudo pacman -S nodejs npm

# Optional: Install Docker
sudo pacman -S docker docker-compose
sudo systemctl enable docker
sudo usermod -aG docker $USER

# Verify installations
python --version && uv --version && git --version
```

#### openSUSE

```bash
# Update system
sudo zypper refresh

# Install prerequisites
sudo zypper install -y python3 python3-pip git curl wget gcc gcc-c++ make

# Install UV package manager
curl -LsSf https://astral.sh/uv/install.sh | sh
source ~/.bashrc

# Optional: Install Node.js
sudo zypper install -y nodejs npm

# Optional: Install Docker
sudo zypper install -y docker docker-compose
sudo systemctl enable docker
sudo usermod -aG docker $USER

# Verify installations
python3 --version && uv --version && git --version
```

### Alternative Python Installation Methods

#### Using pyenv (Recommended for version management)

```bash
# Install pyenv dependencies
# Ubuntu/Debian
sudo apt install -y make build-essential libssl-dev zlib1g-dev libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev libncursesw5-dev xz-utils tk-dev libffi-dev liblzma-dev python3-openssl

# RHEL/Fedora
sudo dnf install -y make gcc zlib-devel bzip2 bzip2-devel readline-devel sqlite sqlite-devel openssl-devel tk-devel libffi-devel xz-devel

# Install pyenv
curl https://pyenv.run | bash

# Add to shell profile
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc
echo 'command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(pyenv init -)"' >> ~/.bashrc
source ~/.bashrc

# Install Python 3.12
pyenv install 3.12.0
pyenv global 3.12.0

# Verify installation
python --version
```

## 3) Configure Environment Variables

### Quick Setup (Recommended)

Use the interactive setup script:

```bash
chmod +x scripts/lab/setup-env.sh
./scripts/lab/setup-env.sh
```

This script will:
- ✅ Set up pre-configured Google API key for workshop or optionally provide your own key
- ✅ Configure MCP server URL
- ✅ Set optimal model defaults
- ✅ Create your `.env` file automatically

### Manual Setup (Alternative)

1. **Copy the workshop template:**
   ```bash
   cp .env_lab .env
   ```

2. **Edit the `.env` file:**
   ```bash
   # Edit with your preferred editor
   nano .env  # or vim .env or code .env
   ```

3. **Required settings for the workshop:**
   ```env
   # Google ADK Configuration (Required)
   GOOGLE_GENAI_USE_VERTEXAI=False
   GOOGLE_API_KEY=your-google-ai-studio-api-key

   # MCP Server Configuration (Required)
   SPLUNK_MCP_SERVER_URL=http://localhost:8003/mcp/

   # Splunk Connection (Required for MCP server)
   SPLUNK_HOST=dev1666-i-035e95d7e4ea1c310.splunk.show
   SPLUNK_PORT=8089
   SPLUNK_SCHEME=https
   SPLUNK_USERNAME=admin
   SPLUNK_PASSWORD=workshop-password-provided-during-session

   # Model Configuration
   BASE_MODEL=gemini-2.0-flash-exp

   # Server Configuration
   HOST=0.0.0.0
   PORT=8087
   ```

## 4) Install Dependencies

Run the prerequisites script to check and install required packages:

```bash
chmod +x scripts/lab/check-prerequisites.sh
./scripts/lab/check-prerequisites.sh
```

This script will:
- ✅ Check for Python 3.11+
- ✅ Install `uv` (fast Python package manager)
- ✅ Create virtual environment with `uv`
- ✅ Install Google ADK and required dependencies
- ✅ Test Google API key connection
- ✅ Test MCP server connectivity

## 5) Start the AI Sidekick

```bash
chmod +x scripts/lab/start-lab-setup.sh
./scripts/lab/start-lab-setup.sh
```

You should see output like:
```
🚀 AI Sidekick Setup Complete!

✅ Virtual environment activated
✅ Google ADK initialized
✅ MCP server connection verified
✅ AI agent ready

🌐 Web interface available at: http://localhost:8087

Opening web interface in your browser...
```

## 6) Access Your AI Sidekick

1. **Open your web browser** and navigate to: `http://localhost:8087`
2. **In the web interface**, locate the **Agent Selection** dropdown in the top left
3. **Select "AI Sidekick for Splunk"** from the dropdown
4. **Start chatting** with your AI Sidekick!

## Troubleshooting

### Common Linux Issues

#### Permission Denied Errors
```bash
# Make scripts executable
chmod +x scripts/lab/*.sh

# Fix ownership issues
sudo chown -R $USER:$USER ~/.local/

# Add user to docker group (if using Docker)
sudo usermod -aG docker $USER
newgrp docker  # or logout and login again
```

#### Python Command Not Found
```bash
# Check available Python commands
which python3
which python

# Create symlink if needed (Ubuntu/Debian)
sudo ln -s /usr/bin/python3 /usr/bin/python

# Or use python3 explicitly
alias python=python3
echo 'alias python=python3' >> ~/.bashrc
```

#### Package Installation Issues
```bash
# Ubuntu/Debian: Fix broken packages
sudo apt --fix-broken install
sudo apt update && sudo apt upgrade

# RHEL/Fedora: Clear cache and update
sudo dnf clean all
sudo dnf update

# Install development tools if missing
# Ubuntu/Debian
sudo apt install -y build-essential python3-dev

# RHEL/Fedora
sudo dnf groupinstall -y "Development Tools"
sudo dnf install -y python3-devel
```

#### UV Installation Issues
```bash
# Try alternative installation methods
# Method 1: Direct download
curl -LsSf https://astral.sh/uv/install.sh | sh

# Method 2: Using pip
pip3 install --user uv

# Method 3: From source
git clone https://github.com/astral-sh/uv.git
cd uv
cargo install --path .

# Add to PATH
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

#### Web Interface Won't Load
```bash
# Check if port 8087 is in use
netstat -tlnp | grep :8087
# or
ss -tlnp | grep :8087

# Check firewall settings
sudo ufw status  # Ubuntu
sudo firewall-cmd --list-all  # RHEL/Fedora

# Temporarily disable firewall for testing
sudo ufw disable  # Ubuntu
sudo systemctl stop firewalld  # RHEL/Fedora

# Run ADK web interface manually
cd ai-sidekick-for-splunk
source .venv/bin/activate
cd src
adk web --port 8087
```

#### Virtual Environment Issues
```bash
# Delete virtual environment and recreate
rm -rf .venv
./scripts/lab/check-prerequisites.sh

# Check Python virtual environment support
python3 -m venv --help

# Install venv if missing (Ubuntu/Debian)
sudo apt install -y python3-venv
```

### MCP Server Connection Issues

If you see "MCP Server not responding":

1. **Start the MCP server first:**
   ```bash
   # Navigate to MCP server directory
   cd ../mcp-for-splunk

   # Run the automated build and run script
   ./scripts/build_and_run.sh
   ```

2. **Manual MCP server setup (if build script fails):**
   ```bash
   cd ../mcp-for-splunk
   uv run fastmcp run src/server.py --transport http --port 8003
   ```

3. **Verify MCP server is running:**
   ```bash
   # Test connection
   curl http://localhost:8003/health
   ```

### Linux-Specific Issues

#### SELinux Issues (RHEL/Fedora)
```bash
# Check SELinux status
sestatus

# Temporarily disable SELinux for testing
sudo setenforce 0

# Check SELinux logs
sudo ausearch -m avc -ts recent
```

#### AppArmor Issues (Ubuntu)
```bash
# Check AppArmor status
sudo aa-status

# Temporarily disable AppArmor for testing
sudo systemctl stop apparmor
```

#### Library Dependencies
```bash
# Install common missing libraries
# Ubuntu/Debian
sudo apt install -y libssl-dev libffi-dev libxml2-dev libxslt1-dev

# RHEL/Fedora
sudo dnf install -y openssl-devel libffi-devel libxml2-devel libxslt-devel
```

### Getting Help

1. **Check the logs:**
   ```bash
   # View recent logs
   tail -f logs/ai-sidekick.log
   ```

2. **Restart services:**
   ```bash
   # Stop services
   ./scripts/lab/stop-lab-setup.sh
   # Restart everything
   ./scripts/lab/start-lab-setup.sh
   ```

3. **Reset configuration:**
   ```bash
   # Remove existing configuration and restart
   rm -f .env
   ./scripts/lab/start-lab-setup.sh
   ```

### Debugging Commands

```bash
# Check all prerequisites
python3 --version
uv --version
node --version
git --version

# Check Linux distribution
cat /etc/os-release
lsb_release -a  # if available

# Check system architecture
uname -a

# Check available memory and disk space
free -h
df -h

# Test network connectivity
nc -zv localhost 8087
nc -zv localhost 8003

# Check running processes
ps aux | grep -E "(python|uv|adk)"

# Check system logs
journalctl -f  # systemd systems
tail -f /var/log/syslog  # older systems
```

## Next Steps

🎉 **Congratulations!** You've successfully set up your AI Sidekick for Splunk on Linux!

### Continue Your Journey:
- **🔗 Return to Main Guide:** [Continue with Step 3: Configure Environment Variables](../../setup-your-personal-ai-sidekick.md#step-3-configure-environment-variables)
- **🔗 Proceed to Lab 4:** [Create Your AI Agent](../../create-your-ai-agent.md)
- **🌟 Explore:** Try the example conversations in the main guide
- **🚀 Customize:** Modify agent configurations for your use case

---

***Return to: [Main AI Sidekick Guide](../../setup-your-personal-ai-sidekick.md)***