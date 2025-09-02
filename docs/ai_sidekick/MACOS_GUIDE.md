# AI Sidekick for Splunk - macOS User Guide

Complete setup and usage guide for Mac users. This guide walks you through installing, configuring, and using your personal AI Sidekick for Splunk on macOS.

## What You'll Build

By the end of this guide, you'll have:
- ✅ A fully functional AI Sidekick running on your Mac
- ✅ Real-time connection to your Splunk environment via MCP
- ✅ Access to specialized AI agents for search, research, and administration
- ✅ A web interface to interact with your AI Sidekick
- ✅ Understanding of the modular agent architecture

## Prerequisites

- macOS 10.15+ (Catalina or later)
- Terminal access (built-in Terminal app or iTerm2)
- Internet connection for downloading dependencies
- Access to a Splunk instance (local or remote)
- Basic familiarity with command line/terminal

---

## Step 1: Pre-Setup Requirements

Before cloning the repository, let's ensure you have Git available:

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

---

## Step 2: Clone and Setup Repository

Now let's get the AI Sidekick project and switch to the workshop branch:

```bash
mkdir ~/dev1666
cd ~/dev1666
git clone https://github.com/deslicer/ai-sidekick-for-splunk.git
cd ai-sidekick-for-splunk
git checkout dev1666
```

> **💡 Important:** The `dev1666` branch has pre-configured `.env` file with all required environment variables for the workshop.

---

## Step 3: Install Prerequisites and Dependencies

Run the prerequisites script to check and install required packages:

```bash
chmod +x scripts/lab/check-prerequisites.sh
./scripts/lab/check-prerequisites.sh
```

This script will:
- ✅ Check and install `uv` (fast Python package manager) 
- ✅ Create virtual environment with `uv`
- ✅ Install Google ADK and required dependencies
- ✅ Test Google API key connection
- ✅ Test MCP server connectivity

<details>
<summary><strong>💡 What does this script do?</strong></summary>

The script uses a **UV-First Approach**:
- **No Python installation needed** - `uv` automatically downloads and manages Python 3.11+ for the project
- **Automatic environment setup** - Creates `.venv` and installs all dependencies
- **Cross-platform compatibility** - Works on macOS, Linux, and Windows
- **Fast and reliable** - Uses `uv` for faster package installation

> **💡 Note:** `uv` automatically downloads and manages the required Python version (3.11+) for the project, so you don't need to install Python separately.
</details>

---

## Step 4: Start AI Sidekick

> **💡 Great news!** The prerequisite scripts have already created your virtual environment and installed all dependencies. You can start immediately!

### Activate the Python environment:

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

## Step 5: Access Your AI Sidekick

1. **Open your web browser** and navigate to: `http://localhost:8087`
2. **In the web interface**, locate the **Agent Selection** dropdown in the top left
3. **Select "AI Sidekick for Splunk"** from the dropdown
4. **Start chatting** with your AI Sidekick!

### Example Conversations

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

### Session Management

Your conversations are automatically saved. To start fresh:
- Click **🗑️ Clear Session** in the interface
- Or start a new session by refreshing the page

## Need Help?

If you encounter any issues during setup or usage, please refer to our comprehensive troubleshooting guide:

**📋 [Troubleshooting Guide](TROUBLESHOOTING.md)** - Complete solutions for common issues

---

## Next Steps

🎉 **Congratulations!** You've successfully set up your personal AI Sidekick for Splunk!

### What You've Accomplished:
- ✅ Deployed a modular AI agent framework
- ✅ Established real-time Splunk integration
- ✅ Experienced multi-agent collaboration
- ✅ Explored advanced search and analysis capabilities

### Continue Your Journey:
- **🌟 Explore:** Try more complex multi-agent workflows
- **🚀 Customize:** Modify agent configurations for your use case
- **🤝 Connect:** Join our community for support and collaboration
- **📚 Learn More:** Explore the architecture and extend the framework

### Resources:
- **GitHub Repository:** https://github.com/deslicer/ai-sidekick-for-splunk
- **Documentation:** https://github.com/deslicer/ai-sidekick-for-splunk/blob/main/README.md
- **Issues/Support:** https://github.com/deslicer/ai-sidekick-for-splunk/issues

---

## Feedback

Your feedback helps us improve! Please share:
- What worked well in this lab?
- What was confusing or could be clearer?
- What additional features would you like to see?

**Share feedback:** https://deslicer.com/contact

---

*Thank you for participating in the Splunk AI Sidekick lab! 🚀*
