# Tool Calling Grammar for Constrained LLM Generation with Itergen

## Task Overview
Create an LR grammar that describes tool calls in a commonly used syntax, and use it with Itergen to constrain the outputs of an LLM. This task demonstrates how formal grammars can be used to semantically constrain the output from LLMs.

## Timeframe
Two weeks

## Requirements
- Lark parser (`pip install lark-parser`)
- Itergen library (https://github.com/structuredllm/itergen)
- Python 3.11+

## Tasks

### 1. Write a grammar for tool calls
Create a Lark LALR(1) grammar that describes a tool call in the JSON format (e.g., `{"name": "tool_name", "args": {"arg1": "value1", "arg2": 42}}`). Note that the tool names could be any string, and the arguments can be of different types (string, integer, float, boolean, list, dictionary).

### 2. Use Itergen to constrain LLM outputs
Use the above grammar with Itergen to constrain the outputs of an LLM (use a small Qwen3 model for testing). The LLM outputs should conform to the defined grammar. Use the scenarios and list of tools in tools.txt for testing. Ensure that the generated tool name is drawn from the provided tool definitions.
After a tool call is generated, check its signature (types of arguments) against the tool definition in tools.txt. If the generated tool call does not follow the signature, backtrack and generate a new tool call (using the `backward`, `forward` calls in Itergen).
Note that the tool call is not actually executed; only its generation and signature checking are required.
Use reasonable defaults for hyperparameters like temperature, number of retries, etc. If you wish, you can try different hyperparameter settings and pick the best-performing one.

### (Bonus) Incremental checking
Instead of waiting for the full tool call to be generated before checking its signature, check the type of each argument as it is generated. If an argument does not match the expected type, backtrack immediately and generate a new argument value.

## Deliverables
- Link to a video containing a demonstration of the working code
- By email, or uploading to a GitHub repository, provide the following files:
    - `tool_call.lark` - Lark grammar file for tool calls
    - `main.py` - Python script that uses Itergen to constrain LLM outputs based on the grammar

## References
- Lark documentation: https://lark-parser.readthedocs.io/en/latest/
- Itergen GitHub repository: https://github.com/structuredllm/itergen
- Itergen paper: https://arxiv.org/abs/2410.07295
