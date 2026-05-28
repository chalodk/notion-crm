# Pipeline Configuration

The sales pipeline stages that deals move through. A deal progresses from left to right. Won and Lost are terminal stages.

## Default Pipeline

```
New → Contacted → Qualified → Proposal → Negotiation → Won
                                                       ↘ Lost
```

## Stage Definitions

| Stage | Description | Entry Condition | Exit Condition |
|-------|------------|-----------------|----------------|
| New | Freshly created deal, no contact made | Deal is created | First contact attempted |
| Contacted | Initial outreach sent or call made | Contact logged (email, call, meeting) | Contact responded positively |
| Qualified | Contact showed interest, deal is viable | Response received, need confirmed | Formal proposal requested or sent |
| Proposal | Formal proposal or quote sent | Proposal document sent | Prospect responds to proposal |
| Negotiation | Terms being discussed, objections handled | Counter-offer or negotiation started | Agreement reached or deal lost |
| Won | Deal closed successfully | Contract signed or payment received | (terminal) |
| Lost | Deal did not close | Prospect declined, went silent, or chose competitor | (terminal) |

## Customization

`New, Contacted, Qualified, Proposal, Negotiation, Won, Lost`

To customize, provide a comma-separated list of stage names in order. The last stage(s) are terminal. Example:

```
New, First Contact, Meeting Scheduled, Demo Done, Proposal Sent, Negotiation, Closed Won, Closed Lost
```

If `New, Contacted, Qualified, Proposal, Negotiation, Won, Lost` is not customized, the default pipeline above is used.

## Stage Properties in Notion

The Deals database has a **Stage** property of type **Select** with each pipeline stage as an option. The Kanban view groups cards by this property.

Colors per stage (Notion defaults):
- New: Gray
- Contacted: Blue
- Qualified: Green
- Proposal: Yellow
- Negotiation: Orange
- Won: Green (dark)
- Lost: Red

## Movement Rules

- A deal can only move forward through stages (no skipping stages backward)
- Moving a deal to Won or Lost is final (terminal stages)
- Each stage change should be logged as an Activity linked to the deal
- The agent should ask for confirmation before moving a deal to Won or Lost
