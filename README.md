# LangGraph Learning

Practical, notebook-based examples for learning how to build stateful LLM workflows and multi-agent systems with [LangGraph](https://langchain-ai.github.io/langgraph/) and [LangChain](https://python.langchain.com/).

The examples use Google Gemini through LangChain's model integration and focus on the control-flow patterns that make agentic applications reliable, inspectable, and easier to extend.

## What You Will Learn

- Model workflows as explicit graphs with typed state.
- Chain multiple LLM calls into a controlled sequence.
- Route requests to specialized graph nodes using structured output.
- Run independent tasks in parallel and aggregate their results.
- Add evaluator and feedback loops that improve generated content.
- Coordinate specialized agents through a supervisor node.
- Inspect and visualize compiled LangGraph workflows.

## Repository Layout

```text
.
├── pyproject.toml
├── requirements.txt
├── uv.lock
└── src/
	├── langgraph_learning/
	│   └── multi_agent.ipynb
	└── wrokFlows/
		├── Prompt_chaining.ipynb
		├── Routing_workflow.ipynb
		├── parallelization.ipynb
		└── evalutor.ipynb
```

> The `wrokFlows` directory name is kept as it exists in the repository.

## Prerequisites

- Python 3.12 or newer
- A Google AI API key with access to Gemini models
- Either [uv](https://docs.astral.sh/uv/) or `pip`

## Setup

### Option 1: uv

From the repository root:

```bash
uv sync
source .venv/bin/activate
```

On Windows PowerShell, activate the environment with:

```powershell
.venv\Scripts\Activate.ps1
```

### Option 2: pip

```bash
python -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

## Configure Environment Variables

Create a `.env` file in the repository root:

```dotenv
GOOGLE_API_KEY=your_google_ai_api_key
```

The notebooks load environment variables with `python-dotenv`. Never commit `.env` or expose your API key in notebook output.

## Run the Notebooks

Start Jupyter from the repository root:

```bash
uv run jupyter lab
```

If you installed with `pip`, use:

```bash
jupyter lab
```

Open a notebook, select the repository's Python environment as the kernel, and run the cells from top to bottom. Each notebook is self-contained and includes graph construction, compilation, execution, and, where applicable, graph visualization.

## Learning Path

| Notebook | Main idea | Example workflow |
| --- | --- | --- |
| [`Prompt_chaining.ipynb`](src/wrokFlows/Prompt_chaining.ipynb) | Sequential calls and conditional transitions | Generate, improve, and polish a joke |
| [`Routing_workflow.ipynb`](src/wrokFlows/Routing_workflow.ipynb) | Structured-output routing | Route an input to a poem, story, or joke node |
| [`parallelization.ipynb`](src/wrokFlows/parallelization.ipynb) | Concurrent branches and aggregation | Generate a joke, story, and poem in parallel |
| [`evalutor.ipynb`](src/wrokFlows/evalutor.ipynb) | Evaluation and feedback loops | Generate a joke, evaluate it, and revise it |
| [`multi_agent.ipynb`](src/langgraph_learning/multi_agent.ipynb) | Supervisor-based multi-agent orchestration | Delegate calculation and explanation to specialized agents |

## Core Concepts Used

The examples repeatedly use a small set of LangGraph primitives:

- `StateGraph` defines a workflow around shared, typed state.
- `START` and `END` define the graph's entry and exit points.
- Nodes are Python functions that read state and return updates.
- Edges describe fixed transitions between nodes.
- Conditional edges select the next node from the current state or model decision.
- Structured output constrains model decisions to an expected schema.
- Compiled graphs can be invoked directly or streamed to inspect intermediate updates.

## Development Notes

This repository is intended for experimentation and learning rather than production deployment. Model responses are non-deterministic and require a valid API key, so notebook output may differ between runs.

The notebooks currently target rapidly evolving LangChain and LangGraph APIs. In particular, the saved `multi_agent.ipynb` output reports that `create_react_agent` has moved to `langchain.agents` in LangGraph v1. If you see deprecation warnings after upgrading dependencies, follow the migration guidance for the installed versions and update the notebook imports and agent construction accordingly.

## License

No license file is currently included in this repository.
