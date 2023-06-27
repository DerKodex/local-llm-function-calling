# Local LLM function calling

## Overview

The `local-llm-function-calling` project is designed to constrain the generation of Hugging Face text generation models by enforcing a JSON schema and facilitating the formulation of prompts for function calls, similar to OpenAI's [function calling](https://openai.com/blog/function-calling-and-other-api-updates) feature, but actually enforcing the schema unlike OpenAI.

The project provides a `Generator` class that allows users to easily generate text while ensuring compliance with the provided prompt and JSON schema. By utilizing the `local-llm-function-calling` library, users can conveniently control the output of text generation models. It uses my own quickly sketched `json-schema-enforcer` project as the enforcer.

## Features

- Constrains the generation of Hugging Face text generation models to follow a JSON schema.
- Provides a mechanism for formulating prompts for function calls, enabling precise data extraction and formatting.
- Simplifies the text generation process through a user-friendly `Generator` class.

## Installation

To install the `local-llm-function-calling` library, use the following command:

```shell
pip install local-llm-function-calling
```

## Usage

Here's a simple example demonstrating how to use `local-llm-function-calling`:

```python
from local_llm_function_calling import Generator

# Define a function and models
functions = [
    {
        "name": "get_current_weather",
        "description": "Get the current weather in a given location",
        "parameters": {
            "type": "object",
            "properties": {
                "location": {
                    "type": "string",
                    "description": "The city and state, e.g. San Francisco, CA",
                },
                "unit": {"type": "string", "enum": ["celsius", "fahrenheit"]},
            },
            "required": ["location"],
        },
    }
]

# Initialize the generator with the Hugging Face model, tokenizer, and functions
generator = Generator(functions, "gpt2")

# Generate text using a prompt
function_call = generator.generate("What is the weather like today in Brooklyn?")
print(function_call)

```

## Extending and Customizing

To extend or customize the prompt structure, you can subclass the `TextPrompter` class. This allows you to modify the prompt generation process according to your specific requirements.
