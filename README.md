
# How to create an MCP server for LM Studio with FastMCP

> Starting from [version 0.3.17 (b10)](https://lmstudio.ai/blog/lmstudio-v0.3.17), LM Studio supports both local and remote [MCP (Model Context Protocol servers)](https://modelcontextprotocol.io/introduction). This repository is a simple guide to create an MCP server in Python using the [FastMCP library](https://pypi.org/project/fastmcp/).

## Prerequisites
To get started, ensure you have the following prerequisites:

- **Python**: Install the latest version from [python.org](https://www.python.org/downloads/).
- **LM Studio**: Download and install LM Studio from [lmstudio.ai/download](https://lmstudio.ai/download).
- **FastMCP library**: Open a terminal and run:
    ```bash
    pip install fastmcp
    ```
- **Optional**: A code editor such as [VS Code](https://code.visualstudio.com/) for editing your Python scripts.

## 1. Write your MCP server logic

Create a Python file and implement your MCP server using FastMCP. Here is a minimal example:

```python
from fastmcp import FastMCP

mcp = FastMCP("Demo 🚀")

@mcp.tool
def add(a: int, b: int) -> int:
    """Add two numbers"""
    return a + b

if __name__ == "__main__":
    mcp.run()
```

This example registers an `add` method that takes two parameters and returns their sum. You can add more methods as needed.

➡️ **You can also copy the `server_math.py` file from this repository for a more complete example.**

## 2. Configure LM Studio to use your MCP server

In LM Studio, switch to the "Program" tab in the right-hand sidebar. Click `Install > Edit mcp.json`.

This will open the `mcp.json` file in the in-app editor. You can add MCP servers by editing this file.

## 3. Example of mcp.json configuration
Use the example below as a template. **Adapt the path in `"args"` to the actual location of your Python script!**


```json
{
  "mcpServers": {
    "Math": {
      "command": "python",
      "args": [
        "C:/Users/.../server_math.py"
      ]
    }
  }
}
```

## 4. Start and test your server

Once your `mcp.json` is configured, LM Studio will automatically launch your MCP server when needed. You can verify that your server is running by interacting with your tool from the LM Studio interface.

To manually test your server, open a terminal and run:
```bash
python server_math.py
```
This should start your MCP server and display its status.

## 5. Debugging and tips

- Double-check the Python executable path and script location in your `mcp.json` configuration.
- Ensure all required dependencies are installed (`fastmcp`, etc).
- For advanced usage, refer to the FastMCP documentation.

### Useful links :

- [FastMCP documentation](https://github.com/jlowin/fastmcp)
- [LM Studio documentation](https://lmstudio.ai/docs/app/plugins/mcp)
