# Notion CRM

Natural language CRM on top of Notion. Pipedrive-style entity model with MCP-powered interaction.

## Task Routing

| Task Type | Go To | Description |
|-----------|-------|-------------|
| Connect and audit | `stages/01-connect-audit/CONTEXT.md` | Connect MCP, inventory Notion databases, classify CRM entities, identify gaps |
| Design CRM schema | `stages/02-schema-design/CONTEXT.md` | Design Deals, Contacts, Organizations, Activities databases with properties and relations |
| Implement schema | `stages/03-schema-implementation/CONTEXT.md` | Create and configure databases in Notion, set up Kanban views |
| Daily CRM operations | (this folder) | Natural language CRM: create deals, move pipeline, query, report |

## Shared Resources

| Resource | Location | Contains |
|----------|----------|----------|
| CRM entity model | `references/crm-entity-model.md` | Pipedrive entities mapped to Notion schema |
| Pipeline config | `references/pipeline-config.md` | Pipeline stages and configuration |
| Notion MCP setup | `references/notion-mcp-setup.md` | How to get an API token and configure MCP |
| NL query patterns | `references/nl-query-patterns.md` | Natural language patterns mapped to MCP tool sequences |
| Report templates | `references/report-templates.md` | CRM report patterns with public URL generation |
| Integration patterns | `references/integration-patterns/` | Email, calendar, and WhatsApp integration guides |
