# Corrective Local RAG with Qwen

<img width="584" alt="Screenshot 2025-04-25 at 07 28 07" src="https://github.com/user-attachments/assets/2587ba70-c850-49b4-a204-81beac85ba63" />

<img width="1269" alt="Screenshot 2025-04-25 at 09 57 15" src="https://github.com/user-attachments/assets/b03964cf-abd8-4889-b389-e4706d049d76" />

<img width="599" alt="Screenshot 2025-04-25 at 10 00 03" src="https://github.com/user-attachments/assets/c971f4fa-96da-4a5c-b317-73f1f48425a3" />

<img width="1023" alt="Screenshot 2025-04-25 at 10 10 57" src="https://github.com/user-attachments/assets/b5ebe5d2-c904-424e-a8f0-f798871999fd" />


[![Python](https://img.shields.io/badge/Python-3.11+-blue.svg)](https://www.python.org/)
[![LangChain](https://img.shields.io/badge/LangChain-0.3.50+-green.svg)](https://python.langchain.com/)
[![LangGraph](https://img.shields.io/badge/LangGraph-0.3.24+-orange.svg)](https://github.com/langchain-ai/langgraph)
[![Ollama](https://img.shields.io/badge/Ollama-latest-red.svg)](https://ollama.ai/)
[![Qwen](https://img.shields.io/badge/Qwen2.5-7B-purple.svg)](https://huggingface.co/Qwen)
[![OpenEvals](https://img.shields.io/badge/OpenEvals-0.0.17+-lightgrey.svg)](https://github.com/langchain-ai/openevals)

## Overview

This project implements a corrective local RAG (Retrieval Augmented Generation) system that uses the Qwen language model through Ollama. The system incorporates self-reflection and correction mechanisms to improve response quality, making it more robust and accurate than traditional RAG approaches.

The implementation leverages LangGraph for orchestrating the workflow of the agent, which includes search query generation, relevance evaluation, and response refinement through self-reflection.

## Features

- **Self-Correcting RAG**: Agent reflects on its responses and corrects itself when needed
- **Relevance Filtering**: Automatically filters search results based on relevance to the query
- **Helpfulness Evaluation**: Evaluates responses to ensure they are helpful to the user's original question
- **Multiple Agent Types**: Includes different agent implementations (corrective, reflection-only, and simple REACT)
- **Local Execution**: Runs on local models via Ollama for privacy and reduced latency

## Architecture

The project consists of three main agent implementations:

1. **Corrective RAG Agent**: The main implementation that includes both relevance filtering and response reflection
2. **Reflection-Only Agent**: Focuses on self-reflection without relevance filtering
3. **Simple REACT Agent**: A baseline implementation for comparison

The agents are implemented as LangGraph workflows, with nodes for:
- Search query generation
- Web search execution
- Relevance filtering
- Response generation
- Self-reflection and correction

## Prerequisites

- Python 3.11+
- Ollama with Qwen2.5:7b model installed
- Tavily API key (for web search)

## Installation

1. Clone the repository
```bash
git clone https://github.com/pakagronglb/langchain-corrective-local-rag-qwen.git
cd langchain-corrective-local-rag-qwen
```

2. Set up a virtual environment
```bash
python -m venv .venv
source .venv/bin/activate  # On Windows, use `.venv\Scripts\activate`
```

3. Install dependencies
```bash
pip install -e .
```

4. Create a `.env` file with your API keys
```
TAVILY_API_KEY=your_tavily_api_key
```

## Usage

You can run the agents using the LangGraph CLI:

```bash
langgraph serve
```

Then access the web UI at http://localhost:8000

Alternatively, you can use the agents programmatically:

```python
from openevals_local_rag.corrective_rag_agent import agent

result = agent.invoke({
    "messages": [
        {"role": "user", "content": "What is the latest news about AI regulation?"}
    ]
})
```

## Development

To run in development mode with auto-reloading:

```bash
langgraph serve --dev
```

## Credits

This project is based on techniques presented by [LangChain](https://www.youtube.com/watch?v=huEiXXQrlsg&ab_channel=LangChain) and incorporates the following key technologies:

- [LangChain](https://python.langchain.com/) - Framework for building LLM-powered applications
- [LangGraph](https://github.com/langchain-ai/langgraph) - DAG orchestration for LLM workflows
- [Ollama](https://ollama.ai/) - Local LLM serving platform
- [Qwen](https://huggingface.co/Qwen) - Qwen language models
- [OpenEvals](https://github.com/langchain-ai/openevals) - Evaluation framework for LLM applications

## License

MIT
