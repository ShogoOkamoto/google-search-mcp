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

Create a `.env` file in the project root directory:

```bash
cp .env.example .env
```

Then edit the `.env` file and add your credentials:

```env
GOOGLE_API_KEY=your-api-key
GOOGLE_CSE_ID=your-custom-search-engine-id
```

Alternatively, you can set environment variables directly:

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

**For macOS/Linux:**

```json
{
  "mcpServers": {
    "google-search": {
      "command": "python",
      "args": ["-m", "google_search_mcp"],
      "env": {
        "GOOGLE_API_KEY": "your-api-key",
        "GOOGLE_CSE_ID": "your-custom-search-engine-id"
      }
    }
  }
}
```

**For Windows:**

If `python` is in your PATH (check with `where python`), you can use the same configuration as macOS/Linux:

```json
{
  "mcpServers": {
    "google-search": {
      "command": "python",
      "args": ["-m", "google_search_mcp"],
      "env": {
        "GOOGLE_API_KEY": "your-api-key",
        "GOOGLE_CSE_ID": "your-custom-search-engine-id"
      }
    }
  }
}
```

If you need to use a specific Python installation, find the full path with:
```bash
python -c "import sys; print(sys.executable)"
```

Then use the full path in the configuration:
```json
{
  "mcpServers": {
    "google-search": {
      "command": "C:\\Users\\YOUR_USERNAME\\AppData\\Local\\Microsoft\\WindowsApps\\PythonSoftwareFoundation.Python.3.13_qbz5n2kfra8p0\\python.exe",
      "args": ["-m", "google_search_mcp"],
      "env": {
        "GOOGLE_API_KEY": "your-api-key",
        "GOOGLE_CSE_ID": "your-custom-search-engine-id"
      }
    }
  }
}
```

**Note:** Environment variables must be set in the Claude Desktop config `env` section for the server to access them.

## Tools

### search

Search the web using Google Custom Search.

**Parameters:**
- `query` (string, required): The search query string
- `num_results` (integer, optional): Number of results to return (1-10, default 10)

## Development

### Running Tests

Install development dependencies:

```bash
pip install -e ".[dev]"
```

Run the test suite:

```bash
pytest
```

Run tests with verbose output:

```bash
pytest -v
```

Run tests with coverage:

```bash
pytest --cov=google_search_mcp --cov-report=html
```

### Test Coverage

The test suite includes comprehensive tests for:
- Successful search requests
- Environment variable validation
- API error handling
- JSON parsing errors
- Empty search results
- Input parameter validation (num_results clamping)
- Result formatting
- Request parameter verification

## License

MIT License - see [LICENSE](LICENSE) for details.
