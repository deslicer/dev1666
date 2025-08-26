<div align="center">
  <img src="./media/deslicer_white.svg" alt="Deslicer" width="200"/>
</div>

# DEV1666 - AI Sidekick for Splunk Lab Exercises

## Table of Contents

1. [Overview](#overview)
2. [Prerequisites](#prerequisites)
3. [Lab Connection Info](#lab-connection-info)
4. [Lab Exercises](#lab-exercises)
   - [Lab Exercise 1: Set up your MCP server for Splunk](#lab-exercise-1---set-up-your-mcp-server-for-splunk)
   - [Lab Exercise 2: Create your custom MCP tool](#lab-exercise-2---create-your-custom-mcp-tool)
   - [Lab Exercise 3: Set up your personal AI Sidekick](#lab-exercise-3---set-up-your-personal-ai-sidekick)
   - [Lab Exercise 4: Create your AI agent](#lab-exercise-4---create-your-ai-agent)
5. [Summary](#summary)

## Overview

This workshop is designed to help you understand how to connect AI with your Splunk Enterprise environment. You'll learn to build AI agents using the Model Context Protocol (MCP) and create intelligent sidekicks that can interact with your Splunk data.

## Prerequisites

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
  - Basic understanding of Splunk concepts (indexes, searches)
  - No programming experience required (we'll guide you through everything!)

- **🔧 Software (will be installed during labs):**
  - Python 3.11+
  - Git
  - Node.js (optional, for MCP Inspector)

## Lab Connection Info

You will be receiving instructions from Splunk about Splunk Show environment details. If you do not receive these details, please let one of the instructors know and we will fix it. Alternatively, we provide instructions to run Splunk in your local Docker environment for those who prefer a local setup.

## Lab Exercises

### Lab Exercise 1 - Set up your MCP server for Splunk

**Description:**
In this lab you will set up your own MCP (Model Context Protocol) server for Splunk, which serves as the bridge between AI agents and your Splunk environment.

**Steps:**
Follow the instructions provided in [1-set-up-your-mcp-server-for-splunk.md](./1-set-up-your-mcp-server-for-splunk.md)

---

### Lab Exercise 2 - Create your custom MCP tool

**Description:**
In this lab you will create your own custom MCP tool, deploy it in your local environment, and test it using MCP Inspector to ensure proper functionality.

**Steps:**
Follow the detailed lab instructions provided in [1-create-your-custom-mcp-tool.md](./1-create-your-custom-mcp-tool.md)

---

### Lab Exercise 3 - Set up your personal AI Sidekick

**Description:**  
In this lab, you will set up and configure your personal AI Sidekick for Splunk. You'll explore the multi-agent system architecture and learn how to assign tasks to different specialized agents.

**Steps:**  
Choose the setup guide that matches your operating system:

- **🚀 Quick Start (All Platforms):** [Beginners Setup Guide](./docs/ai_sidekick/BEGINNERS_SETUP.md)
- **🪟 Windows Users:** [Windows Setup Guide](./docs/ai_sidekick/WINDOWS_GUIDE.md)
- **🍎 macOS Users:** [macOS Setup Guide](./docs/ai_sidekick/MACOS_GUIDE.md)
- **🐧 Linux Users:** [Linux Setup Guide](./docs/ai_sidekick/LINUX_GUIDE.md)
- **📖 Detailed Guide:** [Complete Setup Instructions](./3-setup-your-personal-ai-sidekick.md)

---

### Lab Exercise 4 - Create your AI agent

**Description:**
In this lab, you will create your own custom AI agent from scratch, learning the fundamentals of agent development and integration with the AI Sidekick framework.

**Steps:**
Follow the detailed instructions provided in [4-create-your-ai-agent.md](./4-create-your-ai-agent.md)

---

## Summary

In this workshop, we explored AI agents and the Model Context Protocol (MCP), discovering how to connect AI with your Splunk data. These exercises mirror real-world activities that customers conduct in their environments, empowering you to integrate and automate actions in Splunk Enterprise with an intelligent AI sidekick.

The skills you've learned enable you to:
- ✅ Set up MCP servers for Splunk integration
- ✅ Create custom MCP tools for specific use cases
- ✅ Deploy and configure AI Sidekick agents
- ✅ Build your own specialized AI agents
- ✅ Integrate AI capabilities with Splunk Enterprise workflows

## Resources

- **🐙 GitHub Repository:** https://github.com/desclier/ai-sidekick-for-splunk
- **📧 Support:** opensource@deslicer.com

**Happy Splunking!** 🚀
