# Email Integration

How to connect email to the CRM so the agent can send, log, and track emails against deals and contacts.

**Status:** Conditional. Loaded only when `gmail` is set to `gmail` or `outlook`.

---

## Setup

### Gmail

1. Install a Gmail MCP server. Options:
   - Community servers on npm: search `gmail-mcp-server` on GitHub
   - Google's official APIs via a custom MCP wrapper
2. Configure OAuth or app password in `.mcp.json`
3. Verify connection: ask the agent to list recent emails

### Outlook

1. Install an Outlook/Microsoft Graph MCP server
2. Configure OAuth via Azure AD app registration
3. Verify connection: ask the agent to list recent emails

---

## CRM Email Patterns

### Sending an Email

**User says:** "Mandale un mail a [Contacto] sobre [Deal]"

**Agent does:**
1. Find contact in Notion, get email address
2. Draft the email based on deal context (stage, value, last activity)
3. Present draft to user for approval
4. Send via email MCP
5. Log as Activity in Notion: Type=email, Deal=[deal], Contact=[contact], Outcome="Sent email re: [subject]"

### Logging a Received Email

**User says:** "Me respondió [Contacto] sobre la propuesta"

**Agent does:**
1. Find contact and their active deal
2. Create Activity: Type=email, direction=inbound, Outcome="Received response re: proposal"
3. Optionally: if the email contains a decision signal, suggest a pipeline move

### Email to Activity Sync

**User says:** "Registrá mis últimos mails con [Contacto] como actividades"

**Agent does:**
1. Search recent emails with the contact via email MCP
2. For each email, check if it is already logged as an Activity (avoid duplicates)
3. Create Activity for each unlogged email: Type=email, Date=email date, Outcome=subject line summary
