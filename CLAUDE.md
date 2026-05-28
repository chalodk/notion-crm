# Notion CRM

Natural language CRM on top of Notion. Connects via MCP, models Pipedrive-style entities (Deals, Contacts, Organizations, Activities), and lets you manage your entire sales pipeline by typing what you want.

## Entry Flow

On every entry, the agent checks whether Notion MCP is configured:

- **No credentials:** The agent guides the user step by step: obtain a Notion API token, configure the MCP server, verify the connection. Load `references/notion-mcp-setup.md` for detailed instructions.
- **Credentials OK + stages pending:** Route to the first incomplete stage (run `status` to see which).
- **Credentials OK + all stages complete:** Enter operational mode. Load CRM references and wait for natural language input.

## Folder Map

```
notion-crm/
├── CLAUDE.md              (you are here)
├── CONTEXT.md             (start here for task routing)
├── setup/
│   └── questionnaire.md   (onboarding -- Notion token, pipeline preferences)
├── references/
│   ├── crm-entity-model.md        (Pipedrive entities mapped to Notion)
│   ├── pipeline-config.md         (stages and pipeline configuration)
│   ├── notion-mcp-setup.md        (how to get a token and configure MCP)
│   ├── nl-query-patterns.md       (natural language -> MCP operations)
│   ├── report-templates.md        (CRM report patterns with public URLs)
│   └── integration-patterns/      (email, calendar, WhatsApp guides)
├── stages/
│   ├── 01-connect-audit/          (connect MCP, audit Notion workspace)
│   ├── 02-schema-design/          (design CRM databases and relations)
│   └── 03-schema-implementation/  (create and configure databases in Notion)
└── shared/                        (cross-stage reference files)
```

## Triggers

| Keyword | Action |
|---------|--------|
| `setup` | Run onboarding questionnaire -- configure Notion token, pipeline, currency |
| `status` | Show pipeline completion for all three stages |

## Routing

| Task | Go To |
|------|-------|
| Connect to Notion and audit the workspace | `stages/01-connect-audit/CONTEXT.md` |
| Design the CRM database schema | `stages/02-schema-design/CONTEXT.md` |
| Implement the schema in Notion | `stages/03-schema-implementation/CONTEXT.md` |

## What to Load

| Task | Load These | Do NOT Load |
|------|-----------|-------------|
| Connect and audit | `references/notion-mcp-setup.md` (if MCP not configured), `stages/01-connect-audit/CONTEXT.md` | `stages/02-schema-design/`, `stages/03-schema-implementation/`, `references/crm-entity-model.md` |
| Schema design | `stages/02-schema-design/CONTEXT.md`, `../01-connect-audit/output/workspace-audit.md`, `references/crm-entity-model.md`, `references/pipeline-config.md` | `stages/03-schema-implementation/`, `references/nl-query-patterns.md` |
| Schema implementation | `stages/03-schema-implementation/CONTEXT.md`, `../02-schema-design/output/crm-schema.md` | `stages/01-connect-audit/`, `references/crm-entity-model.md` |
| Daily CRM operations | `references/crm-entity-model.md`, `references/pipeline-config.md`, `references/nl-query-patterns.md`, `references/report-templates.md`, and relevant integration-patterns if configured | Stage CONTEXT.md files (already completed) |

## Stage Handoffs

Each stage writes its output to its own `output/` folder. The next stage reads from there. If you edit an output file between stages, the next stage picks up your edits.

The typical flow is sequential (01 through 03). After all three stages are complete, the workspace enters operational mode for daily CRM use.
