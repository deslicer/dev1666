# Unix (macOS & Linux) Setup Guide

This guide covers installing prerequisites and running the MCP Server for Splunk on macOS and Linux.

## 🚀 Quick Start (Recommended)

### 1) Clone the repository

```bash
git clone https://github.com/deslicer/mcp-for-splunk.git
cd mcp-for-splunk
# Checkout dev1666 branch in git, this branch has a prepared .env file for you.
git checkout dev1666
```
### 2) Copy the lab environment
```bash
cp env.lab .env
```

### 3) Install prerequisites (uv, Node.js, Python via uv)
```bash
./scripts/smart-install.sh
```

### 4) Run the server locally

```python
uv run mcp-server --local -d
# Updated SPLUNK_PASSWORD will be provided by instructors
```

### 5) Verify the mcp server and Splunk connection

```python
uv run mcp-server --test -detailed
```

<details>
<summary>View sample successful output</summary>

```bash
== MCP Server Check ==
URL: http://0.0.0.0:8003/mcp/
• MCP Server: OK ✅
• Tools: 39 | Resources: 17

-- Splunk Health --
• Status: Connected ✅
• Server: sh-i-0b8d6e25a.deslicer.splunkcloud.com
• Version: 9.3.2411.113
• Source: server_config
```
</details>

**Lab complete:** If the script returns MCP Server: OK ✅ and Splunk Health  Status: Connected ✅ you have successfully completed the set up lab.

If Splunk shows "Not connected ❌":

- Verify your `.env` file contains correct values for `SPLUNK_HOST`, `SPLUNK_PORT`, `SPLUNK_USERNAME`, `SPLUNK_PASSWORD`, `SPLUNK_SCHEME`, `SPLUNK_VERIFY_SSL`.
  ```python
  uv run mcp-server --setup --local -d
  ```
  
