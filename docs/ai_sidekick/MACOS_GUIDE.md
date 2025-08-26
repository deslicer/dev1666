# macOS Setup Guide for AI Sidekick for Splunk

This guide covers setting up the AI Sidekick for Splunk on macOS systems.

## Prerequisites

- macOS 10.15+ (Catalina or later)
- Terminal access (built-in Terminal app or iTerm2)
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
| **Homebrew** | Latest | [brew.sh](https://brew.sh/) | Package manager for macOS |
| **Python** | 3.11+ | `brew install python` | Required for AI Sidekick |
| **Git** | Latest | `brew install git` | For cloning repositories |

### Optional Software

| Software | Purpose | Installation |
|----------|---------|--------------|
| **Node.js** | MCP Inspector testing | `brew install node` |
| **iTerm2** | Better terminal experience | `brew install --cask iterm2` |

### Quick Installation (Recommended)

```bash
# Install Homebrew (if not already installed)
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Install all prerequisites
brew install python git node uv

# Verify installations
python3 --version && uv --version && node --version && git --version
```

### Manual Installation Steps

#### Homebrew Installation
```bash
# Install Homebrew package manager
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Add Homebrew to PATH (follow the instructions shown after installation)
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv)"

# Verify installation
brew --version
```

#### Python Installation
```bash
# Option 1: Homebrew (Recommended)
brew install python

# Option 2: Official installer
# Download from https://python.org/downloads/

# Option 3: pyenv for version management
brew install pyenv
pyenv install 3.12.0
pyenv global 3.12.0

# Verify installation
python3 --version
pip3 --version
```

#### UV Package Manager Installation
```bash
# Option 1: Homebrew (Recommended)
brew install uv

# Option 2: Official installer
curl -LsSf https://astral.sh/uv/install.sh | sh

# Option 3: Pip fallback
pip3 install uv

# Verify installation
uv --version
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
   nano .env  # or code .env or vim .env
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

### Common macOS Issues

#### Command Not Found Errors
```bash
# If 'brew' command not found, add to PATH
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
source ~/.zprofile

# If 'python3' command not found, check installation
which python3
brew install python

# If 'uv' command not found
brew install uv
# OR
curl -LsSf https://astral.sh/uv/install.sh | sh
source ~/.bashrc  # or ~/.zshrc
```

#### Permission Issues
```bash
# Make scripts executable
chmod +x scripts/lab/*.sh

# Fix Homebrew permissions (if needed)
sudo chown -R $(whoami) /opt/homebrew/
```

#### Python Version Issues
```bash
# Check Python version
python3 --version

# If version is too old, update
brew upgrade python

# Use pyenv for version management
brew install pyenv
pyenv install 3.12.0
pyenv global 3.12.0
```

#### Web Interface Won't Load
```bash
# Check if port 8087 is in use
lsof -i :8087

# Try accessing alternative URL
# http://127.0.0.1:8087

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

### macOS-Specific Issues

#### Xcode Command Line Tools
```bash
# Install Xcode command line tools (if needed)
xcode-select --install
```

#### Rosetta 2 (Apple Silicon Macs)
```bash
# Install Rosetta 2 for Intel compatibility (if needed)
softwareupdate --install-rosetta
```

#### Firewall Issues
```bash
# Check if macOS firewall is blocking connections
sudo /usr/libexec/ApplicationFirewall/socketfilterfw --getglobalstate

# Temporarily disable firewall for testing (not recommended for production)
sudo /usr/libexec/ApplicationFirewall/socketfilterfw --setglobalstate off
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

# Check macOS version
sw_vers

# Check system architecture
uname -m

# Test network connectivity
nc -zv localhost 8087
nc -zv localhost 8003

# Check running processes
ps aux | grep -E "(python|uv|adk)"
```

## Next Steps

🎉 **Congratulations!** You've successfully set up your AI Sidekick for Splunk on macOS!

### Continue Your Journey:
- **🔗 Return to Main Guide:** [Continue with Step 3: Configure Environment Variables](../../setup-your-personal-ai-sidekick.md#step-3-configure-environment-variables)
- **🔗 Proceed to Lab 4:** [Create Your AI Agent](../../create-your-ai-agent.md)
- **🌟 Explore:** Try the example conversations in the main guide
- **🚀 Customize:** Modify agent configurations for your use case

---

***Return to: [Main AI Sidekick Guide](../../setup-your-personal-ai-sidekick.md)***