# Stage 0 — Brief Intake

**Position:** `PM Brief → BRIEF INTAKE → Research & Plan`

---

## Purpose

แปลง raw brief จาก PM (Word/Slack/voice/email/meeting note) → **PM Card structured** ที่ใช้ start project ได้

---

## Trigger

ทันทีที่:
- PM forward brief (Slack, email, doc link)
- ผู้ใช้พูดถึงลูกค้า + intent ของงาน
- มี attachment (Word, PDF, meeting recording transcript) จาก client conversation
- Phrase: "PM ส่งมา", "ลูกค้าอยาก", "เริ่ม project ใหม่"

---

## Input

- Raw brief ในรูปแบบใดก็ตาม:
  - Pasted text
  - Word/PDF document (Claude reads via file-reading skill)
  - Meeting transcript
  - Email forward
  - Slack thread paste
  - Voice note transcript

---

## Activities

| Activity | Description | How Claude does it |
|---|---|---|
| Read raw brief | Parse whatever PM provided | Direct read / file-reading skill |
| Extract requirements | List explicit + implicit asks | `references/client-brief-parsing.md` |
| Identify client context | Industry, brand, current state | Inference + targeted question if missing |
| Detect tech hints | Stack mentioned? Existing infrastructure? | Scan for tech keywords |
| Classify size | S / M / L / Enterprise | `references/project-sizing.md` |
| Detect stack preference | Client's existing stack OR modern default OR custom | `references/tech-stack-guide.md` |
| Draft PM Card | กรอก `templates/project-card.md` | Auto fill |
| Plan milestones | Stage timing + client checkpoints | Based on size + urgency |
| Present plan | Plan summary (8-12 lines) | Plan summary template ใน SKILL.md |

---

## Output

- `project-card.md` ครบ Section 1-3 อย่างน้อย
- Plan summary in chat
- Open questions list — สิ่งที่ต้องถาม PM/client ก่อน Stage 1

---

## Gate to Stage 1

- [ ] PM Card มี objective + scope + deliverable list (อย่างน้อย)
- [ ] Client tier classified (S/M/L/Enterprise) — มี rationale
- [ ] Timeline expectation captured (deadline หรือ "ไม่มี")
- [ ] Tech stack hint captured (DS or client's own)
- [ ] Plan summary posted
- [ ] Open questions resolved or marked "non-blocking"

---

## When to ask PM/client

**ถาม PM** (ก่อน proceed):
- Deadline + budget signal
- Who is the end user
- Existing brand/style assets (logo, color, fonts)
- Hosting/deploy environment

**ถามลูกค้าผ่าน PM** (เป็น batch):
- Reference sites they like
- Must-have vs nice-to-have
- Maintain by whom after handoff

**อย่าถาม:**
- Implementation detail (ลูกค้าไม่ต้องคิด)
- Design opinion ละเอียดเกินไป — เก็บไว้ Stage 2 variant pick

---

## Common Mistakes

- รับ brief แล้วเริ่ม design เลยโดยไม่สร้าง PM Card → context หาย, ทีมตามไม่ได้
- ถาม PM เยอะเกินไปตอนต้น → frustrate ลูกค้า — รวบถามเป็น batch
- Underestimate size เพราะ brief สั้น → brief สั้นอาจหมายถึง scope ใหญ่ที่ลูกค้ายังไม่บอก
- ลืม timeline expectation → plan ออกมาไม่ realistic
- ไม่ระบุ "out of scope" → scope creep ใน Stage 5

---

## Example output (snippet)

```
📋 Project: Acme Corp — "Order management portal for B2B partners"
🏷  Tier: M / 2.5 weeks / first time client
🛠  Stack hint: ลูกค้ามี existing React app → suggest using their stack (read their codebase Stage 1)
🎯 Objective: B2B partners ของ Acme สามารถดู order status + เปิด case ผ่าน self-service portal

📦 Brief source: PM forward email + meeting recording (transcribed)
📅 Deadline mentioned: end of next month (~6 weeks) — relaxed
👥 End users: ~50 B2B account managers from Acme's partners

แผน (preview):
  ✓ Stage 0 — PM Card built (project-card.md draft)
  → Stage 1 — Research: scan B2B portal patterns, milestone plan (1 day)
  → Stage 2 — Vibe Design: 2 variants (order list focus vs case focus) (3 days)
  → Stage 3 — Vibe Code: 4-5 days
  → Stage 4 — Deploy staging
  → Stage 5 — UAT 2 rounds budgeted
  → Stage 6 — Handoff

⚠ Open questions for PM:
  - ลูกค้ามี brand guide / style guide ไหม?
  - Existing API ของ order status พร้อมไหม หรือ mock เอา?
  - User accounts มาจาก SSO หรือต้อง self-register?
  - Maintain หลังจบ project: ทีมลูกค้า หรือ Sellsuki ต่อ?

🚀 ผม start Stage 1 ต่อเลย ระหว่างนี้รบกวน PM ตอบ 4 ข้อด้านบนนะ
```

---

## Owner

| Role | Responsibility |
|---|---|
| Claude | Parse brief, draft PM Card, plan milestone |
| Level 1 Designer | Review card, validate classification, set client expectation |
| PM | Confirm gaps, get answers from client |
| Level 2 Lead | Spot-check L/Enterprise projects |
