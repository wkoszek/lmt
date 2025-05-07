# LMT (Language Model Tool CLI)

LMT is a command-line tool allowing you to call popular LLMs from command line.
It's meant to be 1 Python script that you can copy around to get the AI
capability anywhere.
Right now supported are language models from OpenAI, Anthropic, Google, and Grok XAI. 
It also has a friendly mode of recording input/output from the models, so
every interaction with AI is recorded to a separate file that you can 
check-in to Git or investigate, copy the outputs from etc.

## Features

- Support for multiple LLM providers:
  - OpenAI (GPT models)
  - Anthropic (Claude models)
  - Google (Gemini models)
  - Grok XAI (Grok models, via OpenAI-compatible API)
- Explicit provider selection
- YAML logging of all interactions with timestamps
- Simple stdin/stdout interface
- Error handling and user-friendly messages
- Symlink support for quick access to specific models

## Prerequisites

- Python 3.7 or higher
- Required API keys:
  - OpenAI API key (set as `OPENAI_API_KEY` environment variable)
  - Anthropic API key (set as `ANTHROPIC_API_KEY` environment variable)
  - Google API key (set as `GOOGLE_API_KEY` environment variable)
  - Grok XAI API key (set as `GROK_API_KEY` environment variable)

## Installation

1. Clone this repository or download the `lmt` script
2. Make the script executable:
   ```bash
   chmod +x lmt
   ```
3. Install required Python packages:
   ```bash
   pip install openai anthropic google-generativeai
   ```
4. Set up your API keys in your environment:
   ```bash
   export OPENAI_API_KEY='your-openai-key'
   export ANTHROPIC_API_KEY='your-anthropic-key'
   export GOOGLE_API_KEY='your-google-key'
   export GROK_API_KEY='your-grok-key'
   ```

## Usage

The basic syntax is:
```bash
echo "Your prompt here" | ./lmt <provider> <model-name>
```

Where:
- `<provider>` is one of: `openai`, `anthropic`, `google`, `xai`
- `<model-name>` is the specific model to use

### Examples

```bash
# OpenAI GPT-4
echo "What is the capital of France?" | ./lmt openai gpt-4

# Anthropic Claude
echo "Write a Python function to calculate fibonacci numbers" | ./lmt anthropic claude-3-opus-20240229

# Google Gemini
echo "Explain quantum computing in simple terms" | ./lmt google gemini-pro

# Grok XAI
echo "What are the latest developments in AI?" | ./lmt xai grok-1
```

### Symlink Usage

You can create symlinks to quickly access specific models. The symlink name should follow the pattern `lmt-<provider>-<model>`:

```bash
# Create symlinks for different models
ln -s lmt lmt-openai-gpt4
ln -s lmt lmt-anthropic-claude3
ln -s lmt lmt-google-gemini
ln -s lmt lmt-xai-grok1

# Use the symlinks directly
echo "What is the capital of France?" | ./lmt-openai-gpt4
echo "Write a Python function" | ./lmt-anthropic-claude3
echo "Explain quantum computing" | ./lmt-google-gemini
echo "What's new in AI?" | ./lmt-xai-grok1
```

### Supported Providers and Models

- OpenAI: `gpt-4`, `gpt-3.5-turbo`, etc.
- Anthropic: `claude-3-opus-20240229`, `claude-3-sonnet-20240229`, etc.
- Google: `gemini-pro`, `gemini-pro-vision`, etc.
- Grok: `grok-1`, etc. (via OpenAI-compatible API at api.x.ai)

## Output

The tool outputs the model's response to stdout and creates a YAML log file with the format `YYYYMMDD-HHMMSS-ffffff-provider-model.yaml` containing:
- Input prompt
- Output response
- Timestamps for request and response
- Provider and model used

Example log file format:
```yaml
sent:
  time_sent_at: 1709123456.789
  prompt: |
    What is the capital of France?
    Please provide a brief explanation.
  provider: openai
  model: gpt-4
received:
  time_recv_at: 1709123457.123
  output: |
    The capital of France is Paris.
    
    Paris has been France's capital since 987 CE. It is the country's largest city
    and serves as its political, economic, and cultural center. The city is known
    for iconic landmarks like the Eiffel Tower, the Louvre Museum, and the
    Notre-Dame Cathedral.
  provider: openai
  model: gpt-4
```

## Copyright

Copyright (c) 2024 Adam W. Koszek <adam@koszek.com>
