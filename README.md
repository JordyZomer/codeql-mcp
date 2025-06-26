# CodeQL MCP Server

This project runs a Model Context Protocol (MCP) server that wraps the CodeQL query server. It enables tools like [Cursor](https://cursor.sh/) or AI agents to interact with CodeQL through structured commands and doc search.

---

##  Features

- ✅ Register CodeQL databases  
- ✅ Run full queries or quick-evaluate a symbol  
- ✅ Decode `.bqrs` files into JSON  
- ✅ Locate predicate/class symbol positions  

---

##  File Structure

| File              | Purpose                                             |
|-------------------|-----------------------------------------------------|
| `server.py`       | Main FastMCP server exposing CodeQL tools           |
| `codeqlclient.py` | CodeQLQueryServer implementation (JSON-RPC handler) |

---

##  Requirements

Install with [`uv`](https://github.com/astral-sh/uv):

```bash
uv pip install -r requirements.txt
```

or with `pip`:
```bash
pip install fastmcp httpx
```

## Running the MCP Server
```bash
uv run mcp run server.py -t sse
```
- Starts the server at http://localhost:8000/sse
- Required for Cursor or AI agent use

## Cursor Config
Make sure your `.cursor/config.json` contains:
```
{
  "mcpServers": {
    "CodeQL": {
      "url": "http://localhost:8000/sse"
    }
  }
}
```

## Notes
- Tools like Cursor will invoke these commands directly via natural language.
- You must have a codeql binary in your $PATH, or hardcode its path in codeqlclient.py.
- You should probably specify query locations, query write locations and database paths in your prompts.

