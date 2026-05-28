# Natural Language Query Patterns

How the agent translates natural language CRM requests into Notion MCP operations. This is the runtime translation layer -- the agent consults these patterns when the user speaks in natural language.

---

## Pattern Categories

### Deal Creation

| User Says | MCP Tools | Sequence |
|-----------|-----------|----------|
| "Creá un deal para [Contacto] por [valor]" | `notion-find` → `notion-create-page` | Find the contact database, search for the contact by name, create a deal page with Title = "[Contacto Org] - Deal", set Value and Contact relation |
| "Abrí un nuevo deal con [Organización]" | `notion-find` → `notion-create-page` | Find org, create deal linked to org, stage = New |
| "Registrá una oportunidad para [Contacto] de [Org]" | `notion-search` → `notion-create-page` | Search for both, create deal linking both |

### Deal Querying

| User Says | MCP Tools | Sequence |
|-----------|-----------|----------|
| "¿Qué deals están en [Stage]?" | `notion-database-query` | Query Deals database, filter by Stage = [stage], return Title + Value + Contact + Expected Close |
| "Mostrame los deals de [Contacto]" | `notion-find` → `notion-database-query` | Find contact, query deals filtered by Contact relation |
| "¿Qué deals vencen esta semana?" | `notion-database-query` | Query Deals, filter Expected Close between today and today+7 |
| "¿Cuánto vale el pipeline total?" | `notion-database-query` | Query all open deals (not Won/Lost), sum Value |

### Pipeline Movement

| User Says | MCP Tools | Sequence |
|-----------|-----------|----------|
| "Pasá el deal de [X] a [Stage]" | `notion-find` → `notion-update-page` | Find the deal page, update Stage property |
| "Avanzá [Deal] a la siguiente etapa" | `notion-find` → `notion-update-page` | Find deal, get current stage, determine next stage from pipeline config, update |
| "Ganamos [Deal]" | `notion-find` → `notion-update-page` → `notion-create-page` | Find deal, set Stage = Won, create Activity logging the win |
| "Perdimos [Deal]" | `notion-find` → `notion-update-page` → `notion-create-page` | Find deal, set Stage = Lost, create Activity with reason |

### Contact and Organization

| User Says | MCP Tools | Sequence |
|-----------|-----------|----------|
| "Agregá un contacto: [Nombre], [Email]" | `notion-create-page` | Create contact page with name, email |
| "¿Qué contactos hay en [Org]?" | `notion-find` → `notion-database-query` | Find org, query contacts filtered by Organization relation |
| "¿De quién es el teléfono [número]?" | `notion-search` | Full-text search across contacts |

### Activity Logging

| User Says | MCP Tools | Sequence |
|-----------|-----------|----------|
| "Llamé a [Contacto], duró [X] min" | `notion-find` → `notion-create-page` | Find contact, create activity Type=call, set date=now, outcome="[X] min call" |
| "Registrá que mandé propuesta a [Deal]" | `notion-find` → `notion-create-page` | Find deal, create activity Type=email, outcome="Sent proposal" |

### Reporting

| User Says | MCP Tools | Sequence |
|-----------|-----------|----------|
| "Reporte de deals por etapa" | `notion-database-query` | Query all deals, group by Stage, count and sum Value per stage |
| "Deals ganados en [periodo]" | `notion-database-query` | Query deals where Stage=Won and last_edited_time in [period], return Title + Value + Contact |
| "Dame una URL pública del pipeline" | `notion-database-query` → share | Query Deals database, return the Kanban view URL. If public access is needed, guide user to enable sharing. |

---

## Pattern Rules

1. **Always resolve names before creating relations.** When the user says a name ("Juan Pérez"), first search for it, then use the found page ID for the relation.
2. **Confirm before destructive actions.** Moving to Won/Lost is final. Ask before deleting anything.
3. **Return URLs.** After creating or finding anything, include the Notion page/database URL so the user can click through.
4. **Use pipeline-config.md for stage order.** When advancing a deal, consult the canonical pipeline config to determine the next stage.
5. **Log everything as activities.** Every deal movement, contact made, email sent -- create an Activity so the timeline is complete.
