# Onboarding Questionnaire

Agent instructions: Read this file when the user types `setup`. Ask ALL questions in a single conversational pass. The user should be able to answer everything in one message. Collect answers. Replace placeholders across the specified files. After all replacements, scan the entire workspace for remaining `{{` patterns. If any remain, flag them and ask for the missing information.

---

### Q1: Do you have a Notion API token ready?
- Type: yes/no guidance
- If NO: The agent guides the user through `references/notion-mcp-setup.md` to obtain one. The user provides the token when ready.
- If YES: The agent verifies the MCP connection. If it fails, troubleshoot using the setup guide.

### Q2: Custom pipeline stages
- Placeholder: `{{PIPELINE_STAGES}}`
- Files: `references/pipeline-config.md`
- Type: free text (comma-separated list)
- Default: New, Contacted, Qualified, Proposal, Negotiation, Won, Lost
- Note: Use the default unless you need different stage names or additional stages. The last one(s) should be terminal stages.

### Q3: Default currency for deal values
- Placeholder: `{{CURRENCY}}`
- Files: `references/crm-entity-model.md`
- Type: selection
- Options: USD, EUR, ARS, MXN, CLP, COP, PEN, Other
- Default: USD

### Q4: Additional deal properties beyond the standard set
- Placeholder: `{{DEAL_CUSTOM_FIELDS}}`
- Files: `references/crm-entity-model.md`
- Type: free text (describe what extra fields you want on deals)
- Default: none
- Example: "Product (Select: Consulting, Software, Support), Lead Source (Select: Referral, Web, Event, Cold)"

### Q5: Additional contact properties beyond the standard set
- Placeholder: `{{CONTACT_CUSTOM_FIELDS}}`
- Files: `references/crm-entity-model.md`
- Type: free text (describe what extra fields you want on contacts)
- Default: none
- Example: "Role (Text), LinkedIn (URL), Birthday (Date)"

### Q6: Do you want email integration?
- Placeholder: `{{EMAIL_PROVIDER}}`
- Files: `references/integration-patterns/email.md`
- Type: selection
- Options: none, gmail, outlook
- Default: none
- Note: If "none", the email integration pattern file will still exist but will not be loaded during operations. You can configure email later.

### Q7: Do you want calendar integration?
- Placeholder: `{{CALENDAR_PROVIDER}}`
- Files: `references/integration-patterns/calendar.md`
- Type: selection
- Options: none, google, outlook
- Default: none
- Note: If "none", the calendar integration pattern file will still exist but will not be loaded. You can configure calendar later.

---

## After Onboarding

The agent:
1. Replaces all placeholders with answers across all specified files
2. Guides the user through MCP setup if not already configured
3. Scans the entire workspace for remaining `{{` patterns
4. Verifies the Notion MCP connection is working
5. Reports: "Notion CRM is ready. Run `status` to see the pipeline. Start with Stage 01 to audit your Notion workspace."
