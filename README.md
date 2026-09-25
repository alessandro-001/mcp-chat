# MCP Chat

MCP Chat is a command-line interface application that enables interactive chat capabilities with AI models through the Anthropic API. The application supports document retrieval, command-based prompts, and extensible tool integrations via the MCP (Model Control Protocol) architecture.

## About this repository

This is my completed project from Anthropic's **Introduction to Model Context Protocol** course. The course provides the CLI chat scaffolding (`main.py`, `core/`); the MCP parts were left as TODOs, which I implemented:

- **MCP server** ([mcp_server.py](mcp_server.py)), built with `FastMCP`:
  - Tools: `read_doc_contents` and `edit_document`
  - Resources: `docs://documents` (list of document ids) and `docs://documents/{doc_id}` (document contents)
  - Prompt: `format`, which rewrites a document in Markdown
- **MCP client** ([mcp_client.py](mcp_client.py)): `list_tools`, `call_tool`, `list_prompts`, `get_prompt` and `read_resource`

Not done: the optional `summarize` prompt is still a TODO in `mcp_server.py`.

## Prerequisites

- Python 3.9+
- Anthropic API Key

## Setup

### Step 1: Configure the environment variables

1. Create or edit the `.env` file in the project root and verify that the following variables are set correctly:

```
ANTHROPIC_API_KEY=""  # Enter your Anthropic API secret key
CLAUDE_MODEL="claude-sonnet-4-5"
USE_UV=1  # 1 if you run the project with uv, 0 if not
```

`.env` is git-ignored, so create your own; never commit your API key.

### Step 2: Install dependencies

#### Option 1: Setup with uv (Recommended)

[uv](https://github.com/astral-sh/uv) is a fast Python package installer and resolver.

1. Install uv, if not already installed:

```bash
pip install uv
```

2. Create and activate a virtual environment:

```bash
uv venv
source .venv/bin/activate  # On Windows: .venv\Scripts\activate
```

3. Install dependencies:

```bash
uv pip install -e .
```

4. Run the project

```bash
uv run main.py
```

#### Option 2: Setup without uv

1. Create and activate a virtual environment:

```bash
python -m venv .venv
source .venv/bin/activate  # On Windows: .venv\Scripts\activate
```

2. Install dependencies:

```bash
pip install anthropic python-dotenv prompt-toolkit "mcp[cli]==1.8.0"
```

3. Run the project

```bash
python main.py
```

## Usage

### Basic Interaction

Simply type your message and press Enter to chat with the model.

### Document Retrieval

Use the @ symbol followed by a document ID to include document content in your query:

```
> Tell me about @deposition.md
```

### Commands

Use the / prefix to execute commands defined in the MCP server:

```
> /format deposition.md
```

Commands will auto-complete when you press Tab.

## Development

### Adding New Documents

Edit the `mcp_server.py` file to add new documents to the `docs` dictionary.

### Linting and Typing Check

There are no lint or type checks implemented.
