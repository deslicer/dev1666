# Beginners Setup (no IDE or Git required)

This guide is for absolute beginners with no prior development experience. You'll get everything running even if you don't have an editor or Git installed.

## 1) Get the project files

### Option A: Download ZIP (no Git)

1. Open the project page: `https://github.com/deslicer/mcp-for-splunk`
2. In the branch dropdown, select the `dev1666` branch.
3. Click the green "Code" button → "Download ZIP".
4. Extract the ZIP (unzip) to a folder you can find (e.g., Desktop).
5. You now have a folder named `mcp-for-splunk` with the `dev1666` branch contents.

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
git clone https://github.com/deslicer/mcp-for-splunk.git
cd mcp-for-splunk
# Checkout dev1666 branch in git, this branch has a prepared .env file for you.
git checkout dev1666
```

## 2) Install a code editor (Visual Studio Code)

- Download VS Code: `https://code.visualstudio.com/`
- Open VS Code → File → Open Folder → select the `mcp-for-splunk` folder
- Open the integrated terminal:
  - Windows: View → Terminal (PowerShell)
  - macOS/Linux: View → Terminal (bash/zsh)

If you prefer, you can use your system terminal instead of VS Code's terminal.

## 3) Install prerequisites (OS guides)

Follow the guide for your operating system and jump directly to the install section:

- Windows: [WINDOWS_GUIDE.md#install-prereqs](WINDOWS_GUIDE.md#2-install-prerequisites)
- macOS: [MACOS_GUIDE.md#install-prereqs](MACOS_GUIDE.md#2-install-prerequisites)
- Linux: [LINUX_GUIDE.md#install-prereqs](LINUX_GUIDE.md#2-install-prerequisites)

These guides cover installing Python, the "uv" package manager, optional Node.js, and Docker.
