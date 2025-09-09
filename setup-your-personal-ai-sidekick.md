# Lab 3: Setup Your Personal AI Sidekick

Welcome to the AI Sidekick for Splunk hands-on lab! In this lab, you'll set up and run your own personal AI Sidekick for Splunk - a powerful, modular agent framework that integrates seamlessly with your Splunk environment.

## What You'll Build

By the end of this lab, you'll have:
- ✅ A fully functional AI Sidekick running on your machine
- ✅ Real-time connection to your Splunk environment via MCP
- ✅ Access to specialized AI agents including FlowPilot workflows
- ✅ A web interface to interact with your AI Sidekick
- ✅ Understanding of the modular agent architecture

## Prerequisites

- Basic familiarity with command line/terminal
- Access to a Splunk instance (local or remote)
- Internet connection for downloading dependencies
- Administrator privileges on your machine (for installing packages)

---

## Step 1: Pre-Setup Requirements

Before cloning the repository, let's ensure you have the necessary tools installed:

### 🍎 macOS Users

macOS typically has Git pre-installed, but you may need to install Command Line Tools:

```bash
# Test if git is available
git --version
```

<details>
<summary><strong>🔧 Troubleshooting: If you get "command line tools" prompt or error</strong></summary>

If you see a popup asking to install Command Line Tools or get an error like "xcrun: error: invalid active developer path", follow these steps:

1. **Install Xcode Command Line Tools:**
   ```bash
   xcode-select --install
   ```

2. **Wait for installation to complete** (this may take several minutes)

3. **Verify installation:**
   ```bash
   xcode-select -p
   ```
   You should see: `/Applications/Xcode.app/Contents/Developer` or `/Library/Developer/CommandLineTools`

4. **Test Git again:**
   ```bash
   git --version
   ```
   You should see something like: `git version 2.39.3 (Apple Git-145)`

5. **If still having issues, try:**
   ```bash
   sudo xcode-select --reset
   xcode-select --install
   ```

</details>

### 🪟 Windows Users

Windows doesn't have Git pre-installed, so let's install it:

> **💡 Skip this section if you already have Git installed.** You can check by running `git --version` in PowerShell.

