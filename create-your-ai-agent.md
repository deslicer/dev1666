# Lab 4: Create Your AI Agent

**Build your own specialized FlowPilot workflow agent in minutes!**

## What You'll Build

**Complete FlowPilot Workflow Agent with Auto-Discovery**

You'll create a fully functional workflow agent that:
1. **Generate** - Create a validated workflow template using one simple command
2. **Discover** - Automatically integrates into the AI Sidekick system
3. **Execute** - Ready to use immediately via ADK web interface

## Prerequisites

- Completed Lab 3: Setup Your Personal AI Sidekick
- AI Sidekick running with activated virtual environment
- Basic understanding of Splunk concepts

---

## Step 1: Create Your FlowPilot Workflow Agent

Create a new workflow agent with a single command:

```bash
uv run ai-sidekick --create-flow-agent workshop_demo
```

<details>
<summary>📋 What this command does</summary>

The unified script will:
- ✅ **Generate Template** - Create a fully validated workflow JSON using Pydantic models
- ✅ **Auto-Validation** - Ensure template passes all schema requirements
- ✅ **Smart Placement** - Place in `contrib/flows/` for community workflows
- ✅ **Documentation** - Generate README.md with workflow details
- ✅ **Integration Ready** - Workflow is immediately discoverable by the system

**Expected Output:**
```
🚀 Creating FlowPilot workflow agent: workshop_demo

✅ Workflow template created: contrib/flows/workshop_demo/workshop_demo.json
✅ Documentation created: contrib/flows/workshop_demo/README.md
✅ Pydantic validation: PASSED
✅ Schema validation: PASSED

📋 Workflow Details:
- ID: contrib.workshop_demo
- Name: DevWorkshop_Demo_Workshop System Health Agent
- Type: Troubleshooting workflow
- Phases: 3 (System Info → Health Checks → Summary Report)

🎯 Next Steps:
1. Restart AI Sidekick: uv run ai-sidekick --stop && uv run ai-sidekick --start
2. Access via ADK Web: http://localhost:8087
3. Try: "Use Workshop Demo workflow"

✨ Your workflow agent is ready!
```
</details>

### What Gets Created

Your new workflow includes:

**🏗️ Workflow Structure:**
- **System Information Phase** - Gather Splunk version and available indexes
- **Health Assessment Phase** - Check data flow and basic performance
- **Summary Report Phase** - Generate educational insights for workshop participants

**📊 Template Features:**
- **Validated Schema** - Passes all Pydantic and system validation
- **Educational Focus** - Designed for workshop learning objectives
- **Beginner Friendly** - Clear explanations and encouraging feedback
- **Real Functionality** - Uses actual Splunk MCP and result synthesizer tools

<details>
<summary>🔍 View Generated Workflow Template Structure</summary>

```json
{
  "workflow_id": "contrib.workshop_demo",
  "workflow_name": "DevWorkshop_Demo_Workshop System Health Agent",
  "version": "1.0.0",
  "description": "A simple workshop demonstration agent that performs basic Splunk environment health checks...",
  "workflow_type": "troubleshooting",
  "workflow_category": "system_health",
  "source": "contrib",
  "complexity_level": "beginner",
  "target_audience": ["Workshop participants", "Splunk beginners", "FlowPilot learners"],
  "core_phases": {
    "system_info": {
      "phase_name": "System Information Gathering",
      "tasks": [
        {
          "task_id": "gather_splunk_version",
          "title": "Gather Splunk Version",
          "tool": "splunk_mcp",
          "prompt": "Please retrieve the Splunk version information..."
        },
        {
          "task_id": "list_available_indexes", 
          "title": "List Available Indexes",
          "tool": "splunk_mcp",
          "prompt": "List all available Splunk indexes..."
        }
      ]
    },
    "health_checks": {
      "phase_name": "Basic Health Assessment",
      "tasks": [
        {
          "task_id": "check_recent_data",
          "title": "Check Recent Data",
          "tool": "splunk_mcp", 
          "prompt": "Search for events from the last 24 hours..."
        },
        {
          "task_id": "check_system_performance",
          "title": "Check System Performance",
          "tool": "splunk_mcp",
          "prompt": "Check basic system performance..."
        }
      ]
    },
    "summary_report": {
      "phase_name": "Health Summary Report",
      "tasks": [
        {
          "task_id": "generate_health_summary",
          "title": "Generate Health Summary", 
          "tool": "result_synthesizer",
          "prompt": "Based on the system information and health checks performed, create a clear and friendly summary report..."
        }
      ]
    }
  }
}
```
</details>

