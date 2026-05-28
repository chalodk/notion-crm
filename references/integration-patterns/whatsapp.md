# WhatsApp Integration

How to connect WhatsApp to the CRM so the agent can send messages and log conversations against deals and contacts.

**Status:** Future. This file is a placeholder for WhatsApp integration via Evolution API or similar. It is not loaded by default.

---

## Planned Architecture

WhatsApp integration will use the Evolution API to connect a WhatsApp number, enabling:

- Send messages to contacts from within the CRM
- Log incoming and outgoing messages as Activities
- Link WhatsApp conversations to deals and contacts

---

## Planned Setup

1. Deploy Evolution API instance (Docker on-prem or cloud)
2. Connect a WhatsApp number via QR code
3. Configure Evolution API credentials in `.mcp.json` or via a custom MCP server
4. Verify connection: send a test message

---

## Planned Patterns

### Sending a WhatsApp Message

**User says:** "Escribile a [Contacto] por WhatsApp sobre [Deal]"

**Agent does:**
1. Find contact in Notion, get phone number
2. Draft message based on deal context
3. Present draft to user
4. Send via Evolution API
5. Log as Activity: Type=message, channel=whatsapp, outcome="Sent WhatsApp re: [context]"

### Logging WhatsApp Conversations

**User says:** "Me escribió [Contacto] por WhatsApp, quiere acelerar el deal"

**Agent does:**
1. Find contact and active deal
2. Create Activity: Type=message, channel=whatsapp, Outcome="Incoming: wants to accelerate deal"
3. Suggest pipeline implications if relevant

---

## When to Implement

This integration will be built out when the `agent-tool-builder` workspace is used to generate WhatsApp tools from the Evolution API documentation. The two workspaces are designed to interoperate:

1. `agent-tool-builder` generates the Evolution API webhook backend with WhatsApp tools
2. `notion-crm` loads those tools and integrates them into CRM workflows

Until then, WhatsApp interactions should be logged manually as Activities.
