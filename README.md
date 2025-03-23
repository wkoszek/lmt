# LMT (Language Model Tool)

A unified command-line interface for interacting with various language models from OpenAI, Anthropic, and Google. 
This tool provides a simple way to send prompts to different LLM providers and automatically logs all interactions.

## Features

- Support for multiple LLM providers:
  - OpenAI (GPT models)
  - Anthropic (Claude models)
  - Google (Gemini models)
- Automatic model detection based on model name
- JSON logging of all interactions with timestamps
- Simple stdin/stdout interface
- Error handling and user-friendly messages

## Prerequisites

- Python 3.7 or higher
- Required API keys:
  - OpenAI API key (set as `OPENAI_API_KEY` environment variable)
  - Anthropic API key (set as `ANTHROPIC_API_KEY` environment variable)
  - Google API key (set as `GOOGLE_API_KEY` environment variable)

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
   ```

## Usage

The basic syntax is:
```bash
echo "Your prompt here" | ./lmt <model-name>
```

### Examples

1. Using OpenAI's GPT-4:
```bash
echo "What is the capital of France?" | ./lmt gpt-4
```

2. Using Anthropic's Claude:
```bash
echo "Write a Python function to calculate fibonacci numbers" | ./lmt claude-3-opus-20240229
```

3. Using Google's Gemini:
```bash
echo "Explain quantum computing in simple terms" | ./lmt gemini-pro
```

### Supported Model Names

- OpenAI: `gpt-4`, `gpt-3.5-turbo`, etc.
- Anthropic: `claude-3-opus-20240229`, `claude-3-sonnet-20240229`, etc.
- Google: `gemini-pro`, `gemini-pro-vision`, etc.

## Output

The tool outputs the model's response to stdout and creates a JSON log file with the format `YYYYMMDD-HHMMSS-model.json` containing:
- Input prompt
- Output response
- Timestamps for request and response
- Model used


## Copyright

Copyright (c) 2024 Adam W. Koszek <adam@koszek.com>
