# Stage 1 — Research

**Position:** `Intake → RESEARCH → Design`

---

## Purpose

เข้าใจ user, context, และ existing flow ก่อนเริ่ม design — ใน depth ที่เหมาะกับ size ของ card

---

## Trigger

- Stage 0 ผ่าน gate — มี `intake-brief.md` draft แล้ว
- Track + size classified

---

## Input

- `intake-brief.md` (draft)
- Parent Epic context (จาก Stage 0)
- Linked tickets, attachments, Confluence pages (ถ้ามี)
- Existing user journey docs / persona docs (ถ้าทีมมีไว้)

---

## Activities

| Activity | S-card | M-card | L-card | How |
|---|---|---|---|---|
| Re-use existing journey | ✓ default | ✓ if exists | ✓ if exists | Search Confluence / prev docs |
| User journey map (new) | skip | ✓ (1 happy path + 1 edge) | ✓ (multi-path, multi-persona) | Generate from AC + context |
| IA prep | skip if no new screen | ✓ light | ✓ full sitemap impact | List affected screens + nav |
| Competitive scan | skip | optional | ✓ required | Search 2-3 similar products |
| Persona signals | inherit from epic | ✓ identify 1-2 personas | ✓ identify 3+ personas | Match to library + custom signals |
| Stakeholder context | skip | quick check | ✓ list stakeholders + their priority | Read Epic comments |

> Claude generates the artifacts, designer reviews — not the other way around.

---

## How to do user journey (the AI-first way)

Claude สามารถ generate journey map ได้จาก:
1. AC ของ card (ต้องการ flow อะไร)
2. Parent Epic (context ของ user task ใหญ่)
3. Persona ที่ identify (ใคร, ทำอะไร, blocker อะไร)

**Format:**
```
User: [persona]
Goal: [task ที่ทำ]
Trigger: [อะไร start flow นี้]

Steps:
  1. [action] → feels: [emotion] → friction: [if any]
  2. ...

Touchpoints affected: [screens / channels]
Success: [user คิดว่า "เสร็จ" เมื่อไหร่]
```

ถ้า user ไม่รู้ persona ที่ชัด → Claude อ้าง `references/ai-persona-library.md` แล้วเสนอ 1-2 ตัวที่ใกล้ที่สุด

---

## Output

- `research-journey.md` ครบ (สำหรับ M/L) หรือ inline note (S)
- IA impact list — ถ้ามี screen ใหม่/แก้ nav
- Persona shortlist — ไว้ใช้ใน Stage 3

---

## Gate to Stage 2

- [ ] Journey map exists (referenced หรือ newly drafted)
- [ ] Persona ที่จะ test ใน Stage 3 identify แล้ว
- [ ] IA impact assessed (screens affected, nav changes)
- [ ] ไม่มี open question ที่ block design (ถ้ามี → ถาม PO ก่อน)

---

## Common Mistakes

- ทำ journey เต็มสำหรับ S-card → over-engineering
- ใช้ persona generic เกินไป ("user") — ต้องมี attribute (role, frequency, tech-savvy)
- ข้าม IA impact → ไป design แล้วเจอว่าต้องแก้ nav ทั้งระบบ
- Research แล้วไม่ link กลับมา intake brief — ทำให้ Stage 2 ไม่รู้ว่าใช้ assumption ไหน

---

## When to ask the user

ถาม **เฉพาะ** กรณีนี้:
- Persona library ไม่มีตัวที่ใกล้ → ขอข้อมูลเพิ่ม
- AC ขัดแย้งกันเอง → ขอ clarification จาก PO
- Parent Epic หายไป / link เสีย

อย่างอื่น → Claude ตัดสินใจ default แล้ว document ใน journey ว่าใช้ assumption อะไร

---

## Owner

| Role | Responsibility |
|---|---|
| Claude | Generate journey, IA impact, persona shortlist |
| Level 1 Designer | Review, override Claude's interpretation, validate persona choice |
| Level 2 Lead | Required review for L-card (เพื่อ avoid scope drift) |
