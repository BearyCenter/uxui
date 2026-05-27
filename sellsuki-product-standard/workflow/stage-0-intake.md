# Stage 0 — Intake

**Position:** `Jira Card → INTAKE → Research`

---

## Purpose

Parse Jira card, classify ทั้ง track + size, และวาง plan ของ flow ทั้งหมด — **ภายในไม่กี่นาที** หลังจาก card เข้า

---

## Trigger

ทันทีที่เจอ signal เหล่านี้:
- Jira URL: `*.atlassian.net/browse/XXX-NNN`
- Jira key: `PROJ-123`, `SUKI-45`, `OC-2`
- พาดถึง Epic/Story/Card ในข้อความ
- ผู้ใช้ paste content ของ ticket

---

## Input

- Jira key หรือ URL (Claude ดึงข้อมูลเอง via Atlassian MCP)
- หรือ pasted content ถ้า MCP ใช้งานไม่ได้

---

## Activities

| Activity | Description | How Claude does it |
|---|---|---|
| Fetch card | ดึง summary, description, AC, attachments, links, parent epic | `Atlassian:getJiraIssue` |
| Identify parent | ถ้าเป็น Story → ดู Epic; ถ้า Epic → list child stories | `Atlassian:searchJiraIssuesUsingJql` with `parent = X` |
| Extract AC | List acceptance criteria จาก description หรือ custom field | Regex/heuristic |
| Classify track | Product (internal Sellsuki) vs Project (client) | จาก project key / label / epic context |
| Classify size | S / M / L | จาก signals — ดู `references/card-classification.md` |
| Detect DS hint | ถ้า card หรือ epic mention brand/product → ตั้ง default DS | ดู `references/ds-selection-guide.md` |
| Draft intake brief | กรอก `templates/intake-brief.md` | Auto fill จาก fetched data |
| Plan stages | เลือกว่า stage ไหน run full / compress / skip | จาก size + track |
| Present plan | สรุปสั้น ๆ ให้ user ดู (5-10 บรรทัด) | Plan summary template ใน SKILL.md |

---

## Output

- `intake-brief.md` (draft, ครบ Section 1-2 อย่างน้อย)
- Plan summary ใน chat (text)
- Stage 0 status: ready → Stage 1

---

## Gate to Stage 1

- [ ] Card data ดึงครบ (summary, description, AC at least 1)
- [ ] Track classified (Product / Project)
- [ ] Size classified (S / M / L) — Claude อธิบาย rationale ได้
- [ ] Plan summary posted in chat
- [ ] User ไม่ได้ interrupt หรือบอกให้ปรับ

> ถ้า user เงียบหลัง plan summary → ถือว่า "go" → proceed Stage 1
> ถ้า user มี comment → adjust plan แล้วค่อยไป

---

## Common Mistakes

- ดึง card แล้วถาม "อยากให้ทำอะไรต่อ?" — เสียประโยชน์ของ skill, ควร auto-plan ก่อน
- กระโดดไป Stage 2 (design) เลยโดยไม่ทำ intake brief — ไม่มี trace ของการตัดสินใจ
- Classify size ตามความรู้สึก — ต้องอ้าง signals ที่เห็นได้
- ลืม parent Epic — context หาย, อาจ design ขัดกับสิ่งที่ Epic วางไว้

---

## Example output (snippet)

```
📋 Card: SUKI-234 — "Add bulk export to order list"
🏷  Type: Product track / M-size
    Reason: 5 story points, 4 ACs, mentions new UI surface + backend dep

📦 Parent Epic: SUKI-200 — "Order management Q2"
   Sibling stories: SUKI-235 (filter), SUKI-236 (sort) — note: may share UI patterns

🎯 Direction: Let merchants export filtered orders to CSV/Excel without leaving the list view

แผน:
  ✓ Stage 0 — intake-brief.md drafted
  → Stage 1 — Light research (journey for export, no new persona)
  → Stage 2 — Wireframe (export dialog + state management)
  → Stage 3 — AI Usability: power user (merchant with 1000+ orders)
  → Stage 4 — 1 iteration likely
  → Stage 5 — Vibe code with DS2 (current standard for order module)

🛑 Confirm needed before Stage 3 และ Stage 5
🚀 ผม run ต่อเลยนะ ถ้าอยากปรับ plan บอกได้
```

---

## Owner

| Role | Responsibility |
|---|---|
| Claude (AI) | Execute parsing + classification + planning |
| Level 1 Designer | Review plan, override if needed |
| Level 2 Lead | Spot-check for L-cards |
