# Stage 4 — Refine

**Position:** `AI Usability → REFINE → Vibe Code`

---

## Purpose

Apply usability findings → finalize design-spec.md → พร้อม handoff ไป Stage 5

---

## Trigger

- Stage 3 ผ่าน gate — มี friction list ที่จัด severity แล้ว

---

## Input

- `persona-test-result.md` (ครบ)
- Must-fix friction list
- `design-spec.md` (draft จาก Stage 2)
- Prototype (artifact)

---

## Activities

| Activity | Description |
|---|---|
| Apply must-fix | แก้ wireframe + prototype ตาม blocker/major friction |
| Re-test (optional) | ถ้า must-fix เปลี่ยน flow มาก → run Stage 3 1 รอบสั้น ๆ |
| Finalize spec | กรอก `design-spec.md` ครบทุก section |
| Final self-critique | Run checklist ของ Stage 2 อีกครั้ง |
| Peer review (M/L card) | Share spec ใน Slack/Confluence ขอ feedback 1-2 คน |
| Lead approval (L card) | L2 review — ดู rules/standard-master.md |
| Update intake brief | กรอก final scope + open items ใน `intake-brief.md` |

---

## Iteration cap

| Size | Max refine cycles |
|---|---|
| S | 1 |
| M | 2 |
| L | 3 (mehr → escalate, อาจะ scope ใหญ่เกิน) |

ถ้า refine เกิน cap → signal ว่า "scope problem" — กลับไปคุย PO ที่ Stage 0

---

## Output

- `design-spec.md` final, ครบทุก section
- Open decisions list (ถ้ายังมี — ต้องปิดก่อน Stage 5)
- Deviation note: อะไรที่เห็นใน finding แต่ไม่ fix และเพราะอะไร

---

## Gate to Stage 5 (Vibe Code)

- [ ] Blocker friction ทั้งหมด fixed
- [ ] Major friction fixed หรือมี documented deviation
- [ ] `design-spec.md` ครบทุก section
- [ ] Open decisions เหลือ 0 (หรือ ระบุ assumptions ที่จะใช้)
- [ ] DS selection ตัดสินใจแล้ว (DS1 หรือ DS2 + brand variant ถ้าใช้ DS2)
- [ ] Peer review done (M/L card)
- [ ] Lead approve (L card)

---

## Confirmation gate กับ user

**ก่อน proceed Stage 5:**
Claude ถาม:
> Spec final แล้ว ผมจะ vibe code ด้วย **[DS1 / DS2 + variant]** — เห็นด้วยไหม?

User ต้อง explicitly OK เพราะ DS choice กระทบ implementation มาก

---

## Common Mistakes

- Fix ทุก friction รวม minor → over-engineering
- Refine แบบไม่ document → context หายไป Stage 5 ไม่รู้เหตุผล
- Skip peer review → bias ของ designer ติดไปจน production
- Finalize spec แต่ยังมี open decision → dev ต้องเดา ใน vibe code
- Refine จนเกิน iteration cap → ไม่ยอมรับว่า scope ใหญ่เกิน

---

## Owner

| Role | Responsibility |
|---|---|
| Claude | Generate spec revisions, suggest fix priority |
| Level 1 Designer | Decide what to fix, finalize spec, request peer review |
| Level 2 Lead | Approve L-card, validate DS choice |
