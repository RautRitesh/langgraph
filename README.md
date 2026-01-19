# LangGraph Agents & Workflows

A comprehensive collection of tutorials and implementations demonstrating how to build stateful, agentic AI applications using **LangGraph**. This repository explores various patterns including basic chatbots, tool calling, human-in-the-loop workflows, and specialized domain agents.

## 🚀 Overview

This project serves as a practical guide to mastering **LangGraph**, a library for building stateful, multi-actor applications with LLMs. The notebooks cover a progression from simple graph structures to complex, multi-agent systems with decision-making capabilities.

### Key Features
* **State Management**: Efficient handling of conversation history using `MessagesState`.
* **Tool Integration**: Seamless connection of agents to external tools (Tavily Search, YFinance, Custom Functions).
* **Human-in-the-Loop (HITL)**: Workflows that pause for user approval before executing sensitive or costly actions.
* **Conditional Routing**: Dynamic graph edges that decide the next step based on agent output (e.g., Tool vs. End).
* **Memory & Persistence**: Using `MemorySaver` to maintain context across conversation turns.
* **Domain Specific Agents**: Implementation of a Financial Analyst agent.

## 🛠️ Tech Stack

* **Framework**: [LangGraph](https://langchain-ai.github.io/langgraph/), [LangChain](https://www.langchain.com/)
* **LLM Provider**: [Groq](https://groq.com/) (using `openai/gpt-oss-20b` and other models)
* **Search Engine**: [Tavily AI](https://tavily.com/)
* **Financial Data**: [yfinance](https://pypi.org/project/yfinance/)
* **Vector Store**: FAISS (referenced in advanced agents)

## 📂 Repository Contents

### 1. [Langgraph_with_MessagesState.ipynb](Langgraph_with_MessagesState.ipynb)
**Foundation & Basics**
* **Goal**: Introduction to the core concepts of LangGraph.
* **Features**:
    * Setting up a basic `StateGraph`.
    * Using `MessagesState` to append and manage chat history.
    * Binding tools to an LLM.
    * Implementing a basic `router` to switch between generating text and calling tools.
    * Adding conversation memory using checkpoints.
  ```mermaid
graph LR
    __start__([Start]) --> chatbot
    chatbot --> __end__([End])
    style chatbot fill:#f9f,stroke:#333,stroke-width:2px

### 2. [Human_in_the_loop.ipynb](Human_in_the_loop.ipynb)
**Interactive Workflows**
* **Goal**: Implement a workflow where the agent requires human permission to proceed.
* **Features**:
    * Custom tool logic that intercepts specific actions (e.g., "Search").
    * Prompts the user: *"Do you want me to use the tavily search it will cost you[Y/N]"*.
    * Conditional execution based on user input (Yes/No).
    * Demonstrates how to interrupt graph execution for human feedback.

  ```mermaid
  graph TD
    __start__([Start]) --> agent
    agent -->|Tool Call| tools[Tool Node]
    agent -->|No Tool| human[Human Review]
    
    tools --> agent
    
    human -->|Rejected/Feedback| agent
    human -->|Approved| __end__([End])

    style human fill:#ffcc00,stroke:#333,stroke-width:2px
    style agent fill:#f9f,stroke:#333,stroke-width:2px

### 3. [Advanced_agent_with_decision_making.ipynb](Advanced_agent_with_decision_making.ipynb)
**Complex Routing & Safety**
* **Goal**: Build an agent that can dynamically choose between "safe" and "risky" paths.
* **Features**:
    * Integration of PDF document loading (RAG concepts).
    * Categorization of tools into "risky" (e.g., internet search) and "safe".
    * A router function that directs the flow to specific nodes based on the tool requested.
    * Uses `HuggingFaceEmbeddings` and vector stores for context retrieval.

     ```mermaid
  graph TD
    __start__([Start]) --> agent
    
    agent -->|Search Request| risky[Risky Tools Node]
    agent -->|Calculation| safe[Safe Tools Node]
    agent -->|Final Answer| __end__([End])
    
    risky --> agent
    safe --> agent

    style risky fill:#ff9999,stroke:#333,stroke-width:2px
    style safe fill:#99ff99,stroke:#333,stroke-width:2pxe


### 4. [financial_analyst_agents.ipynb](financial_analyst_agents.ipynb)
**Domain-Specific Implementation**
* **Goal**: Create a "Senior Financial Analyst" agent.
* **Features**:
    * **Tools**:
        * `lookup_ticker`: Finds the correct stock symbol for a company name (e.g., "Apple" -> "AAPL").
        * `get_stock_data`: Fetches historical stock data using `yfinance`.
        * `optimized_search`: Searches for news to explain market movements.
    * **Workflow**: The agent identifies the ticker, retrieves data, and synthesizes an explanation for stock performance.
    ```mermaid
  graph LR
    __start__([Start]) --> agent
    agent -->|Tools Condition| tools[Financial Tools]
    tools --> agent
    agent -->|Response| __end__([End])
    
    style tools fill:#66ccff,stroke:#333,stroke-width:2px

## ⚡ Installation

To run these notebooks, you will need to install the required Python packages. You can install them using pip:

```bash
pip install langgraph langchain langchain-groq langchain-community tavily-python yfinance faiss-cpu pypdf
