# For the [Ready Tensor Agentic AI 2025 Competition](https://www.readytensor.ai/agentic-ai-2025/)

This project is maintaining multiple implementations for different use cases.

## Environment Configuration

- Docker
  - AttackBox:
    - Kali
    - Nmap
    - Metasploit
    - Hashcat
  - TargetBox: Win7
- Python
- Deno/TS
- Open-Webui
- Ollama
  - [Local AI Setup](https://cmndcntrl.notion.site/local-ai-setup)

### Models

The pentest-agent-system submodule can be extended to include support for more model providers. The current implementation features support for multiple models from OpenAI or Anthropic.

- [Antrhopic](https://anthropic.com)
- [OpenAI](https://openai.com)

[qwen2.5-coder:7b](https://ollama.com/library/qwen2.5-coder)
[deepseek-r1:7b](https://ollama.com/library/deepseek-r1)

### Cloudflare AI Workers

[deepseek-r1-distill-qwen-32b](https://developers.cloudflare.com/workers-ai/models/deepseek-r1-distill-qwen-32b/)

## Tools

- Kali
- Nmap
- Metasploit
- hashcat
- More to come!

## Researcher

- Submodule: pentest-agent-system/Security Analyst Agent

## Orchestration Agent

- Submodule: pentest-agent-system/Orchestrator Agent

## Planner

- [ATT&CK PLANNER](https://github.com/cmndcntrlcyber/attck-planner)
- Submodule: pentest-agent-system/Security Analyst Agent

## Executor

- [ATT&CK-PE (Portable Executor)](https://cmndcntrl.notion.site/portable-executor)
- Submodule: pentest-agent-system/Orchestrator Agent
  - Executor Agent in development.

## LLM-based Agents in the Pentest-Agent-System

The system follows a hybrid approach:

The Python implementation uses LLM-based agents with a Streamlit UI
The Deno implementation uses a structured multi-agent architecture

### Architecture Overview

LLM-based agents are being used in several places in this repository:

1. Main Production Agent (Python Implementation)
The primary LLM-based agent is implemented in python/main.py:
   - Uses LangChain's create_tool_calling_agent and AgentExecutor
   - Supports two LLM backends:
     - Claude (Anthropic) via ChatAnthropic
     - GPT-4o mini (OpenAI) via ChatOpenAI
   - Implements a Streamlit-based UI for user interaction
   - Has access to multiple specialized tools:
     - nmap_tool: For network scanning
     - security_analyst_tool: For vulnerability analysis
     - metasploit_search_tool and metasploit_process_tool: For exploit discovery
     - search_tool and wiki_tool: For web research
     - save_tool: For saving findings

    This agent serves as the main interface for the Python implementation of the system, handling user queries and orchestrating the penetration testing workflow.

2. Experimental/Example Agents
There are also some experimental or example agent implementations:
   - `python/modules/oai-agent-00.py:`
     - A simple example agent that generates a haiku about recursion
     - Uses an Agent class from an "agents" module

   - `python/modules/react-agent.py:`
     - An experimental implementation using LangGraph's create_react_agent
     - Uses OpenAI's GPT-4o mini model
     - Set up to perform nmap scans (though appears to be incomplete)

3. Deno Implementation (TypeScript)
The pentest-agent-system submodule repository also contains a Deno/TypeScript implementation that follows a multi-agent architecture as described in `SYSTEM_OVERVIEW.md`:

   - Orchestrator Agent: Coordinates the overall operation flow
     - Implemented as `PentestOrchestratorAgent` in `agents/orchestrator.ts`
   - Planner Agent: Generates attack plans based on MITRE ATT&CK framework
     - Implemented as `MitrePlannerAgent` in `agents/planner.ts`
   - Executor Agent: Executes attack plans against target systems
     - Implemented as `ExploitExecutorAgent` in `agents/executor.ts`

The TypeScript implementation appears is more focused on structured, rule-based agents following the MITRE ATT&CK framework.
