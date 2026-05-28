# Stage 03: Implement Schema in Notion

Create and configure the CRM databases in Notion via MCP. Set up all properties, relations, and views.

## Inputs

| Source | File/Location | Section/Scope | Why |
|--------|--------------|---------------|-----|
| Previous stage | `../02-schema-design/output/crm-schema.md` | Full file | Schema to implement |
| Tool | Notion MCP server | Connection | Required to create and modify databases |

## Process

1. Read the CRM schema from Stage 02.
2. Confirm with the user before making any changes: "I am about to create X databases and modify Y existing ones. Proceed?"
3. For each database in the schema:
   - If it does not exist: create it via MCP with all properties, then configure relations, then create all specified views.
   - If it exists: add only missing properties. Add new relations. Add new views. Leave existing properties and views unchanged.
4. Configure the Deals Kanban view: group by Stage, order stages by pipeline position.
5. Verify each database: confirm every property exists with correct type, relations resolve, Kanban view renders deals in correct stage columns.
6. Generate public share links for key views if the user wants them.
7. Write `implementation-report.md` with: what was created, what was modified, database URLs, verification results.
8. Run audit. Fix gaps before saving.

## Audit

| Check | Pass Condition |
|-------|---------------|
| Schema coverage | Every database from the schema exists in Notion |
| Property match | Every property from the schema exists with correct type |
| Relations functional | Every relation from the schema links correctly between databases |
| Kanban renders | Deals database has a Kanban view grouped by Stage |
| Existing data intact | No existing properties deleted, renamed, or re-typed |
| URLs documented | Database URLs and public share links are in the report |

## Outputs

| Artifact | Location | Format |
|----------|----------|--------|
| Implementation report | `output/implementation-report.md` | Created and modified databases, property/relation/view details, URLs, verification results |
