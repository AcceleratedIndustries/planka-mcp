# planka-mcp

A Model Context Protocol (MCP) server for [Planka](https://planka.app/) kanban boards, written in Rust.

## Installation

### From GitHub (recommended)

```bash
cargo install --git https://github.com/AcceleratedIndustries/planka-mcp
```

### From source

```bash
git clone https://github.com/AcceleratedIndustries/planka-mcp
cd planka-mcp
cargo build --release
```

## Setup

### Environment Variables

```bash
export PLANKA_URL="https://kanban.local"

# Option 1: Bearer token (preferred)
export PLANKA_TOKEN="your-token-here"

# Option 2: Email/password authentication
export PLANKA_EMAIL="admin@example.com"
export PLANKA_PASSWORD="your-password"
```

### Run

```bash
# If installed via cargo install:
planka-mcp

# If built from source:
./target/release/planka-mcp
```

## MCP Client Configuration

Add to your MCP client configuration:

```json
{
  "mcpServers": {
    "planka": {
      "command": "/path/to/planka-mcp",
      "env": {
        "PLANKA_URL": "https://kanban.local",
        "PLANKA_TOKEN": "your-token"
      }
    }
  }
}
```

## Available Tools

| Tool | Description |
|------|-------------|
| `list_projects` | List all Planka projects |
| `list_boards` | List boards in a project |
| `list_lists` | List columns on a board |
| `list_cards` | List cards on a board |
| `create_board` | Create a new board (requires Project Manager role) |
| `create_list` | Create a new column on a board |
| `create_card` | Create a new card in a list |
| `update_card` | Update card name/description |
| `move_card` | Move card to different list |
| `delete_card` | Delete a card |
| `delete_list` | Delete a list and all its cards |

## Claude Code Integration

Add to `~/.claude/mcp.json`:

```json
{
  "mcpServers": {
    "planka": {
      "command": "/path/to/planka-mcp",
      "env": {
        "PLANKA_URL": "https://kanban.local",
        "PLANKA_EMAIL": "user@example.com",
        "PLANKA_PASSWORD": "your-password"
      }
    }
  }
}
```

Then restart Claude Code or run `/mcp` to see the server.

## Extending

To add new tools:

1. Add HTTP method to `src/planka/client.rs`
2. Add any new types to `src/planka/types.rs`
3. Add tool definition and handler to `src/tools/mod.rs`

Future tools to consider:
- `add_comment` - Add comment to a card
- `set_due_date` - Set card due date
- `add_label` - Add label to a card

## License

MIT
