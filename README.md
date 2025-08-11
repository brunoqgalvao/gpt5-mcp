# GPT-5 MCP Server

<div align="center">
  <img src="assets/images/gpt5-mcp-logo.png" alt="GPT-5 MCP Server Logo" width="300" />
</div>

A Model Context Protocol (MCP) server that provides seamless integration with OpenAI's GPT-5 API. Access the most advanced language model directly through your favorite AI development tools.

## Features

- **Direct GPT-5 Integration**: Access OpenAI's most advanced model through MCP
- **Dual Tool Support**:
  - `gpt5_generate`: Simple text generation with prompts
  - `gpt5_messages`: Structured conversation handling
- **Flexible Parameters**: Control temperature, max tokens, reasoning effort, and more
- **Usage Tracking**: Built-in token usage reporting
- **TypeScript**: Fully typed for better development experience

## Installation

### Prerequisites

- Node.js (v18 or higher)
- OpenAI API key with GPT-5 access

### Quick Start

**Option 1: Install from NPM (Recommended)**
```bash
npm install -g @dannyboy2042/gpt5-mcp-server
```

**Option 2: Build from Source**
```bash
git clone https://github.com/danielbowne/gpt5-mcp.git
cd gpt5-mcp/servers/gpt5-server
npm install
npm run build
```

Set your OpenAI API key:
```bash
export OPENAI_API_KEY=your-api-key-here
```

## Client Configuration

### Claude Desktop

Add to your `claude_desktop_config.json`:

**macOS**: `~/Library/Application Support/Claude/claude_desktop_config.json`
**Windows**: `%APPDATA%\Claude\claude_desktop_config.json`

```json
{
  "mcpServers": {
    "gpt5-server": {
      "command": "npx",
      "args": ["@dannyboy2042/gpt5-mcp-server"],
      "env": {
        "OPENAI_API_KEY": "your-api-key-here"
      }
    }
  }
}
```

<details>
<summary>Alternative: Using local build</summary>

```json
{
  "mcpServers": {
    "gpt5-server": {
      "command": "node",
      "args": ["/path/to/gpt5-mcp/servers/gpt5-server/build/index.js"],
      "env": {
        "OPENAI_API_KEY": "your-api-key-here"
      }
    }
  }
}
```
</details>

### Cursor

Add to your Cursor settings:

```json
{
  "mcpServers": {
    "gpt5-server": {
      "command": "npx",
      "args": ["@dannyboy2042/gpt5-mcp-server"],
      "env": {
        "OPENAI_API_KEY": "your-api-key-here"
      }
    }
  }
}
```

### Windsurf

Add to your Windsurf configuration file:

**macOS**: `~/Library/Application Support/Windsurf/config.json`
**Windows**: `%APPDATA%\Windsurf\config.json`

```json
{
  "mcpServers": {
    "gpt5-server": {
      "command": "npx",
      "args": ["@dannyboy2042/gpt5-mcp-server"],
      "env": {
        "OPENAI_API_KEY": "your-api-key-here"
      }
    }
  }
}
```

### Continue

Add to your Continue configuration:

```json
{
  "models": [
    {
      "model": "AUTODETECT",
      "provider": "mcp",
      "apiKey": "",
      "mcpServers": [
        {
          "command": "npx",
          "args": ["@dannyboy2042/gpt5-mcp-server"],
          "env": {
            "OPENAI_API_KEY": "your-api-key-here"
          }
        }
      ]
    }
  ]
}
```

### Claude Code

**Local Server Connection (Recommended)**
```bash
claude mcp add gpt5-server -- npx -y @dannyboy2042/gpt5-mcp-server
```

**With Environment Variable**
```bash
claude mcp add gpt5-server -e OPENAI_API_KEY=your-api-key-here -- npx -y @dannyboy2042/gpt5-mcp-server
```

**Legacy Method**
```bash
claude mcp add gpt5-server -e OPENAI_API_KEY=your-api-key-here -- npx @dannyboy2042/gpt5-mcp-server
```

### Generic MCP Client

For any MCP-compatible client, use:

