# hello-mcp

A minimal hello-world MCP server for MCPLambda integration testing.

## Overview

This repository contains a simple MCP (Model Context Protocol) server built with FastMCP, designed as a test fixture for MCPLambda. It demonstrates the basic structure of an MCP server with tools, resources, and prompts.

## Files

| File | Purpose |
|------|---------|
| `server.py` | FastMCP server with `echo_tool` tool, static/dynamic resources, and prompts |
| `mcplambda.yaml` | MCPLambda deployment config — `run: "python server.py"` |
| `requirements.txt` | Python dependencies (`fastmcp>=2.0.0`) |

## MCP Components

### Tools
- `echo_tool(text: str)` — Echoes the input text back

### Resources
- `echo://static` — Static resource returning "Echo!"
- `echo://{text}` — Template resource that echoes dynamic text

### Prompts
- `echo` — Simple prompt that echoes text

## Deployment

MCPLambda auto-detects the build strategy:
1. No `Dockerfile` → skip
2. No `uv.lock` / `poetry.lock` → skip
3. `requirements.txt` found → **strategy: `pip`**

The server runs on port 8080 (configurable via `PORT` env var).

## Testing Other Strategies

To test other build strategies, create variants:
- **uv**: Add `uv.lock` + `pyproject.toml` with `[tool.uv]`
- **poetry**: Add `poetry.lock` + `pyproject.toml` with `[tool.poetry]`
- **npm**: Replace `requirements.txt` with `package.json` + `index.js`
- **go**: Replace with `go.mod` + `main.go`
