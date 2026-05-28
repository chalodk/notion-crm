# CRM Entity Model

How Pipedrive CRM entities map to Notion databases. This is the canonical reference for the CRM data model. Every stage that touches CRM entities reads from here.

---

## Entity: Deals

The central entity. A deal represents a sales opportunity with a contact at an organization. Deals move through pipeline stages from New to Won or Lost.

### Standard Properties

| Property | Notion Type | Required | Description |
|----------|------------|----------|-------------|
| Title | Title | Yes | Deal name. Convention: "[Organization] - [Product/Service]" |
| Stage | Select | Yes | Pipeline stage. Options from `pipeline-config.md` |
| Value | Number | Yes | Deal value in `CLP` |
| Expected Close | Date | No | Expected close date |
| Contact | Relation → Contacts | Yes | Primary contact for this deal |
| Organization | Relation → Organizations | No | Organization this deal belongs to |
| Activities | Relation → Activities | No | Linked activities (calls, emails, meetings) |
| Owner | Person | No | Team member responsible for this deal |
| Notes | Text | No | Free-text notes about the deal |
| Created | Created time | Auto | When the deal was created |

### Custom Properties

`Product (Select)`

Default: none. Examples of common additions: Product (Select), Lead Source (Select), Priority (Select: High/Medium/Low), Probability (Number, 0-100).

### Views

- **Kanban by Stage** (primary): Cards grouped by Stage, ordered by pipeline position. Shows Title, Contact, Value, Expected Close.
- **Table** (backup): All properties as columns. Sortable and filterable.
- **Calendar by Expected Close** (optional): Shows deals on a timeline.

---

## Entity: Contacts

A person you are selling to or communicating with. Contacts are linked to deals and organizations.

### Standard Properties

| Property | Notion Type | Required | Description |
|----------|------------|----------|-------------|
| Name | Title | Yes | Full name |
| Email | Email | No | Primary email address |
| Phone | Phone | No | Primary phone number |
| Organization | Relation → Organizations | No | Organization this contact belongs to |
| Deals | Relation → Deals | No | Deals this contact is involved in |
| Activities | Relation → Activities | No | Linked activities |
| Notes | Text | No | Free-text notes |

### Custom Properties

`Role (Text)`

Default: none. Examples: Role (Select), LinkedIn (URL), Lead Status (Select: Active/Inactive/Customer).

### Views

- **Table** (primary): All contacts with name, email, phone, organization.
- **Gallery** (optional): Contact cards with photo if available.

---

## Entity: Organizations

A company or organization that contacts and deals belong to.

### Standard Properties

| Property | Notion Type | Required | Description |
|----------|------------|----------|-------------|
| Name | Title | Yes | Organization name |
| Website | URL | No | Company website |
| Industry | Select | No | Industry category |
| Contacts | Relation → Contacts | No | Contacts at this organization |
| Deals | Relation → Deals | No | Deals with this organization |
| Notes | Text | No | Free-text notes |

### Views

- **Table** (primary): All organizations with name, website, industry.

---

## Entity: Activities

Actions linked to deals, contacts, or organizations. Activities track every touchpoint in the sales process.

### Standard Properties

| Property | Notion Type | Required | Description |
|----------|------------|----------|-------------|
| Title | Title | Yes | Brief description of the activity |
| Type | Select | Yes | call, email, meeting, note, task |
| Date | Date | No | When the activity occurred or is scheduled |
| Deal | Relation → Deals | No | Deal this activity relates to |
| Contact | Relation → Contacts | No | Contact this activity relates to |
| Organization | Relation → Organizations | No | Organization this activity relates to |
| Outcome | Text | No | Summary of what happened |
| Due | Date | No | Due date (for tasks and follow-ups) |
| Done | Checkbox | No | Whether the activity is complete |

### Views

- **Table** (primary): Grouped by Type or Date. Shows Title, Type, Date, Deal, Contact, Done.
- **Calendar by Due** (optional): Tasks and meetings on a timeline.
- **Filtered by Deal** (optional): Activities for a specific deal.

---

## Relation Map

```
Organizations ──→ Contacts ──→ Deals
     │               │            │
     └───────→ Activities ←────────┘
```

- A deal has one contact (primary) and optionally one organization
- A contact belongs to optionally one organization
- An activity can link to any combination of deal, contact, organization
- All relations are two-way in Notion
