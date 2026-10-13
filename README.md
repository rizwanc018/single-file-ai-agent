# single-file-ai-agent

A minimal conversational coding agent in a single Python file. It runs in the terminal, talks to Claude through the Anthropic API, and can read, list, and edit files in your working directory using tool calls.

## Features

- Interactive chat loop in the terminal
- Agentic tool-use loop: Claude can call tools repeatedly until it has an answer
- Three built-in tools:
  - `read_file` – read a file's contents
  - `list_files` – list files and directories at a path
  - `edit_file` – replace text in a file, or create a new file
- Logs user input, tool calls, and tool results to `agent.log`

## Requirements

- Python 3.12+
- [uv](https://docs.astral.sh/uv/)
- An Anthropic API key

## Usage

```bash
export ANTHROPIC_API_KEY=your-key-here
uv run src/single_file_ai_agent/main.py
```

Or pass the key as an argument:

```bash
uv run src/single_file_ai_agent/main.py --api-key your-key-here
```

Type a message at the `You:` prompt. Type `exit` or `quit` (or press Ctrl+C) to end the session.

### Example

```
You: list the files in this directory
Assistant: Here are the files in the current directory: ...

You: create hello.py that prints hello world
Assistant: Created hello.py ...
```

## How it works

1. Your message is appended to the conversation history.
2. The history and the tool definitions are sent to Claude.
3. If Claude responds with tool calls, each tool is executed locally and the results are sent back.
4. Steps 2–3 repeat until Claude replies with plain text, which is printed to the terminal.
