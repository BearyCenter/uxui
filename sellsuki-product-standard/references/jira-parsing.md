# Jira Parsing Reference

> วิธี Claude extract ข้อมูลจาก Jira card ใน Stage 0

---

## Available Atlassian MCP tools

Already connected in this workspace. Common tools (deferred — `tool_search` ก่อนใช้):

| Tool | Use |
|---|---|
| `Atlassian:getAccessibleAtlassianResources` | Get cloudId — call once first |
| `Atlassian:getJiraIssue` | Fetch single card by key |
| `Atlassian:searchJiraIssuesUsingJql` | Find related (siblings, parent's children) |
| `Atlassian:getJiraProjectIssueTypesMetadata` | Know what issue types exist |
| `Atlassian:getTransitionsForJiraIssue` | Know workflow state |
| `Atlassian:searchConfluenceUsingCql` | Find research docs |
| `Atlassian:getConfluencePage` | Read research doc body |

---

## Step-by-step parse

### 1. Get cloudId (once per session)
```
Atlassian:getAccessibleAtlassianResources
```
Save the cloudId for subsequent calls.

### 2. Fetch the card
```
Atlassian:getJiraIssue
  cloudId: {cloudId}
  issueIdOrKey: {SUKI-234}
  fields: ["summary", "description", "issuetype", "status", "priority",
           "labels", "components", "parent", "subtasks", "issuelinks",
           "customfield_xxx (acceptance criteria, if separate field)",
           "attachment", "created", "updated", "duedate"]
```

### 3. Identify parent + siblings
If the card has a parent epic:
```
Atlassian:searchJiraIssuesUsingJql
  jql: "parent = {parent-key}"
  fields: ["summary", "status", "issuetype"]
```

### 4. Pull linked Confluence (research docs)
If description references Confluence:
```
Atlassian:searchConfluenceUsingCql
  cql: "type = page AND text ~ \"{card key}\""
```

---

## Fields to extract

| Field | Where in Jira | Goes to intake brief |
|---|---|---|
| Card key | URL or `key` | Section 1 |
| Title | `summary` | Section 1 |
| Type | `issuetype.name` | Section 1 |
| Description | `description` (may be ADF or markdown) | Section 3 |
| Acceptance criteria | `description` (parse) or custom field | Section 4 |
| Labels | `labels[]` | Classification signals |
| Components | `components[]` | DS hint (e.g., "order-module" → likely DS context) |
| Story points | `customfield_xxx` (varies by org) | Size signal |
| Priority | `priority.name` | Plan adjustment |
| Parent epic | `parent.key` + fetch epic | Section 1 |
| Linked issues | `issuelinks[]` | Section 1, dependencies |
| Attachments | `attachment[]` | Reference in research |

---

## Parsing AC from description

AC is usually inside the description. Common patterns:

### Pattern 1 — Headed list
```
Acceptance Criteria:
- User can click "Export" button
- A dialog appears with format options
- ...
```

### Pattern 2 — Given/When/Then
```
GIVEN merchant is on order list page
WHEN they click "Export" with filter applied
THEN a CSV file matching the filter downloads
```

### Pattern 3 — Numbered
```
AC:
1. ...
2. ...
```

### Pattern 4 — In a custom field
Some Jira projects have a separate "Acceptance Criteria" field — check custom fields after fetching.

**Claude's parsing approach:**
1. Look for "Acceptance Criteria", "AC", "Acceptance" header
2. If found, extract list items below
3. If not, fall back to bullet/numbered items in description
4. If still nothing, surface as open question in intake brief

---

## Handling missing fields

| Missing field | Action |
|---|---|
| Description | Block — ask PO before Stage 1 |
| AC | Add to open questions, draft AC from description if obvious |
| Story points | Use other signals for size classification |
| Parent epic | Note "no parent" in brief; if Story type, surface as concern |
| Labels | Skip — use other signals |

---

## When MCP isn't available (fallback)

If Atlassian MCP is disconnected:
1. Ask user to paste the card content
2. Parse from text using same field-extraction logic
3. Note in intake brief: "fetched manually — verify against Jira"

---

## Don't be a Jira nerd

The point of Stage 0 is to start work fast, not to be a Jira archaeologist. Stop fetching when:
- You have title, description, AC (or attempted AC), parent context
- You can classify track + size
- You can draft the plan

Other fields are nice-to-have, not blocking.

---

## Common Mistakes

- ❌ Fetch card → display all fields verbatim → user has to read Jira again
- ❌ Skip parent epic fetch → miss context for Story-type cards
- ❌ Misinterpret ADF (Atlassian Document Format) — request markdown format if needed (`contentFormat: "markdown"`)
- ❌ Get stuck because AC field is empty — draft from description, mark as assumption
- ❌ Fetch 50 fields when 6 are enough
