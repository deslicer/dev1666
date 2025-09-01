# Lab 2: Create your custom MCP tool (🧩)

Build your first tool with the generator, validate it, and run it in MCP Inspector.

> This lab is Part 2. If you haven’t completed Part 1 (mcp setup), finish that first so your environment and MCP server are ready.

## 1. Generate a Splunk Search tool with the helper script (🚀)

```bash
uv run generate-tool
```

Follow the instructions in the script output. or follow the simple search tool steps.
<details>
<summary><b>Steps: Create a simple search tool</b></summary>

- Select the template: ***2*** (Splunk Search)
- Choose a category: ***1*** (examples)
- Provide a tool name: ***dev1666***
- Add a tool description:
    > Tool description should define what the tool does and how it should be used.
- Splunk Search Configuration: ***2*** (single-line input)
- Provide SPL, query description and default search params (-1h, now), max returned results: 100
- Add custom search parameters?: ***2*** (No, not for this lab)
- Additional tags: just press enter
- Create tool: ***1*** (yes)
- Create Tests: ***2*** (no)
</details>


The generator creates files under `contrib/tools/<category>/` and includes boilerplate with `BaseTool`, `ToolMetadata`, and an `execute` method. It may also add starter tests under `tests/contrib/` depending on the template.

<details>
<summary>Tool Reference </summary>

Helpful reference docs:
- [Contributor guide](https://github.com/deslicer/mcp-for-splunk/blob/main/contrib/README.md)
- [Tool Development Guide](https://github.com/deslicer/mcp-for-splunk/blob/main/docs/contrib/tool_development.md) 

Understand the tool structure

- Your class inherits from `BaseTool`
- Metadata lives in `METADATA = ToolMetadata(...)`
- Main logic goes in `async def execute(self, ctx: Context)`

```python
from typing import Any, Dict
from fastmcp import Context
from src.core.base import BaseTool, ToolMetadata

class HelloWorldTool(BaseTool):
    """A simple example tool that returns a greeting."""

    METADATA = ToolMetadata(
        name="hello_world", # tool name
        description="Say hello to someone", # Tool Description
        category="examples",
        tags=["example", "tutorial"],
        requires_connection=False # requires splunk connection
    )

    async def execute(self, ctx: Context, name: str = "World") -> Dict[str, Any]:
        message = f"Hello, {name}!"
        return self.format_success_response({"message": message})
```

- For Splunk-backed tools, set `requires_connection=True` and use `await self.get_splunk_service(ctx)` inside `execute`.

</details>

## 2. Validate the generated tool (🔎)

```bash
uv run validate-tools
```

Expected output includes a success message or specific actionable validation errors to fix.

## 3. Run the tool in MCP Inspector (🖥️)

Restart the mcp server, to verify that changes take affect.

```bash
uv run mcp-server --restart
```

- Open MCP Inspector at [http://localhost:6274](http://localhost:6274)
- Connect to your MCP server
- navigate to tools tab and click list_tools
- Select your tool by its `METADATA.name` (for example `dev1666`)
- Click Run and review the formatted result

For Splunk tools, verify your `.env` connection settings. If you see connection errors, confirm `MCP_SPLUNK_HOST`, `MCP_SPLUNK_USERNAME`, and `MCP_SPLUNK_PASSWORD` are set and the Splunk instance is reachable.


***Lab Completed*** You have now created an new mcp tool, and run the tool towards your Splunk environment. Your tool is now ready to use by any AI agent. ✅

### Troubleshooting your tool

- Missing tool in Inspector: ensure the file is under `contrib/tools/<category>/` and the class inherits `BaseTool`
- Validation errors: re-run the validator for precise hints
- Splunk errors: verify credentials and try a simple search first

---

### Please continue with Lab 3 [Setup your personal AI Sidekick](setup-your-personal-ai-sidekick.md)

---

### Extra: Part 3 — Create and run a workflow

If you have extra time, try Part 3: build and execute a workflow using the workflow tools. You can discover available workflows and run them with parameters, then review results in MCP Inspector. See: [Hands-on Lab — Part 3 (Create and run a workflow)](https://github.com/deslicer/mcp-for-splunk/blob/main/docs/labs/hands-on-lab.md#part-3--extra-create-and-run-a-workflow-).


