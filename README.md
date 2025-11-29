# google-search-mcp

A Model Context Protocol (MCP) server that utilizes Google Custom Search (CSE) to retrieve information from the internet. By leveraging this MCP, the Large Language Model (LLM) is enabled to perform real-time Web searches.

## Prerequisites

A Google Custom Search API key and Custom Search Engine ID are required:

1. Get a Google API Key from the [Google Cloud Console](https://console.cloud.google.com/)
2. Create a Custom Search Engine at [Programmable Search Engine](https://programmablesearchengine.google.com/)

## Installation

```bash
pip install google-search-mcp
```

Or install from source:

```bash
pip install .
```

## Configuration

Set the following environment variables:

```bash
export GOOGLE_API_KEY="your-api-key"
export GOOGLE_CSE_ID="your-custom-search-engine-id"
```

## Usage

### As a CLI

```bash
google-search-mcp
```

### With Claude Desktop

Add the following to your Claude Desktop configuration file:

**macOS**: `~/Library/Application Support/Claude/claude_desktop_config.json`
**Windows**: `%APPDATA%\Claude\claude_desktop_config.json`

```json
{
  "mcpServers": {
    "google-search": {
      "command": "google-search-mcp",
      "env": {
        "GOOGLE_API_KEY": "your-api-key",
        "GOOGLE_CSE_ID": "your-custom-search-engine-id"
      }
    }
  }
}
```

## Tools

### search

Search the web using Google Custom Search.

**Parameters:**
- `query` (string, required): The search query string
- `num_results` (integer, optional): Number of results to return (1-10, default 10)

## License

MIT License - see [LICENSE](LICENSE) for details.
