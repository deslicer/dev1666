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

Create a new workflow agent using the built-in data quality check template:

```bash
uv run ai-sidekick --create-flow-agent data_quality_check --template data_quality_check
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
🚀 Creating FlowPilot workflow agent: data_quality_check

✅ Using built-in template: data_quality_check
✅ Workflow template created: contrib/flows/data_quality_check/data_quality_check.json
✅ Documentation created: contrib/flows/data_quality_check/README.md
✅ Pydantic validation: PASSED
✅ Schema validation: PASSED

📋 Workflow Details:
- ID: contrib.data_quality_check
- Name: Data Quality Check Agent
- Type: Data analysis workflow
- Phases: 3 (Data Discovery → Quality Assessment → Recommendations)

🎯 Next Steps:
1. Restart AI Sidekick: uv run ai-sidekick --stop && uv run ai-sidekick --start
2. Access via ADK Web: http://localhost:8087
3. Try: "Use Data Quality Check workflow"

✨ Your workflow agent is ready!
```
</details>

### What Gets Created

Your new workflow includes:

**🏗️ Workflow Structure:**
- **Data Discovery Phase** - Identify available indexes and data sources
- **Quality Assessment Phase** - Analyze data completeness, consistency, and patterns
- **Recommendations Phase** - Generate actionable data quality insights and improvements

**📊 Template Features:**
- **Built-in Template** - Uses proven data quality check patterns
- **Validated Schema** - Passes all Pydantic and system validation
- **Production-Ready** - Based on real-world data quality assessment needs
- **Educational Focus** - Clear explanations and learning opportunities
- **Real Functionality** - Uses actual Splunk MCP and result synthesizer tools

<details>
<summary>🔍 View Generated Workflow Template Structure</summary>

```json
{
  "workflow_id": "contrib.data_quality_check",
  "workflow_name": "Data Quality Check Agent",
  "version": "1.0.0",
  "description": "Comprehensive data quality assessment workflow that analyzes Splunk data for completeness, consistency, and patterns...",
  "workflow_type": "data_analysis",
  "workflow_category": "data_quality",
  "source": "contrib",
  "complexity_level": "intermediate",
  "target_audience": ["Data analysts", "Splunk administrators", "Quality engineers"],
  "core_phases": {
    "data_discovery": {
      "phase_name": "Data Discovery and Inventory",
      "tasks": [
        {
          "task_id": "discover_data_sources",
          "title": "Discover Available Data Sources",
          "tool": "splunk_mcp",
          "prompt": "Identify all available indexes and their data characteristics..."
        },
        {
          "task_id": "analyze_data_volume", 
          "title": "Analyze Data Volume Patterns",
          "tool": "splunk_mcp",
          "prompt": "Examine data ingestion patterns and volume trends..."
        }
      ]
    },
    "quality_assessment": {
      "phase_name": "Data Quality Assessment",
      "tasks": [
        {
          "task_id": "check_data_completeness",
          "title": "Assess Data Completeness",
          "tool": "splunk_mcp", 
          "prompt": "Analyze data completeness and identify gaps..."
        },
        {
          "task_id": "validate_data_consistency",
          "title": "Validate Data Consistency",
          "tool": "splunk_mcp",
          "prompt": "Check for data consistency issues and anomalies..."
        }
      ]
    },
    "recommendations": {
      "phase_name": "Quality Recommendations",
      "tasks": [
        {
          "task_id": "generate_quality_report",
          "title": "Generate Data Quality Report", 
          "tool": "result_synthesizer",
          "prompt": "Create comprehensive data quality assessment with actionable recommendations..."
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
✅ Found 2 contrib workflows (including data_quality_check)
✅ All workflows validated successfully

🤖 Creating FlowPilot agents...
✅ System_Health_Check agent created
✅ Index_Analysis agent created
✅ System_Info agent created
✅ Data_Quality_Check agent created  ← Your new agent!

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
Use Data Quality Check workflow to analyze my Splunk data
```

**Query 2: Specific Analysis**
```
Execute data quality check workflow and provide recommendations
```

<details>
<summary>✅ Expected Results</summary>

Your workflow agent will execute and show:

**🔍 Data Quality Check Analysis**

```
Summary of Findings:

• Ingestion Latency: For the access_combined sourcetype, the median ingestion latency is 2 seconds, and the 95th percentile is 3 seconds.
• Timestamp Parsing Warnings: No timestamp parsing warnings were found in the splunkd logs.
• Line Breaking Risk: No events with a length greater than or equal to 10000 characters were found, indicating no immediate line breaking risk.
• Duplicate Events: No duplicate events were found.
• Time Issues: No events with time issues (future_gt_1h or past_gt_1y) were found.
• Field Coverage Summary: The 'cookie' and 'root' fields are always null, which may indicate a data ingestion or configuration issue.
• Source Host Coverage: The sourcetype access_combined has 1 host and 1 source.
• Event Rate Stability: No significant changes in event rate were detected.
• Queue Pressure: The typingqueue has the highest fill percentage at 1.44%. The nullqueue fill percentage is 0.00%.
• Index Storage Headroom: The index 's4c_weather' is at 33.00% of its maximum size, 's4c_tutorial' is at 17.00%, and 's4c_www' is at 4.75%.
• Line Breaking Candidates (XML/JSON): No line breaking candidates were found in XML or JSON events.

Potential Issues Identified:

• The 'cookie' and 'root' fields are always null, indicating a potential data ingestion or configuration issue. Further investigation is recommended.

Recommendation:

Investigate why the 'cookie' and 'root' fields are always null, as this may indicate a data ingestion or configuration issue. Would you like me to investigate this further?
```

**💡 Key Insights from Real Analysis:**
- **Comprehensive Coverage**: The workflow analyzes ingestion latency, timestamp parsing, line breaking risks, duplicates, and field coverage
- **Performance Metrics**: Provides specific latency percentiles (median: 2s, 95th: 3s) 
- **Storage Analysis**: Shows index storage utilization across multiple indexes
- **Issue Detection**: Identifies specific problems like null fields that need investigation
- **Actionable Results**: Offers to investigate further and provides specific recommendations

**🎯 Educational Value:**
This demonstrates how FlowPilot workflows can perform production-level data quality assessments, providing detailed technical insights that help maintain healthy Splunk environments.
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