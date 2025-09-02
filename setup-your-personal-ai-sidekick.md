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
- Git installed on your system (will be checked and installed if needed)

---

## Step 1: Clone and Setup Repository

`Start a new terminal window`

First, let's get the AI Sidekick project and switch to the workshop branch:

```bash
mkdir ~/dev1666
cd ~/dev1666
git clone https://github.com/deslicer/ai-sidekick-for-splunk.git
cd ai-sidekick-for-splunk
git checkout dev1666
```

> **💡 Important:** The `dev1666` branch has pre-configured `.env` file with all required environment variables for the workshop.

---

## Step 2: Install Prerequisites and Dependencies

Choose your operating system and run the appropriate prerequisite script:

### 🪟 Windows
```powershell
.\scripts\lab\check-prerequisites.ps1
```

### 🍎 macOS
```bash
./scripts/lab/check-prerequisites.sh
```

### 🐧 Linux
   ```bash
./scripts/lab/check-prerequisites.sh
   ```

### 🐍 Cross-Platform (Python)
Alternative Python-based script(If you already have python installed):
   ```bash
python scripts/check-prerequisites.py
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

🚀 Ready to Start:
1. Activate the virtual environment: source .venv/bin/activate
2. Start AI Sidekick: uv run ai-sidekick --start
3. Access web interface: http://localhost:8087

Virtual environment and dependencies are ready!
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

## Step 3: Start AI Sidekick

> **💡 Great news!** The prerequisite scripts have already created your virtual environment and installed all dependencies. You can start immediately!

### Activate the Python environment:

**Windows:**
```powershell
.venv\Scripts\activate
```

**macOS/Linux:**
```bash
source .venv/bin/activate
```

### Start the AI Sidekick:
```bash
uv run ai-sidekick --start
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

---

## Step 4: Meet Your AI Sidekick

### Understanding the Agent Architecture

Your AI Sidekick uses a **modular multi-agent architecture** with these specialized agents:

1. **🎯 Root Agent** - Main coordinator and conversation handler
2. **🔍 Search Guru** - SPL expert for search optimization and strategy
3. **🔬 Data Explorer** - Comprehensive data analysis with 5-phase workflow
4. **🧠 Researcher** - Google Search integration for current information
5. **🔧 SplunkShow** - Direct Splunk environment access and execution
6. **⚡ FlowPilot Workflows** - Template-driven specialized workflows

### Agent Selection

1. **In the web interface**, locate the **Agent Selection** dropdown in the top left
2. **Select "AI Sidekick for Splunk"** from the dropdown
3. The framework will automatically route your requests to the appropriate specialized agents

---

## Step 5: Try Your AI Sidekick

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
✅ System Health Check Complete

📊 System Overview:
- Splunk Version: 9.4.0 (Build: abc123)
- System Status: Healthy
- Data Flow: Active (1.2M events/24h)

🎯 Health Assessment:
- ✅ Splunk services running normally
- ✅ Data ingestion active
- ⚠️  Consider index optimization for better performance

📚 Educational Insights:
This health check verified your Splunk environment is ready for workshop activities.
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
📋 Available Splunk Indexes:

🔍 Core Indexes:
- main (2.1GB, last event: 2 minutes ago)
- _internal (890MB, last event: 30 seconds ago)
- _audit (45MB, last event: 1 minute ago)

🏢 Workshop Indexes:
- pas (1.5GB, last event: 5 minutes ago)
- security (780MB, last event: 3 minutes ago)

💡 Recommendation: Use 'pas' index for analysis exercises - it has rich sample data perfect for learning.
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
🔬 Index Analysis Complete: s4c_www

📊 Analysis Summary:
- Total Events: 2,456,789 events
- Time Range: 30 days
- Primary Sourcetypes: access_combined (60%), error_log (25%), ssl_access (15%)
- Peak Activity: Business hours (9 AM - 6 PM) with weekend traffic

🎯 Actionable Insights:

🔒 Security Analyst:
- Monitor 404 error patterns (detected unusual spikes)
- Set up alerts for suspicious user agents and bot traffic
- Dashboard: | search index=s4c_www status=404 | stats count by clientip

⚙️ DevOps Engineer:
- SSL certificate errors increasing (5% of traffic)
- High response times during peak hours (>2s average)
- Monitor: | search index=s4c_www ssl_error | timechart span=1h count

📈 Business Analyst:
- Mobile traffic growing 25% month-over-month
- Popular content pages driving 70% of engagement
- Track: | search index=s4c_www | stats count by uri_path | sort -count

🚀 Next Steps:
1. Implement recommended dashboards
2. Set up automated monitoring alerts
3. Schedule regular index health checks
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
