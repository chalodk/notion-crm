# Stage 02: Design CRM Schema

Design the complete CRM database schema for Notion: Deals, Contacts, Organizations, and Activities with all properties, relations, and views.

## Inputs

| Source | File/Location | Section/Scope | Why |
|--------|--------------|---------------|-----|
| Previous stage | `../01-connect-audit/output/workspace-audit.md` | Full file | Current Notion workspace state |
| Reference | `../../references/crm-entity-model.md` | Full file | Pipedrive entity definitions mapped to Notion |
| Reference | `../../references/pipeline-config.md` | Full file | Pipeline stages and configuration |

## Process

1. Read the workspace audit from Stage 01 and the CRM reference files.
2. For each CRM entity (Deals, Contacts, Organizations, Activities), design the Notion database:
   - Name, properties (name, type, options, required), relations to other databases, views (type, grouping, filter, sort).
3. For Deals: define the Stage select property with pipeline stages from `pipeline-config.md`. Design the Kanban view grouped by Stage.
4. For Activities: define standard types (call, email, meeting, note, task) and relations to Deals, Contacts, and Organizations.
5. For existing databases (from audit): design an additive modification plan. Add missing properties and relations. Never rename, delete, or re-type existing properties.
6. **[Checkpoint]** -- Present the complete schema: all databases with properties, relations, and views. User reviews naming, types, pipeline stages, and coverage.
7. Write `crm-schema.md` with: per-database property tables, relation map, view specifications, modification plan for existing databases.
8. Run audit. Fix gaps before saving.

## Checkpoints

| After Step | Agent Presents | Human Decides |
|------------|---------------|---------------|
| 5 | Complete schema: all databases with properties, relations, views | Whether naming, property types, pipeline stages, and entity coverage are correct |

## Audit

| Check | Pass Condition |
|-------|---------------|
| Four entities covered | Deals, Contacts, Organizations, and Activities databases all defined |
| Pipeline stages defined | Stage property has select options matching pipeline config |
| Relations explicit | Every cross-database relation is named with type and direction |
| Views specified | At least one view per database; Deals has Kanban grouped by Stage |
| Existing data preserved | Modification plan is additive only (no deletes, no renames, no type changes) |
| Properties typed | Every property has a Notion type |

## Outputs

| Artifact | Location | Format |
|----------|----------|--------|
| CRM schema | `output/crm-schema.md` | Per-database: properties table, relations, views. Modification plan for existing databases. |
