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

## 📂 Repository Contents & Workflows

### 1. [Langgraph_with_MessagesState.ipynb](Langgraph_with_MessagesState.ipynb)
**Foundation & Basics**
* **Goal**: Introduction to the core concepts of LangGraph.
* **Features**: Basic `StateGraph` setup, `MessagesState` management, and simple chatbot flow.

```mermaid
graph LR
    __start__([Start]) --> chatbot
    chatbot --> __end__([End])
    style chatbot fill:#f9f,stroke:#333,stroke-width:2px
