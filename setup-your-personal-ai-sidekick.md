# Lab 3: Setup Your Personal AI Sidekick

Welcome to the AI Sidekick for Splunk hands-on lab! In this lab, you'll set up and run your own personal AI Sidekick for Splunk - a powerful, modular agent framework that integrates seamlessly with your Splunk environment.

## What You'll Build

By the end of this lab, you'll have:
- ✅ A fully functional AI Sidekick running on your machine
- ✅ Real-time connection to your Splunk environment via MCP
- ✅ Access to specialized AI agents for search, research, and administration
- ✅ A web interface to interact with your AI Sidekick
- ✅ Understanding of the modular agent architecture

## Prerequisites

- Basic familiarity with command line/terminal
- Access to a Splunk instance (local or remote)
- Internet connection for downloading dependencies
- Administrator privileges on your machine (for installing Python packages)

---

## Step 1: Clone the Repository

First, let's get the AI Sidekick project:

```bash
git clone https://github.com/deslicer/ai-sidekick-for-splunk.git
cd ai-sidekick-for-splunk
```

---

## Step 2: Install Prerequisites and Dependencies

**Choose the setup guide for your operating system:**

- **🚀 Quick Start (All Platforms):** [Beginners Setup Guide](./docs/ai_sidekick/BEGINNERS_SETUP.md)
- **🪟 Windows Users:** [Windows Setup Guide](./docs/ai_sidekick/WINDOWS_GUIDE.md)
- **🍎 macOS Users:** [macOS Setup Guide](./docs/ai_sidekick/MACOS_GUIDE.md)
- **🐧 Linux Users:** [Linux Setup Guide](./docs/ai_sidekick/LINUX_GUIDE.md)

