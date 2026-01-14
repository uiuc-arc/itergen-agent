# Tool Calling Grammar for Constrained LLM Generation with Itergen

## Task Overview
Create an LR grammar that describes tool calls in JSON syntax, and use it with Itergen to constrain the outputs of an LLM. This task demonstrates how formal grammars can be used to constrain the output from LLMs semantically.

## Timeframe
Two weeks

## Requirements
- Itergen library (https://github.com/structuredllm/itergen)
- Python 3.11+

## Tasks

### 1. Write a grammar for tool calls
Create a Lark LALR(1) grammar that describes a tool call in the JSON format (e.g., `{"name": "tool_name", "args": {"arg1": "value1", "arg2": 42}}`). Note that the tool names could be any string, and the arguments can be of different types (string, integer, float, boolean, list, dictionary).

### 2. Use Itergen to constrain LLM outputs
Use the above grammar with Itergen to constrain the outputs of an LLM (use a small Qwen3 model for testing). The LLM outputs should conform to the defined grammar. Use the scenarios and list of tools in tools.txt for testing. Ensure that the generated tool name is valid (a tool name is valid if it is present in the provided tool definitions).
After a tool call is generated, check its signature (types of the arguments) against the tool definition in tools.txt. If the generated tool call does not obey the signature, backtrack and generate a new tool call (use the `backward`, `forward` calls in Itergen).
Note that the tool call is not actually executed; only its generation and signature checking are required.
Use reasonable defaults for hyperparameters like temperature, number of retries, etc. If you wish, you can try different hyperparameter settings and pick the best-performing one.

### (Bonus) Incremental checking
Instead of waiting for the full tool call to be generated before checking its signature, check the type of each argument as it is generated. If an argument does not match the expected type, backtrack immediately and generate a new argument value.

## Tips

- Use Lark parser (`pip install lark-parser`) to debug the grammar you write for JSON. You can also use the Lark online IDE (https://www.lark-parser.org/ide/) to debug your grammar if you encounter any issues with it.
- Refer to the Itergen documentation and the example in README.md for guidance on how to use it effectively. You might find example grammars in the SynCode repository (https://github.com/structuredllm/syncode) useful as references.

## Deliverables
- Link to a video containing a demonstration of the working code
- Link to a GitHub repository, with the following files:
    - `tool_call.lark` - Lark grammar file for tool calls
    - `main.py` - Python script that uses Itergen to constrain LLM outputs based on the grammar

## References
- Lark documentation: https://lark-parser.readthedocs.io/en/latest/
- Itergen GitHub repository: https://github.com/structuredllm/itergen
- Itergen paper: https://arxiv.org/abs/2410.07295