```json
{
  "command": "npx",
  "args": ["@dannyboy2042/gpt5-mcp-server"],
  "env": {
    "OPENAI_API_KEY": "your-api-key-here"
  }
}
```

## Tools

### `gpt5_generate`

Generate text using a simple input prompt.

**Parameters:**
- `input` (required): The text prompt for GPT-5
- `model` (optional): GPT-5 model variant (default: "gpt-5")
- `instructions` (optional): System instructions for the model
- `reasoning_effort` (optional): Reasoning level ("low", "medium", "high")
- `max_tokens` (optional): Maximum tokens to generate
- `temperature` (optional): Randomness level (0-2)
- `top_p` (optional): Top-p sampling parameter (0-1)

**Example:**
```json
{
  "input": "Explain quantum computing in simple terms",
  "reasoning_effort": "high",
  "max_tokens": 500
}
```

### `gpt5_messages`

Generate text using structured conversation messages.

**Parameters:**
- `messages` (required): Array of conversation messages
  - `role`: "user", "developer", or "assistant"
  - `content`: Message text
- `model` (optional): GPT-5 model variant (default: "gpt-5")
- `instructions` (optional): System instructions
- `reasoning_effort` (optional): Reasoning level
- `max_tokens` (optional): Maximum tokens
- `temperature` (optional): Randomness (0-2)
- `top_p` (optional): Top-p sampling (0-1)

**Example:**
```json
{
  "messages": [
    {"role": "user", "content": "What is the capital of France?"},
    {"role": "assistant", "content": "The capital of France is Paris."},
    {"role": "user", "content": "What about Germany?"}
  ],
  "instructions": "Be concise and informative",
  "reasoning_effort": "medium"
}
```

## Usage Examples

### Simple Generation
```
Use GPT-5 to explain the theory of relativity
```

### Code Review
```
Ask GPT-5 to review this code and suggest improvements
```

### Creative Writing
```
Have GPT-5 write a short story about time travel
```

### Technical Analysis
```
Use GPT-5 with high reasoning to solve this complex algorithm problem
```

## Environment Variables

Create a `.env` file in the `servers` directory:

```bash
# Required
OPENAI_API_KEY=your-openai-api-key-here

# Optional (for development)
DEBUG=true
```

## Development

### Building from Source

```bash
# Install dependencies
npm install

# Build the server
npm run build

# Run in development mode
npm run dev
```

### Project Structure

```
gpt5-mcp/
├── servers/
│   └── gpt5-server/
│       ├── src/
│       │   ├── index.ts      # Main server
│       │   └── utils.ts      # API utilities
│       ├── build/            # Compiled output
│       ├── package.json
│       └── tsconfig.json
└── README.md
```

## Troubleshooting

### Server not responding
- Verify your OpenAI API key is valid
- Check that you have GPT-5 access on your account
- Ensure Node.js v18+ is installed

### Build errors
```bash
# Clean rebuild
rm -rf build/
npm install
npm run build
```

### API errors
- Check your API key has sufficient credits
- Verify GPT-5 model access
- Review rate limits on your OpenAI account

## Security

- API keys are never hardcoded
- Environment variables for sensitive data
- Secure HTTPS communication with OpenAI
- Error messages don't expose sensitive information

## Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

MIT License - see [LICENSE](LICENSE) file for details

## Acknowledgments

- Built with [Model Context Protocol](https://modelcontextprotocol.io)
- Powered by [OpenAI GPT-5](https://openai.com)
- TypeScript SDK by [@modelcontextprotocol](https://github.com/modelcontextprotocol)

## Support

- **Issues**: [GitHub Issues](https://github.com/danielbowne/gpt5-mcp/issues)
- **Discussions**: [GitHub Discussions](https://github.com/danielbowne/gpt5-mcp/discussions)

## Special Thanks

💡 **Inspired by**: [All About AI](https://www.youtube.com/@AllAboutAI) - Thanks for the awesome content that sparked this project!

---

> "The future is already here — it's just not evenly distributed." - William Gibson

⭐ **Star this repo if you find it useful!**