# Multi-Agent Customer Service System with A2A and MCP

## Overview
This project implements a **distributed multi-agent customer service system** designed to handle customer requests automatically. It leverages:

- **Agent-to-Agent (A2A) communication** for inter-agent task delegation.  
- **Model Context Protocol (MCP)** for standardized, secure agent interactions.  
- **LLM-based intent classification** to route requests accurately.  

The system consists of three core agents:

1. **Customer Data Agent** – Handles data retrieval and updates.  
2. **Support Agent** – Manages specialized tasks such as refunds, subscription changes, and escalations.  
3. **Router Agent** – Interprets user queries via an LLM, determines intent, and routes tasks to the appropriate agent.

---

## Setup Instructions

1. **Clone the repository**:
git clone https://github.com/Aadya04/multi_agent.git
cd multi_agent

Install dependencies:
pip install -qr requirements.txt
pip install pyngrok nest_asyncio uvicorn --quiet

Prepare environment variables (replace with your tokens):
import os

os.environ['HF_TOKEN'] = "<YOUR_HF_TOKEN>"
os.environ['NGROK_AUTHTOKEN'] = "<YOUR_NGROK_TOKEN>"

Create logs directory:
mkdir logs

Launch agents:
python -m mcp_server.main > logs/mcp_server.log 2>&1 &
python -m agents.customer_data_agent > logs/data_agent.log 2>&1 &
python -m agents.support_agent > logs/support_agent.log 2>&1 &
python -m agents.router_agent > logs/router_agent.log 2>&1 &

Run test scenarios:
python tests/run_scenarios.py

