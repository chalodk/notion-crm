# Notion MCP Setup

How to connect Claude Code to Notion so this workspace can operate on your Notion databases.

---

## Quick Setup (Recommended)

Install the official Notion plugin from the Claude Code plugin marketplace:

```
/plugin marketplace add makenotion/claude-code-notion-plugin
/plugin install notion-workspace-plugin@notion-plugin-marketplace
```

This bundles the Notion MCP server, skills, and slash commands in one step. After installation, run `/mcp` in Claude Code to verify the Notion server is listed and connected.

---

## Manual Setup

If the plugin does not work for your setup, configure MCP manually.

### Step 1: Get a Notion API Token

1. Go to [notion.so/my-integrations](https://www.notion.so/my-integrations)
2. Click **New integration**
3. Give it a name (e.g., "Claude CRM")
4. Select your workspace
5. Copy the **Internal Integration Secret** (starts with `ntn_`)

### Step 2: Grant Access to Your Databases

For each database you want the CRM to access:

1. Open the database in Notion
2. Click the `...` menu in the top right
3. Go to **Connections** → **Add connections**
4. Select your integration ("Claude CRM")
5. Repeat for every database the CRM needs to touch

### Step 3: Configure MCP in Claude Code

Add the Notion MCP server to your project's `.mcp.json`:

```json
{
  "mcpServers": {
    "notion": {
      "url": "https://mcp.notion.com/mcp",
      "env": {
        "NOTION_TOKEN": "ntn_your_token_here"
      }
    }
  }
}
```

Or add it directly via CLI:

```bash
claude mcp add --transport http notion https://mcp.notion.com/mcp
```

### Step 4: Verify

Run `/mcp` in Claude Code. You should see `notion` listed as connected. The agent can now:
- Search your workspace
- List and read databases
- Create and update pages
- Insert database rows
- Read and update properties

---

## Troubleshooting

**MCP server not connecting:** Verify your token starts with `ntn_` and the integration has access to at least one database.

**Database not appearing:** Go to the database in Notion → Connections → add your integration. Notion requires explicit per-database access grants.

**Permission errors:** The integration needs "Read content" and "Insert content" capabilities at minimum. For schema changes (creating databases, adding properties), it also needs "Update content" capability.