---

## Step 2: Restart and Discover Your Agent

### Restart AI Sidekick to discover the new workflow:

```bash
# Stop current session
uv run ai-sidekick --stop

# Start fresh session (discovers new workflows)
uv run ai-sidekick --start
```

<details>
<summary>📋 What happens during restart</summary>

**Auto-Discovery Process:**
- ✅ **Scan Workflows** - System scans `core/flows/` and `contrib/flows/` directories
- ✅ **Validate Templates** - Each JSON template is validated against Pydantic schema
- ✅ **Create Agents** - Valid workflows become FlowPilot agents automatically
- ✅ **Register Tools** - Agents are registered as available tools in the orchestrator
- ✅ **Update Web UI** - New agents appear in the ADK web interface

**Expected Output:**
```
🔍 Discovering workflows...
✅ Found 4 core workflows
✅ Found 2 contrib workflows (including workshop_demo)
✅ All workflows validated successfully

🤖 Creating FlowPilot agents...
✅ System_Health_Check agent created
✅ Index_Analysis agent created
✅ System_Info agent created
✅ Workshop_Demo agent created  ← Your new agent!

🚀 AI Sidekick ready with 6 workflow agents
🌐 Web interface: http://localhost:8087
```
</details>

---

## Step 3: Test Your Agent in ADK Web

### Access the Web Interface

1. **Open your browser** to http://localhost:8087
2. **Select Agent** - Choose "AI Sidekick for Splunk" from the dropdown
3. **Test Your Workflow** - Try these example queries

### Example Queries to Test

**Query 1: Direct Workflow Invocation**
```
Use Workshop Demo workflow to check my Splunk environment
```

**Query 2: Natural Language Request**
```
Run the workshop demo health check
```

**Query 3: Specific Analysis**
```
Execute workshop demo workflow and explain the results for beginners
```

<details>
<summary>✅ Expected Results</summary>

Your workflow agent will execute and show:

**Phase 1: System Information Gathering**
```
🔍 Gathering Splunk Version...
✅ Splunk Enterprise 9.4.0 (Build: abc123)
✅ System configured and operational

📋 Listing Available Indexes...
✅ Found 8 indexes: main, _internal, _audit, pas, security, web_logs, app_logs, network
✅ Data landscape mapped successfully
```

**Phase 2: Basic Health Assessment**
```
📊 Checking Recent Data Flow...
✅ 1,234,567 events indexed in last 24 hours
✅ Data ingestion active and healthy

⚡ Assessing System Performance...
✅ Average search response time: 0.8 seconds
✅ System performance within normal parameters
```

**Phase 3: Health Summary Report**
```
📋 Workshop Health Summary Report

🎯 System Overview:
Your Splunk environment is healthy and ready for workshop activities!

📊 Key Findings:
- ✅ Splunk 9.4.0 running smoothly
- ✅ 8 indexes available for exploration
- ✅ Active data flow (1.2M events/day)
- ✅ Good system performance

🚀 Workshop Recommendations:
1. Use 'pas' index for hands-on exercises (rich sample data)
2. Try 'security' index for security analysis scenarios
3. Explore '_internal' for system monitoring examples

💡 Educational Insight:
This workflow demonstrates how FlowPilot agents coordinate multiple tools (Splunk MCP + Result Synthesizer) to deliver comprehensive analysis. You've just seen a 3-phase workflow execute seamlessly!

🎉 Your Splunk environment is workshop-ready!
```
</details>

---

## Step 4: Understanding Your Creation

### What You Built

