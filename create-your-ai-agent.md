# Lab 4: Create Your AI Agent

**Build your own specialized AI agent for Splunk index analysis!**

## What You'll Build

**Complete Index Analyzer Agent with Orchestrator Integration**

You'll create a fully functional Splunk index analysis agent using a systematic 3-step process:
1. **Create** - Generate the base agent structure for contributors
2. **Implement** - Add complete working 5-phase analysis workflow
3. **Integrate** - Connect agent to the main orchestrator as agent tool

## Prerequisites

- Completed Lab 3: Setup Your Personal AI Sidekick
- Basic Python knowledge
- Familiarity with Splunk indexes and SPL

---

## Step 1: Create Agent Structure

Generate the base agent structure that contributors can use:

```bash
./scripts/agent/create-agent.sh index_analyzer
```

**This creates the contributor-ready structure:**
```
index_analyzer/
├── __init__.py      # ← Auto-discovery setup
├── agent.py         # ← Agent class with metadata (methods as TODO)
├── prompt.py        # ← Placeholder for instructions
└── README.md        # ← Documentation
```

**What you get:**
- ✅ **Base agent class** - Proper inheritance and metadata
- ✅ **Auto-discovery setup** - Factory functions and exports
- ✅ **Method placeholders** - TODO comments for core methods
- ✅ **Prompt structure** - Ready for specific instructions

> **💡 Key Learning:** This creates the foundation that any contributor can use to build agents!

---

## Step 2: Add Working Implementation

Add the complete 5-phase workflow implementation:

```bash
./scripts/agent/add-agent.sh index_analyzer
```

**This adds the complete working agent:**

### 2.1 What Gets Added

#### **📋 Complete Index Analyzer Prompt (prompt.py)**
Full 5-phase workflow instructions with real SPL queries:
- ✅ **Phase 1:** Data Types Discovery with tstats analysis
- ✅ **Phase 2:** Field Analysis with fieldsummary
- ✅ **Phase 3:** Sample Data Collection with real events
- ✅ **Phase 4:** Volume Assessment with REST API
- ✅ **Phase 5:** Business Insights with persona-based use cases

#### **🔧 Working Agent Methods (agent.py)**
Complete implementation of all core methods:
- ✅ **`execute()`** - Full 5-phase workflow with structured output
- ✅ **`get_adk_agent()`** - ADK integration for orchestrator
- ✅ **`supports_streaming()`** - Streaming capability detection
- ✅ **`validate_input()`** - Input validation logic
- ✅ **`get_capabilities()`** - Capability listing

### 2.2 Implementation Highlights

#### **🎯 Real Working Execute Method**
```python
def execute(self, task: str, context: Optional[dict[str, Any]] = None) -> dict[str, Any]:
    # Extract index name from task
    index_match = re.search(r'index[=\s]+([^\s]+)', task.lower())

    # Return structured analysis with:
    # - 5 analysis phases with SPL queries
    # - Business insights for 3 personas
    # - Actionable recommendations
```

#### **📊 Structured Output**
- **Analysis Phases** - Each phase with SPL query and findings
- **Business Insights** - SecOps, DevOps, and Business Analyst use cases
- **Recommendations** - Actionable next steps

> **💡 Workshop Focus:** You now have a complete, working agent ready for testing!

---

## Step 3: Integrate with Orchestrator

Connect your agent to the main orchestrator so it can be called as a tool:

```bash
./scripts/agent/integrate-agent.sh index_analyzer
```

**This integrates your agent with the orchestrator:**

### 3.1 What Gets Integrated

#### **🔗 Agent Import**
Adds your agent to the main orchestrator imports:
```python
from .contrib.agents.index_analyzer.agent import index_analyzer_agent
```

#### **🛠️ Agent Tool**
Adds your agent as an AgentTool in the orchestrator:
```python
tools = [
    # ... existing tools ...
    AgentTool(index_analyzer_agent),
]
```

#### **📝 Orchestrator Prompt**
Updates the orchestrator prompt to document your agent:
```
## Index Analyzer Agent
- **Purpose**: Systematic Splunk index analysis and business insight generation
- **Capabilities**: 5-phase analysis workflow
- **Usage**: "Use index_analyzer to analyze index=<index_name>"
```

