# Stage 01: Connect and Audit

Connect to Notion via MCP, inventory the workspace, and identify what CRM entities already exist and what is missing.

## Inputs

| Source | File/Location | Section/Scope | Why |
|--------|--------------|---------------|-----|
| User | Conversation | Notion workspace name or URL | Which workspace to operate on |
| Reference | `../../references/notion-mcp-setup.md` | Full file (if MCP not configured) | Guide user through token and MCP setup |
| Tool | Notion MCP server | Connection | Required to query Notion |

## Process

1. Check if Notion MCP is configured. If not, load `../../references/notion-mcp-setup.md` and guide the user step by step: obtain API token, configure MCP server, verify connection.
2. Ask the user which Notion workspace to use (if they have multiple).
3. Retrieve the list of all databases in the workspace via MCP.
4. For each database, capture: name, URL, all properties (name, type, options), all relations, row count.
5. Sample a few rows from each database to understand content and purpose.
6. Classify each database: which CRM entity does it map to? (Deal, Contact, Organization, Activity, Other). Note partial matches.
7. Identify gaps: which CRM entities have no corresponding database? Which existing databases are missing key CRM properties?
8. Flag existing data that must be preserved: databases with rows, properties with values, existing relations.
9. Write `workspace-audit.md` with: database inventory, CRM classification, gap analysis, preservation notes.
10. Run audit. Fix gaps before saving.

## Audit

| Check | Pass Condition |
|-------|---------------|
| MCP connected | Connection verified and working |
| All databases found | Every database in the workspace appears in the inventory |
| Properties captured | Every property per database listed with name and type |
| CRM classification | Each database classified (Deal/Contact/Org/Activity/Other) |
| Gaps explicit | Missing entities and missing properties are listed |
| Preservation flagged | Databases and properties that must not be deleted are marked |
| No credentials | Zero API tokens or secrets in the file |

## Outputs

| Artifact | Location | Format |
|----------|----------|--------|
| Workspace audit | `output/workspace-audit.md` | Database inventory, CRM classification, gap analysis, preservation notes |