**🏗️ FlowPilot Workflow Agent**
- **Template-Driven** - JSON configuration defines behavior
- **Auto-Discovery** - System finds and integrates automatically
- **Multi-Phase** - Structured workflow with clear progression
- **Tool Coordination** - Orchestrates Splunk MCP and Result Synthesizer
- **Educational Focus** - Designed for learning and demonstration

### Key Architecture Benefits

**🚀 Instant Integration**
- No code changes required in core system
- Automatic discovery and registration
- Immediate availability in web interface

**📋 Template Validation**
- Pydantic schema ensures correctness
- Prevents runtime errors
- Maintains system stability

**🔧 Tool Orchestration**
- Coordinates multiple specialized tools
- Structured phase-by-phase execution
- Comprehensive result synthesis

**🎯 Scalable Design**
- Add unlimited workflow agents
- Community contributions without code changes
- Enterprise and open-source hybrid model

<details>
<summary>🔍 Advanced: How Auto-Discovery Works</summary>

**Discovery Process:**
1. **Scan Directories** - System scans `core/flows/` and `contrib/flows/`
2. **Load Templates** - Each `.json` file is loaded and parsed
3. **Validate Schema** - Pydantic models ensure template correctness
4. **Create Agents** - Valid templates become FlowPilot agent instances
5. **Register Tools** - Agents are wrapped as AgentTools for orchestrator
6. **Update Registry** - New agents appear in available tools list

**Dynamic Factory Pattern:**
```python
# Simplified view of what happens internally
def discover_workflows():
    workflows = scan_workflow_directories()
    for template in workflows:
        if validate_template(template):
            agent = create_flowpilot_agent(template)
            register_agent_tool(agent)
```

This means you can add unlimited workflow agents just by creating JSON templates!
</details>

---

## Step 5: Create More Workflow Agents (Optional)

Try creating additional workflow agents for different scenarios:

### Security Analysis Workflow
```bash
uv run ai-sidekick --create-flow-agent security_audit
```

### Performance Monitoring Workflow
```bash
uv run ai-sidekick --create-flow-agent performance_monitor
```

### Data Quality Assessment Workflow
```bash
uv run ai-sidekick --create-flow-agent data_quality
```

Each workflow will:
- ✅ Generate with appropriate templates for the use case
- ✅ Auto-integrate after restart
- ✅ Be immediately available in ADK web interface
- ✅ Provide structured, educational results

---

## 🎉 Congratulations!

You've successfully created and deployed your own FlowPilot workflow agent!

### What You've Accomplished:
- ✅ **Built a Workflow Agent** - Created template-driven AI agent in minutes
- ✅ **Experienced Auto-Discovery** - Saw automatic system integration
- ✅ **Tested Real Functionality** - Executed multi-phase workflows via web interface
- ✅ **Understood Architecture** - Learned scalable, template-driven design

### Key Learning Points:

**🚀 Rapid Development**
- Single command creates complete workflow agent
- No coding required - just JSON configuration
- Immediate integration and availability

**📋 Template-Driven Architecture**
- JSON templates define agent behavior
- Pydantic validation ensures correctness
- Automatic tool coordination and result synthesis

**🔧 Production-Ready System**
- Auto-discovery enables unlimited agents
- Community contributions without code changes
- Enterprise scalability with open-source flexibility

### Next Steps:

**🌟 Contribute to Open Source**
- Share your workflow templates with the community
- Create specialized agents for your industry/use case
- Help expand the FlowPilot ecosystem

**🚀 Deploy in Production**
- Use this pattern for enterprise workflow automation
- Create organization-specific workflow libraries
- Scale to hundreds of specialized agents

**🔧 Advanced Development**
- Explore custom tool integration
- Build complex multi-agent workflows
- Contribute to the core FlowPilot engine

---

## Resources

- **GitHub Repository:** https://github.com/deslicer/ai-sidekick-for-splunk
- **FlowPilot Documentation:** Complete workflow development guides
- **Community Templates:** Share and discover workflow templates
- **Issues/Support:** https://github.com/deslicer/ai-sidekick-for-splunk/issues

---

**Your journey from zero to AI agent creator is complete! 🚀**

*The FlowPilot system you've experienced represents the future of scalable, template-driven AI agent development. You've not just used the system - you've extended it!*