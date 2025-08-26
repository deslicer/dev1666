# Beginners Setup for AI Sidekick for Splunk (no IDE or Git required)

This guide is for absolute beginners with no prior development experience. You'll get the AI Sidekick running even if you don't have an editor or Git installed.

## 1) Get the project files

### Option A: Download ZIP (no Git)

1. Open the project page: `https://github.com/deslicer/ai-sidekick-for-splunk`
2. Click the green "Code" button → "Download ZIP".
3. Extract the ZIP (unzip) to a folder you can find (e.g., Desktop).
4. You now have a folder named `ai-sidekick-for-splunk` with all the files.

### Option B: Use Git (recommended)

Install Git (pick your OS):

- Windows (PowerShell):
  ```powershell
  winget install Git.Git
  git --version
  ```

- macOS (Terminal with Homebrew):
  ```bash
  brew install git
  git --version
  ```

- Linux:
  ```bash
  # Ubuntu/Debian
  sudo apt update && sudo apt install -y git
  # RHEL/Fedora
  sudo dnf install -y git
  git --version
  ```

Then clone the repository:

```bash
git clone https://github.com/deslicer/ai-sidekick-for-splunk.git
cd ai-sidekick-for-splunk
```

## 2) Install a code editor (Visual Studio Code)

- Download VS Code: `https://code.visualstudio.com/`
- Open VS Code → File → Open Folder → select the `ai-sidekick-for-splunk` folder
- Open the integrated terminal:
  - Windows: View → Terminal (PowerShell)
  - macOS/Linux: View → Terminal (bash/zsh)

If you prefer, you can use your system terminal instead of VS Code's terminal.

## 3) Install prerequisites (OS guides)

Follow the guide for your operating system and jump directly to the install section:

- Windows: [WINDOWS_GUIDE](WINDOWS_GUIDE.md#2-install-prerequisites)
- macOS: [MACOS_GUIDE](MACOS_GUIDE.md#2-install-prerequisites)
- Linux: [LINUX_GUIDE](LINUX_GUIDE.md#2-install-prerequisites)

These guides cover installing Python, the "uv" package manager, optional Node.js, and other dependencies.

## 4) Quick Start

Once you have the prerequisites installed, you can use the automated setup scripts:

### Windows
```powershell
# Run the complete setup
.\scripts\lab\start-lab-setup.ps1
```

### macOS/Linux
```bash
# Make scripts executable and run setup
chmod +x scripts/lab/*.sh
./scripts/lab/start-lab-setup.sh
```

## 5) Access Your AI Sidekick

1. **Open your web browser** and navigate to: `http://localhost:8087`
2. **In the web interface**, locate the **Agent Selection** dropdown in the top left
3. **Select "AI Sidekick for Splunk"** from the dropdown
4. **Start chatting** with your AI Sidekick!

## Need Help?

If you encounter any issues:

1. **Check the platform-specific troubleshooting sections:**
   - [Windows Troubleshooting](WINDOWS_GUIDE.md#troubleshooting)
   - [macOS Troubleshooting](MACOS_GUIDE.md#troubleshooting)
   - [Linux Troubleshooting](LINUX_GUIDE.md#troubleshooting)

2. **Make sure the MCP server is running first:**
   - Follow the [MCP Server Setup Guide](../mcp/BEGINNERS_SETUP.md)
   - The AI Sidekick requires the MCP server to communicate with Splunk

3. **Try the detailed setup guides:**
   - Return to the [main AI Sidekick guide](../../3-setup-your-personal-ai-sidekick.md) for step-by-step instructions

## What's Next?

Once your AI Sidekick is running:
- **🔗 Return to Main Guide:** [Continue with Step 3: Configure Environment Variables](../../3-setup-your-personal-ai-sidekick.md#step-3-configure-environment-variables)
- **🔗 Proceed to Lab 4:** [Create Your AI Agent](../../4-create-your-ai-agent.md)
- **🌟 Explore:** Try different agent types and capabilities
- **🚀 Customize:** Modify configurations for your specific use case