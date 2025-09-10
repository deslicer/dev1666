<div align="center">
  <img src="./media/deslicer_white.svg" alt="Deslicer" width="200"/>
</div>

# DEV1666 - AI Sidekick for Splunk Lab Exersices

## Table of Contents

- [Lab Environment Information](#lab-environment-information)
- [Lab Exercises](#lab-exercises)
  - [Lab 1: Set up MCP Server](#lab-1-set-up-mcp-server-for-data-analytics)
  - [Lab 2: Set up AI Sidekick](#lab-2-set-up-your-personal-ai-sidekick)
  - [Lab 3: Create AI Agent](#lab-3-create-your-ai-agent)
- [Summary](#summary)
- [Resources](#resources)

## Lab Environment Information

### Lab Environment Overview

Throughout this workshop, you will work with AI agents and the Model Context Protocol (MCP) to create intelligent sidekicks that can interact with your data analytics environment. You'll learn to build AI agents that can understand, analyze, and provide insights from your data.

### Prerequisites

Before starting the workshop, ensure you have:

- **💻 Computer Requirements:**
  - Windows 10/11, macOS 10.15+, or Linux (Ubuntu 18.04+, RHEL 8+, etc.)
  - Administrator/sudo privileges for installing software
  - 4GB+ RAM and 2GB+ free disk space

- **🌐 Network Access:**
  - Stable internet connection for downloading dependencies
  - Access to GitHub for cloning repositories
  - Ability to access localhost ports (8003, 8087)

- **🧠 Knowledge Requirements:**
  - Basic familiarity with command line/terminal
  - Basic understanding of data analytics concepts (indexes, searches)
  - No programming experience required (we'll guide you through everything!)

- **🔧 Software (will be installed during labs):**
  - Python 3.11+
  - Git
  - Node.js (optional, for MCP Inspector)
  - uv (fast Python package manager)

### Lab Connection Information

Lab: https://splunk.show/dev1666

Guide: https://splunk.show/dev1666-guide

If you have any issues with the lab guide or show access, contact show staff in the room.
Alternatively, we provide links to use a Deslicer Show Instance.

## Lab Exercises


This comprehensive guide walks you through each lab with detailed instructions, troubleshooting tips, and verification steps to ensure successful completion.

---

### Lab 1: Set up MCP Server for Data Analytics

**Description:**
In this lab you will set up your own MCP (Model Context Protocol) server for data analytics, which serves as the bridge between AI agents and your data analytics environment.

**Key Learning Objectives:**
- Understand MCP architecture and its role in AI-data integration
- Configure and deploy MCP server for data analytics
- Verify connectivity and test server functionality

**Steps:**
1. **Clone the repository and prepare environment:**

   **macOS/Linux:**
   ```bash
   mkdir -p ~/dev1666
   cd ~/dev1666
   git clone https://github.com/deslicer/mcp-for-splunk.git
   cd mcp-for-splunk
   git checkout dev1666
   unset UV_PROJECT_ENVIRONMENT
   ```

   **Windows:**
   ```powershell
   mkdir $HOME\dev1666
   cd $HOME\dev1666
   git clone https://github.com/deslicer/mcp-for-splunk.git
   cd mcp-for-splunk
   git checkout dev1666
   ```

2. **Copy the lab environment configuration:**

   **macOS/Linux:**
   ```bash
   cp env.lab .env
   ```

   **Windows:**
   ```powershell
   Copy-Item env.lab .env -Force
   ```

3. **Install prerequisites using the smart install script:**

   **macOS/Linux:**
   ```bash
   ./scripts/smart-install.sh
   ```

   **Windows:**
   ```powershell
   pwsh -File scripts\smart-install.ps1
   ```

⚠️ After completing the smart-install you need to provide splunk connection details. 

Lab: https://splunk.show/dev1666

Guide: https://splunk.show/dev1666-guide

If you have any issues with the lab guide or show access, contact show staff in the room.
Alternatively, we provide links to use a Deslicer Show Instance. Ensure you have access to the Splunk host, port, username and password before continuing to the next step. If you are lacking that information, reach out to one of the speakers.

   ```
   Host:
   Port:
   Username:
   Password: (No echo prompt)
   ```

4. **Start the MCP server and verify it's running:**
   ```bash
   uv run mcp-server --local -d
   ```

5. **Test the MCP server and data analytics connection:**
   ```bash
   uv run mcp-server --test
   ```

**Expected Output:**
```
== MCP Server Check ==
URL: http://0.0.0.0:8003/mcp/
• MCP Server: OK ✅
• Tools: 39 | Resources: 17

-- Data Analytics Health --
• Status: Connected ✅
• Server: splunk-server-name
• Version: 9.3.2411.113
• Source: server_config
```

**Lab completion verification:**
- If the script returns "MCP Server: OK ✅" and "Data Analytics Health Status: Connected ✅", you have successfully completed the setup lab.

---

### Lab 2: Set up Your Personal AI Sidekick

**Description:**
In this lab, you will set up and configure your personal AI Sidekick for data analytics. You'll explore the multi-agent system architecture and learn how to assign tasks to different specialized agents.

**Key Learning Objectives:**
- Deploy the AI Sidekick multi-agent framework
- Understand specialized agent roles and capabilities
- Experience automated workflow execution

**Steps:**

6. **Clone and setup AI Sidekick repository:**

   **macOS/Linux:**
   ```bash
   mkdir -p ~/dev1666
   cd ~/dev1666
   git clone https://github.com/deslicer/ai-sidekick-for-splunk.git
   cd ai-sidekick-for-splunk
   git checkout dev1666
   unset UV_PROJECT_ENVIRONMENT
   ```

   **Windows:**
   ```powershell
   mkdir $HOME\dev1666
   cd $HOME\dev1666
   git clone https://github.com/deslicer/ai-sidekick-for-splunk.git
   cd ai-sidekick-for-splunk
   git checkout dev1666
   ```

7. **Run the smart-install script:**

   **macOS/Linux:**
   ```bash
   unset UV_PROJECT_ENVIRONMENT
   ./scripts/smart-install.sh
   ```

   **Windows:**
   ```powershell
   .\scripts\smart-install.ps1
   ```

8. **AI Sidekick:**

⚠️ After completing the smart-install you need to provide splunk connection details. 

Lab: https://splunk.show/dev1666

Guide: https://splunk.show/dev1666-guide

If you have any issues with the lab guide or show access, contact show staff in the room.
Alternatively, we provide links to use a Deslicer Show Instance. Ensure you have access to the Splunk host, port, username and password before continuing to the next step. If you are lacking that information, reach out to one of the speakers.

   ```
   Host:
   Username:
   Password: (No echo prompt)
   ```

   **macOS/Linux:**
   ```bash
   uv run ai-sidekick --start
   ```

   **Windows:**
   ```powershell
   uv run ai-sidekick --start
   ```

9. **Open your web browser to http://localhost:8087 and verify the web interface loads successfully**

10. **Test your AI Sidekick with these queries:**(If you could run any workflow, continue with next lab)
   - "Hey Sidekick, What tools and workflows are available?"
   - "Run a system health check"
   - "List all available indexes"
   - "Use index analysis flow to analyze data in index=s4c_www and provide actionable insights"

**Detailed Instructions:**
Follow the complete guide: [setup-your-personal-ai-sidekick.md](./setup-your-personal-ai-sidekick.md)

---

### Lab 3: Create Your AI Agent

**Description:**
In this lab, you will create your own custom AI agent, learning the fundamentals of agent development and integration with the AI Sidekick framework.

**Key Learning Objectives:**
- Create FlowPilot workflow agents using template-driven architecture
- Understand auto-discovery and agent registration
- Test custom agents in the web interface
- Experience rapid development and deployment patterns

**Steps:**

11. **Create Your FlowPilot Workflow Agent with a single command:**
Open a new terminal window

**macOS/Linux:**
   ```bash
   cd ~/dev1666/ai-sidekick-for-splunk
   unset UV_PROJECT_ENVIRONMENT
   uv run ai-sidekick --create-flow-agent data_quality_check --template data_quality_check
   ```
**Windows:**
   ```powershell
   cd $HOME\dev1666\ai-sidekick-for-splunk
   uv run ai-sidekick --create-flow-agent data_quality_check --template data_quality_check
   ```

12. **Stop and restart AI Sidekick to discover new workflows:**
   ```bash
   uv run ai-sidekick --stop
   uv run ai-sidekick --start
   ```

13. **Open your browser to http://localhost:8087 and select "AI Sidekick for Splunk" from the dropdown**

14. **Discover your agent with this queries:**
   ```bash
   Execute data quality check workflow and provide recommendations
   ```

15. **Create additional workflow agents (optional):**
   ```bash
   # Security Analysis Workflow
   uv run ai-sidekick --create-flow-agent security_audit

   # Data Quality Assessment Workflow
   uv run ai-sidekick --create-flow-agent data_quality
   ```

**Detailed Instructions:**
Follow the complete guide: [create-your-ai-agent.md](./create-your-ai-agent.md)

---

## Summary

### What You've Accomplished

In this workshop, you've successfully:

- ✅ **Set up MCP Server** - Established the bridge between AI agents and your data analytics environment
- ✅ **Deployed AI Sidekick** - Created a modular multi-agent framework with specialized capabilities
- ✅ **Built Custom Agents** - Developed your own FlowPilot workflow agents using template-driven architecture
- ✅ **Experienced Auto-Discovery** - Saw automatic system integration and agent registration
- ✅ **Tested Real Functionality** - Executed multi-phase workflows via web interface

### Key Learning Points

**🚀 Rapid Development:**
- Single command creates complete workflow agents
- No coding required - just JSON configuration
- Immediate integration and availability

**📋 Template-Driven Architecture:**
- JSON templates define agent behavior
- Pydantic validation ensures correctness
- Automatic tool coordination and result synthesis

**🔧 Production-Ready System:**
- Auto-discovery enables unlimited agents
- Community contributions without code changes
- Enterprise scalability with open-source flexibility

### Next Steps

**🌟 Contribute to Open Source:**
- Share your workflow templates with the community
- Create specialized agents for your industry/use case
- Help expand the FlowPilot ecosystem

**🚀 Deploy in Production:**
- Use this pattern for enterprise workflow automation
- Create organization-specific workflow libraries
- Scale to hundreds of specialized agents

**🔧 Advanced Development:**
- Explore custom tool integration
- Build complex multi-agent workflows
- Contribute to the core FlowPilot engine

## Resources

- **🐙 GitHub Repository:** https://github.com/deslicer/ai-sidekick-for-splunk
- **🐙 GitHub Repository:** https://github.com/deslicer/mcp-for-splunk
- **📧 Support:** opensource@deslicer.com
- **📖 Documentation:** Complete guides in the repositories
- **🐛 Issues/Support:** https://github.com/deslicer/ai-sidekick-for-splunk/issues
- **🐛 Issues/Support:** https://github.com/deslicer/mcp-for-splunk/issues


---

**Your journey from zero to AI agent creator is complete! 🚀**

*The FlowPilot system you've experienced represents the future of scalable, template-driven AI agent development. You've not just used the system - you've extended it!*

**Happy Data Analytics!** 🚀
