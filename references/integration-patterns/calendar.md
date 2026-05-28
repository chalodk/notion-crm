# Calendar Integration

How to connect calendar to the CRM so the agent can schedule meetings, check availability, and log calls against deals and contacts.

**Status:** Conditional. Loaded only when `google` is set to `google` or `outlook`.

---

## Setup

### Google Calendar

1. Install a Google Calendar MCP server. Options:
   - Community servers on npm: search `google-calendar-mcp` on GitHub
   - Official Google Calendar API via a custom MCP wrapper
2. Configure OAuth in `.mcp.json`
3. Verify connection: ask the agent to list today's events

### Outlook Calendar

1. Install a Microsoft Graph MCP server (covers both email and calendar)
2. Configure OAuth via Azure AD
3. Verify connection

---

## CRM Calendar Patterns

### Scheduling a Meeting

**User says:** "Agendá una reunión con [Contacto] para el [día] a las [hora]"

**Agent does:**
1. Find contact in Notion, get name and deal context
2. Check calendar availability via calendar MCP
3. Create calendar event: title = "Reunion: [Contacto] - [Deal]", attendees = [contact email], time = [specified]
4. Log as Activity in Notion: Type=meeting, Date=[meeting date], Deal=[deal], Contact=[contact], Outcome="Scheduled for [time]"
5. Return calendar event link

### Checking Availability

**User says:** "¿Cuándo tengo hueco esta semana?"

**Agent does:**
1. Query calendar for free/busy this week
2. Present open slots
3. If the user specifies a contact/deal, suggest slots and offer to schedule

### Logging a Call or Meeting

**User says:** "Recién llamé a [Contacto], hablamos 20 min sobre el pricing"

**Agent does:**
1. Find contact and active deal
2. Create Activity: Type=call, Date=now, outcome="20 min call re: pricing"
3. If there is a calendar event for this call, link it in the outcome

### Pre-meeting Brief

**User says:** "¿Qué tengo que saber antes de la reunión con [Contacto]?"

**Agent does:**
1. Find contact and their open deals
2. Query recent activities for the contact (last 5)
3. Query deal stage, value, and notes
4. Present a brief: who, what deal, current stage, last touchpoint, open questions
