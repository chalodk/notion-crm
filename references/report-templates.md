# Report Templates

Common CRM reports and how to generate them with public Notion URLs for sharing.

---

## Pipeline Overview

**What:** A snapshot of all open deals grouped by stage with total value per stage.

**How:**
1. Query Deals database, filter Stage != Won, Stage != Lost
2. Group by Stage, count deals per stage, sum Value per stage
3. Present as a table with Stage, Count, Total Value
4. Include link to the Deals Kanban view for visual inspection

**Public URL:** The Deals Kanban view URL. Notion Kanban views are shareable. Guide user to enable sharing: View menu → Share → Publish.

---

## Won/Lost Report

**What:** Deals closed in a date range, with win rate.

**How:**
1. Query Deals where Stage = Won or Lost
2. Filter by last_edited_time in the requested range
3. Count Won, count Lost, calculate win rate = Won / (Won + Lost)
4. List each deal with Title, Value, Contact, Organization, Close Date
5. Sort by Value descending

**Public URL:** Filtered table view URL pointing to the Deals database with Stage filter set to Won and Lost.

---

## Contact Activity Report

**What:** Recent activities for a specific contact or across all contacts.

**How:**
1. If specific contact: find contact, query Activities filtered by Contact relation
2. If all contacts: query Activities, sort by Date descending, limit to last N
3. Group by Type (call/email/meeting)
4. Present as timeline with Date, Type, Outcome, linked Deal

**Public URL:** Activities table view filtered and sorted by Date.

---

## Forecast Report

**What:** Deals expected to close in a future period with weighted value.

**How:**
1. Query all open deals (not Won/Lost)
2. Filter by Expected Close in the requested range
3. Apply probability weights per stage: Qualified=20%, Proposal=50%, Negotiation=80%
4. Calculate weighted value = Value × probability
5. Sum weighted and unweighted totals
6. List deals sorted by Expected Close

**Public URL:** Filtered Deals table view with Expected Close column.

---

## Generating Public URLs

Notion does not have a "create public share link" API. To share a view:

1. Open the database view in Notion
2. Click the view name → Share → Publish
3. Copy the public URL
4. The agent should open the URL for the user if they confirm

For reports that aggregate data (pipeline overview, win rate), the agent presents the summary directly in the conversation and offers to open the relevant Notion view as supporting detail.