1. **Install Git for Windows:**

   **Option A: Using winget (Recommended - Windows 10/11):**
   ```powershell
   winget install Git.Git
   ```
   **Option B: Manual Download:**
   - Visit [https://git-scm.com/download/windows](https://git-scm.com/download/windows)
   - Download and run the installer
   - Use default settings during installation

2. **Restart your terminal/PowerShell** after installation

3. **Verify Git installation:**
   ```powershell
   git --version
   ```
   You should see something like: `git version 2.45.2.windows.1`

<details>
<summary><strong>🔧 Troubleshooting: If git command is not found</strong></summary>

If you get "'git' is not recognized as an internal or external command":

1. **Close and reopen your terminal/PowerShell**
2. **Check if Git is in your PATH:**
   ```powershell
   $env:PATH -split ';' | Select-String -Pattern 'Git'
   ```
3. **If not found, add Git to PATH manually:**
   - Open System Properties → Environment Variables
   - Add `C:\Program Files\Git\bin` to your PATH variable
   - Restart terminal and test again

4. **Alternative: Use Git Bash**
   - Search for "Git Bash" in Start Menu
   - Use Git Bash instead of PowerShell for git commands

</details>

---

## Step 2: Clone and Setup Repository

`Start a new terminal window`

Now let's get the AI Sidekick project and switch to the workshop branch:

### 🍎 macOS / 🐧 Linux
```bash
cd ~/dev1666
git clone https://github.com/deslicer/ai-sidekick-for-splunk.git
cd ai-sidekick-for-splunk
git checkout dev1666
```

### 🪟 Windows
```powershell
cd $HOME\dev1666
git clone https://github.com/deslicer/ai-sidekick-for-splunk.git
cd ai-sidekick-for-splunk
git checkout dev1666
```

> **💡 Important:** The `dev1666` branch has pre-configured `.env` file with all required environment variables for the workshop.

---

## Step 3: Install Prerequisites and Dependencies

Choose your operating system and run the appropriate prerequisite script:

### 🍎 macOS / 🐧 Linux
```bash
./scripts/smart-install.sh
```

### 🪟 Windows
```powershell
.\scripts\smart-install.ps1
```

### 🐍 Cross-Platform (Python)
Alternative Python-based script (if you already have Python installed):
   ```bash
python scripts/smart-install.py
```

<details>
<summary>📋 What the prerequisite scripts do</summary>

The scripts will:
- ✅ Install `uv` (fast Python package manager) - handles Python automatically
- ✅ Create Python virtual environment using `uv sync`
- ✅ Install all project dependencies automatically
- ✅ Verify Git installation and install if needed
- ✅ Complete environment setup in one step

**Expected output:**
```
✅ UV Package Manager available
✅ Setting up project environment...
✅ Virtual environment created and dependencies installed
✅ Git version control available

🚀 Next Steps:
Continue with the lab guide to start your AI Sidekick

Installation complete! Your environment is ready.
```
</details>

<details>
<summary>🛠️ Manual Installation (Fallback)</summary>

If the prerequisite scripts don't work for your system:

**Install uv (handles Python automatically):**
   ```bash
# macOS/Linux
curl -LsSf https://astral.sh/uv/install.sh | sh

# Windows (PowerShell)
powershell -c "irm https://astral.sh/uv/install.ps1 | iex"
```

**Create virtual environment and install dependencies:**
```bash
uv sync
```

> **💡 Note:** `uv` automatically downloads and manages the required Python version (3.11+) for the project, so you don't need to install Python separately.
</details>

---

## Step 4: Start AI Sidekick

> **💡 Great news!** The prerequisite scripts have already created your virtual environment and installed all dependencies. You can start immediately!

### Start the AI Sidekick:
```bash
uv run ai-sidekick --start
```

<details>
<summary>🔧 First-Time Environment Setup (Interactive Prompts)</summary>

On your first run, the system will automatically prompt you to configure your Splunk connection details. You'll be asked to provide:

- **Google AI Studio API key** - Required for AI agent functionality
- **Splunk MCP server URL** - URL to your MCP server (e.g., http://localhost:8003)
- **Splunk host** - Your Splunk hostname (e.g., localhost)
- **Splunk username** - Username for Splunk authentication
- **Splunk password** - Password for authentication (will be masked in display)

After providing these details, the system will:
- Save your configuration to the .env file
- Display your connection information (with masked sensitive data)
- Proceed with startup

</details>

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

---

## Step 5: Meet Your AI Sidekick

### Understanding the Agent Architecture

Your AI Sidekick uses a **modular multi-agent architecture** with these specialized agents:

1. **🎯 Root Agent** - Main coordinator and conversation handler
2. **🔍 Search Guru** - SPL expert for search optimization and strategy
4. **🧠 Researcher** - Google Search integration for current information
5. **🔧 SplunkShow** - Direct Splunk environment access and execution
6. **⚡ FlowPilot Workflows** - Template-driven specialized workflows

### Agent Selection

1. **In the web interface**, locate the **Agent Selection** dropdown in the top left
2. **Select "AI Sidekick for Splunk"** from the dropdown
3. The framework will automatically route your requests to the appropriate specialized agents

---

## Step 6: Try Your AI Sidekick

Let's test your AI Sidekick with three essential workflows:

### Example 1: System Health Check 🏥

**You:**
```bash
Run a system health check
```

<details>
<summary>Expected Response</summary>

The AI Sidekick will:
- Automatically delegate to the **System Health Check Flow** (FlowPilot workflow)
- Check Splunk connectivity and version
- Verify data ingestion (last 24 hours)
- Assess basic system performance
- Provide health recommendations and educational insights

**Sample Output:**
```
Here are the results of the System Health Check Flow:

Phase 1: Rapid Health Assessment

• Indexer Health Check: No indexer peers were found.
• Search Head Health Check: The search head 'show-demo-i-030177b79939df4c' is healthy with CPU usage at 13.96% and memory usage at 0.19%.
• License Usage Check: No license usage data was available for the last hour.
• Data Ingestion Health: Data ingestion for index 's4c_www' is healthy with a count of 906 and an ingestion rate of 60.40.
• Forwarder Connectivity: No data was found, which indicates either no active universal forwarders sending data or improper indexing.
• Search Performance Check: User admin had one slow search with an average runtime of 6.14 seconds, a max runtime of 6.14 seconds, and a performance status of good.
• Skipped Searches Check: No skipped searches were found in the last hour, indicating no scheduler pressure.
• SHC Status Check: The search returned no results. This could indicate that a search head cluster is not configured in this environment, or that there was an issue retrieving the cluster status.

Phase 2: Health Status Synthesis

• Overall health assessment was completed successfully.

It appears there might be issues with indexer peers, license usage data, forwarder connectivity, and SHC status. Further investigation may be required for these items.

Would you like me to investigate any of these issues further?
```
</details>

### Example 2: List Available Indexes 📋

**You:**
```bash
List all available indexes
```

<details>
<summary>Expected Response</summary>

The SplunkShow agent will:
- Connect to your Splunk environment
- Retrieve all available indexes
- Show data volume and last update information
- Provide index usage recommendations

**Sample Output:**
```
The indexes available are: history, main, s4c_phyphox, s4c_stocks, s4c_tutorial, s4c_weather, s4c_www, splunklogger, and summary. A total of 9 indexes are available to you, and there are 18 total indexes including internal indexes.

Would you like to explore any of these indexes further? For example, I can list the sourcetypes for a specific index.
```
</details>

### Example 3: Index Analysis Flow 🔬

**You:**
```bash
Use index analysis flow to analyze index=s4c_www and provide actionable insights
```

<details>
<summary>Expected Response</summary>

The **Index Analysis Flow** (FlowPilot workflow) will execute a comprehensive analysis:

**Phase 1: Data Collection** - Gather basic index information and samples
**Phase 2: Field Analysis** - Analyze field patterns and distributions  
**Phase 3: Pattern Recognition** - Identify trends and anomalies
**Phase 4: Volume Assessment** - Evaluate data volume and performance
**Phase 5: Insight Generation** - Generate actionable business insights

**Sample Output:**
```
The IndexAnalysis Flow has completed for index=s4c_www.
Here's a summary of the analysis:

• Intelligent Data Discovery: Simulated data discovery to outline the index structure.
• Adaptive Data Sampling:
  ○ Volume sampling identified consistent hourly event volumes for the access_combined sourcetype, with a slight dip on '2025-09-01T03:00:00.000+00:00'.
  ○ Field sampling revealed key fields like JSESSIONID, action, bytes, clientip, product_id, status, and uri with their respective counts and distinct values.
• Intelligent Pattern Analysis:
  ○ Identified a high percentage of 503 (Service Unavailable) and 404 (Not Found) errors, particularly affecting the /product.screen endpoint.
  ○ Anomaly detection found anomalies on '2025-09-01T03:00:00.000+00:00' and '2025-09-08T14:00:00.000+00:00'.
  ○ Correlation analysis showed a strong relationship between the access_combined sourcetype and the field webgurke.
  ○ Temporal analysis indicated that access_combined is the most common sourcetype, with higher counts on Mondays between 06:00 and 13:00.
• Contextual Result Synthesis: Phase-level synthesis handled result aggregation.

Key recommendations:

• Investigate the root cause of 503 errors.
• Examine product links and IDs for correctness to address 404 errors.
• Check for unusual traffic patterns that might indicate bot activity.
• Further investigate anomalies detected on '2025-09-01T03:00:00.000+00:00' and '2025-09-08T14:00:00.000+00:00'.

Would you like me to investigate any of these recommendations further? For example, I could investigate the root cause of the 503 errors.
```
</details>

---

## 🎉 Congratulations!

You've successfully set up and tested your personal AI Sidekick for Splunk!
### Please continue with Lab 4: [Create your AI Agent](create-your-ai-agent.md)

### What You've Accomplished:
- ✅ Deployed a modular AI agent framework
- ✅ Established real-time Splunk integration
- ✅ Experienced FlowPilot workflow execution
- ✅ Explored system health monitoring and index analysis

### Continue Your Journey:
- **🌟 Contribute:** Add your own workflow agents to the framework
- **🚀 Deploy:** Set up for production use in your organization

### Resources:
- **GitHub Repository:** https://github.com/deslicer/ai-sidekick-for-splunk
- **Documentation:** Complete guides in the repository
- **Issues/Support:** https://github.com/deslicer/ai-sidekick-for-splunk/issues

---

## Need Help?

If you encounter any issues:

1. **Re-run Prerequisites:** Run the prerequisite script again to ensure all components are installed
2. **Environment:** Verify you're in the `dev1666` branch with activated virtual environment
3. **MCP Connection:** Ensure the MCP server is running (should start automatically)
4. **Browser:** Try refreshing the web interface at http://localhost:8087

---

*Thank you for participating in the AI Sidekick for Splunk lab! 🚀*