**After completing your platform-specific setup, return here to continue with [Step 3: Configure Environment Variables](#step-3-configure-environment-variables).**

---

## Step 3: Configure Environment Variables

**🚀 Quick Setup (Recommended):**

Use the interactive setup script for easy configuration:

```bash
./scripts/lab/setup-env.sh
```

This script will:
- ✅ Configure MCP server URL (local or Docker)
- ✅ Set optimal model defaults
- ✅ Create your `.env` file automatically
- ✅ Set up pre-configured Google API key for workshop

**📋 Manual Setup (Alternative):**

If you prefer manual configuration:

1. **Copy the workshop template:**
   ```bash
   cp .env_lab .env
   ```

2. **Edit the `.env` file with your values:**
   ```bash
   # Edit with your preferred editor
   nano .env  # or code .env
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

   **MCP Server Information:**
   - The workshop assumes you have the `mcp-for-splunk` running on port 8003
   - Or use a provided workshop MCP server URL

4. **Save the file**

---

## Step 4: Start the AI Sidekick

#### For macOS/Linux/Unix:
```bash
chmod +x scripts/lab/start-lab-setup.sh
./scripts/lab/start-lab-setup.sh
```

#### For Windows:
```powershell
.\scripts\lab\start-lab-setup.ps1
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

## Step 5: Meet Your AI Sidekick

### Understanding the Agent Architecture

Your AI Sidekick uses a **modular multi-agent architecture** with these specialized agents:

1. **🎯 Root Agent** - Main coordinator and conversation handler
2. **🔍 Search Guru** - SPL expert for search optimization and strategy
3. **🔬 Data Explorer** - Comprehensive data analysis with 5-phase workflow
4. **🧠 Researcher** - Google Search integration for current information
5. **🔧 Splunk MCP** - Direct Splunk environment access and execution

### Agent Selection

1. **In the web interface**, locate the **Agent Selection** dropdown in the top left
2. **Select "AI Sidekick for Splunk"** from the dropdown
3. The framework will automatically route your requests to the appropriate specialized agents

---

## Step 6: Example Conversations

Let's explore what your AI Sidekick can do! Try these example conversations:

### Example 1: Basic Splunk Health Check

**You:** "Check my Splunk health and show me available indexes"

**Expected Response:** The AI Sidekick will:
- Automatically delegate to the Splunk MCP agent
- Check Splunk connectivity
- List available indexes with data volume information
- Provide health recommendations

### Example 2: Search Query Optimization

**You:** "Help me optimize this SPL query: `index=pas | stats count by user | sort -count`"

**Expected Response:** The Search Guru will:
- Analyze your query for performance improvements
- Suggest optimizations (time range, field filtering, etc.)
- Provide best practices explanation
- Offer alternative approaches

### Example 3: Data Explorer Workflow

**You:** "Use data explorer to analyze index=pas"

**Expected Response:** The Data Explorer will execute a comprehensive 5-phase workflow:
1. **Phase 1: Data Collection** - Gather basic index information and samples
2. **Phase 2: Field Analysis** - Analyze field patterns and distributions
3. **Phase 3: Pattern Recognition** - Identify trends and anomalies
4. **Phase 4: Insight Generation** - Generate 5 actionable business insights
5. **Phase 5: Quality Assessment** - Validate findings and provide recommendations

### Example 4: Current Information Research

**You:** "What are the latest Splunk security advisories for version 9.4?"

**Expected Response:** The Researcher will:
- Use Google Search to find current security information
- Provide links to official Splunk security advisories
- Summarize key findings and recommendations
- Suggest next steps for security updates

### Example 5: Multi-Agent Collaboration

**You:** "Help me analyze file operations patterns in index=pas and create optimized searches"

**Expected Response:** Multiple agents will collaborate:
- **Data Explorer** performs comprehensive 5-phase analysis of file operations data
- **Search Guru** optimizes the SPL queries generated by Data Explorer
- **Splunk MCP** executes all searches and returns formatted results
- **Root Agent** coordinates the workflow and presents unified results

### 🎯 More Example Questions to Try

**Data Explorer (Comprehensive Analysis):**
```
"Use data explorer to analyze index=_internal"
"Data explorer analyze index=_audit"
```

**Search Guru (SPL Optimization & Strategy):**
```
"Help me create a search to find errors in index=_internal"
"What's the best SPL approach for analyzing failed logins?"
"Create an efficient search for monitoring system performance"
```

**Splunk MCP (Direct Operations):**
```
"Run this search: index=_internal | head 10 | table _time, component"
"Show me events from index=pas | head 20"
"List all available indexes"
```

**Researcher (Current Information):**
```
"What are the latest Splunk best practices for search optimization?"
"Research current security threats for Windows authentication"
"What's new in Splunk Enterprise 10.0?"
```

**Multi-Agent Workflows:**
```
"Help me investigate security patterns in my data"
"Create a complete monitoring strategy for index=_internal"
```

---

### Session Management

Your conversations are automatically saved. To start fresh:
- Click **🗑️ Clear Session** in the interface
- Or start a new session by refreshing the page

---

## Step 7: Understanding the Architecture

### Modular Design Benefits

1. **Specialized Expertise** - Each agent excels in its domain
2. **Automatic Delegation** - Framework routes tasks to appropriate agents
3. **Extensible** - Easy to add new agents and capabilities
4. **Session Persistence** - Maintains context across interactions
5. **Real-Time Integration** - Direct Splunk environment access

### MCP (Model Context Protocol) Integration

- **Real-Time Connection** - Live access to your Splunk environment
- **Session Management** - Persistent connections with automatic reconnection
- **Tool Integration** - Rich set of Splunk administration tools
- **Security** - Secure credential handling and SSL support

### Google ADK Framework

- **Multi-Agent Coordination** - Native support for agent collaboration
- **Google Search Integration** - Access to current information
- **Conversation Management** - Advanced dialog state handling
- **Tool Orchestration** - Seamless tool-to-agent integration

## Need Help?

If you encounter any issues during setup or while using the AI Sidekick, check our comprehensive troubleshooting guide:

**📖 [AI Sidekick Troubleshooting Guide](./docs/ai_sidekick/TROUBLESHOOTING.md)**

For platform-specific issues, also refer to:
- **🪟 [Windows Troubleshooting](./docs/ai_sidekick/WINDOWS_GUIDE.md#troubleshooting)**
- **🍎 [macOS Troubleshooting](./docs/ai_sidekick/MACOS_GUIDE.md#troubleshooting)**
- **🐧 [Linux Troubleshooting](./docs/ai_sidekick/LINUX_GUIDE.md#troubleshooting)**

---

## Next Steps

🎉 **Congratulations!** You've successfully set up your personal AI Sidekick for Splunk!

### What You've Accomplished:
- ✅ Deployed a modular AI agent framework
- ✅ Established real-time Splunk integration
- ✅ Experienced multi-agent collaboration
- ✅ Explored advanced search and analysis capabilities

### Continue Your Journey:
- **🔗 Proceed to Lab 4:** [Create Your AI Agent](./create-your-ai-agent.md)
- **🌟 Contribute:** Add your own agents to the framework
- **🚀 Deploy:** Set up for production use in your organization

### Resources:
- **GitHub Repository:** https://github.com/desclier/ai-sidekick-for-splunk
- **Documentation:** https://docs.ai-sidekick-for-splunk.com
- **Issues/Support:** https://github.com/desclier/ai-sidekick-for-splunk/issues

---

## Feedback

Your feedback helps us improve! Please share:
- What worked well in this lab?
- What was confusing or could be clearer?
- What additional features would you like to see?

**Share feedback:** opensource@deslicer.com

---

*Thank you for participating in the AI Sidekick for Splunk lab! 🚀*
