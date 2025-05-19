# qq: Simple Bash CLI for OpenAI Chat Completions

qq is a minimal Bash script that lets you interact with OpenAI-compatible chat models from the command line. It supports both single-message and system-prompted conversations, and can read input from stdin for flexible scripting.

## Features
- Send prompts and messages to OpenAI's chat/completions API (or compatible endpoints)
- Supports system prompts and user messages
- Reads message from stdin if last argument is `-`
- Loads API keys and settings from `.env` or `~/.config/qq-env`
- Minimal dependencies: only `curl` and `jq`

## Usage

```bash
qq <prompt> <message>
qq <message>
qq <prompt> -    # message from stdin
```

- If only one argument is given, it is treated as the user message with a default system prompt.
- If two or more arguments are given, the first is the system prompt, the rest are joined as the user message.
- If the last argument is `-`, the message is read from stdin.

## Environment Variables
qq uses the following environment variables (set in `.env` or `~/.config/qq-env`):
- `LLM_API_KEY` (required): Your OpenAI API key
- `LLM_BASE_URL` (optional): API endpoint (default: `https://api.openai.com/v1/chat/completions`)
- `LLM_MODEL` (optional): Model name (default: `openai/gpt-4o-mini`)
- `LLM_TEMPERATURE` (optional): Sampling temperature (default: `0.1`)

## Example

```bash
echo "Summarize this text:" | qq "You are a helpful assistant." -
qq "You are a helpful assistant." "What is the capital of France?"
qq "What is the capital of France?"
qq "You are a helpful assistant." - < message.txt
qq "$(cat prompt.txt)" "$(cat message.txt)"
qq "$(cat prompt.txt)" - < message.txt
```

## Requirements
- bash
- curl
- jq

## Installation
Just copy the `qq` script somewhere in your `$PATH` and make it executable:

```bash
chmod +x qq
```

## License
MIT