### 3.2 Integration Benefits

- ✅ **Seamless Routing** - Orchestrator automatically delegates to your agent
- ✅ **Tool Discovery** - Your agent appears in available tools
- ✅ **Proper Documentation** - Users know how to invoke your agent
- ✅ **Production Ready** - Full integration with the AI Sidekick system

---

## Step 4: Test Your Complete Agent

**1. Start the ADK lab environment:**
```bash
./scripts/lab/start-lab-setup.sh
```

**2. Test your agent integration:**

**Option A: Direct Python Test**
```bash
cd src && uv run python -c "
from splunk_ai_sidekick.contrib.agents.index_analyzer import index_analyzer_agent
result = index_analyzer_agent.execute('analyze index=pas')
print('Agent Response:', result['message'])
print('Business Insights:', len(result['business_insights']))
"
```

**Option B: Web Interface Test**
- Open `http://localhost:8087` in your browser
- Try: "Use index analyzer to analyze index=pas"
- Try: "Help me analyze index=_internal with the index analyzer"

### 4.1 Expected Results

Your agent is **fully functional and integrated**! Here's what you'll see:

#### **✅ Complete Analysis Output**
```json
{
  "success": true,
  "message": "Index analysis completed for index=pas",
  "analysis_phases": {
    "phase_1": {
      "name": "Data Types Discovery",
      "spl_query": "| tstats summariesonly=true count WHERE index=pas by _time, sourcetype...",
      "findings": "Discovered primary data types and ingestion patterns"
    },
    // ... 4 more phases
  },
  "business_insights": [
    {
      "persona": "SecOps Analyst",
      "use_case": "Security Monitoring Dashboard",
      "dashboard_query": "index=pas | stats count by sourcetype..."
    },
    // ... 2 more personas
  ],
  "recommendations": [
    "Set up automated dashboards for continuous monitoring",
    // ... more recommendations
  ]
}
```

#### **✅ Orchestrator Integration**
- Agent appears in orchestrator tools
- Requests are properly routed
- Structured responses are returned
- Full ADK compatibility

---

## Step 5: Understanding Your Creation

### 5.1 What You Built

**🏗️ Architecture Pattern**
- **Base Structure** - Standard agent foundation for contributors
- **Working Implementation** - Complete 5-phase analysis workflow
- **Orchestrator Integration** - Full tool integration with routing

**🔧 Technical Components**
- **Agent Class** - Inherits from BaseAgent with proper metadata
- **ADK Integration** - LlmAgent creation for orchestrator compatibility
- **Structured Output** - JSON responses with analysis phases and insights
- **Tool Registration** - AgentTool wrapper for seamless delegation

### 5.2 Key Learning Points

**📋 3-Step Development Process**
1. **Structure First** - Create reusable foundation
2. **Implementation Second** - Add working functionality
3. **Integration Third** - Connect to orchestrator system

**🎯 Production Patterns**
- **Auto-discovery** - Agents are automatically found and registered
- **Tool Delegation** - Orchestrator routes requests to appropriate agents
- **Structured Responses** - Consistent output format across all agents
- **Real Integration** - Not just demos, but production-ready components

### 5.3 Next Steps

**🚀 Enhancement Opportunities**
- Add real SplunkMCP delegation for live data
- Implement streaming responses for long-running analysis
- Add error handling and validation
- Create custom visualizations for insights

**🔧 Development Workflow**
- Use the 3-script process for new agents
- Follow the established patterns for consistency
- Test integration at each step
- Document capabilities in orchestrator prompt

---

## Congratulations! 🎉

You've successfully created a **complete, working AI agent** that:

- ✅ **Follows established patterns** for contributor-friendly development
- ✅ **Implements real functionality** with structured 5-phase analysis
- ✅ **Integrates seamlessly** with the orchestrator system
- ✅ **Provides business value** with actionable insights and recommendations

**Your IndexAnalyzer agent is now part of the AI Sidekick ecosystem and ready for production use!**

The 3-step process you learned (Create → Implement → Integrate) is the standard workflow for building agents in this system. You can now use this same process to create any specialized agent for your Splunk environment!
