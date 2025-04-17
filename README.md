# MCP-Server-Development-Workshop

# Prerequisites Setup Guide
## 1. Install Claude Desktop Client
 - **Windows/Mac**: [Download from claude.ai](https://claude.ai/download)
 - **Debian Linux:** [GitHub - claude-desktop-debian](https://github.com/aaddrick/claude-desktop-debian)
  
## 2. Install Python 3.10+
 - Required for both Windows & Linux/Mac.

## 3. Install `uv` (Universal Virtualenv)

 - **Linux/Mac:** `curl -LsSf <https://astral.sh/uv/install.sh> | sh`
 - **Windows:** `irm https://astral.sh/uv/install.ps1 | iex`

## 4. Setup Test Project

 - **Linux/Mac:**
```bash
# Create project directory
uv init test
cd test

# Create & activate virtual environment
uv venv
source .venv/bin/activate

# Install dependencies
uv add fastmcp httpx

# Create server file
touch test.py
```

 - **Windows:**
```bash
# Create project directory
uv init test
cd test

# Create & activate virtual environment
uv venv
.\.venv\Scripts\activate

# Install dependencies
uv add fastmcp httpx

# Create server file
New-Item test.py
```

## 5. Write the Echo Server Code

- Add following into test.py file:
```python

from fastmcp import FastMCP

mcp = FastMCP("Echo Server")

@mcp.tool()
def echo(text: str) → str:
    """Echo the input text"""
    return text

if __name__ == "__main__":
    mcp.run()
```

## 6. Modify Claude Configuration
- Linux:
```bash
nano ~/.config/Claude/claude_desktop_config.json
```
- Windows:
```bash
notepad "$env:AppData\Claude\claude_desktop_config.json"
```

## 7. Add MCP Server Config

- Linux/Mac:
```json
{
    "mcpServers": {
        "test": {
            "command": "/ABSOLUTE/PATH/TO/uv",
            "args": [
                "--directory",
                "/ABSOLUTE/PATH/TO/test",
                "run",
                "test.py"
            ]
        }
    }
}
```

- Windows:
```json
{
    "mcpServers": {
        "test": {
            "command": "uv",
            "args": [
                "--directory",
                "C:\\PATH\\TO\\test",
                "run",
                "test.py"
            ]
        }
    }
}
```

## 8. Start Claude & Verify
 - Launch Claude Desktop.
 - No errors? You're ready!
 - Errors? Read the claude logs 
