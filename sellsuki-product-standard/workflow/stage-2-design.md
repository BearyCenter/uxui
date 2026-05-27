# Stage 2 — Design

**Position:** `Research → DESIGN → AI Usability`

---

## Purpose

แปลง research output → IA → Wireframe → AI Prototype — เป็น **iteration เดียวกัน**, ไม่ใช่ 3 phase แยก

---

## Trigger

- Stage 1 ผ่าน gate — มี journey + IA impact + persona shortlist

---

## Input

- `intake-brief.md` (Section 1-2 complete)
- `research-journey.md`
- IA impact list
- Sellsuki Design System reference (DS1 หรือ DS2 — guideline ตั้งแต่ตอนนี้)

---

## Activities (in order — แต่ Claude generate ทั้งหมดในรอบเดียวก็ได้)

### 2.1 IA (Information Architecture)

| สิ่งที่ต้องทำ | Output |
|---|---|
| List screens ที่ affected | screen list with state |
| Define entry/exit point ของ flow | nav map snippet |
| Map data field ที่ต้อง show / collect | field-to-screen table |

### 2.2 Wireframe

**กฎ:**
- Low-fidelity, ASCII หรือ markdown table หรือ Mermaid (Claude generate ได้)
- ระบุครบทุก state: default, loading, empty, error, success, disabled
- Annotate behavior + interaction inline
- ใช้ component name ของ DS (ssk-button, ssk-input, ssk-modal) — ไม่ใช่ generic ("button A")

### 2.3 AI Prototype

ตัวเลือกในการสร้าง prototype:
1. **Claude SVG widget** (ใช้ `visualize:show_widget`) — ดีสำหรับ static screens
2. **Claude HTML artifact** — interactive, ทดสอบใน chat ได้
3. **Figma Make / Figma AI** (ถ้าทีมต้องการ design tool fidelity) — Claude generate Mermaid หรือ component spec ให้ paste

**Default:** Claude สร้าง HTML artifact ที่ใช้ DS component (ssk-* tags) — ทดสอบ flow ได้, paste เข้า Storybook ได้

---

## Output

- `ia-wireframe-spec.md` (ครบทุก section)
- Prototype artifact (HTML/SVG/Mermaid)
- Updated `design-spec.md` (Section 1-3) — living document, จะ finalize ใน Stage 4

---

## Gate to Stage 3 (AI Usability)

- [ ] ทุก screen ระบุครบ 6 states (default, loading, empty, error, success, disabled)
- [ ] Wireframe ใช้ component name ของ DS เท่านั้น
- [ ] Prototype run ผ่าน happy path ได้ (ไม่ break)
- [ ] Edge case ครบ — text ยาว, data = 0, no permission, network error
- [ ] Responsive behavior ระบุ (mobile / tablet / desktop)
- [ ] Self-critique passed — ถาม "designer ตัวเองเชื่อ flow นี้ไหม?"

---

## Self-critique checklist (Claude run ก่อน proceed)

- [ ] Flow มี dead-end หรือไม่?
- [ ] User รู้ว่าตัวเองอยู่ขั้นไหนของ flow?
- [ ] ถ้า user ผิดพลาด มี exit / undo path ไหม?
- [ ] Empty state มี action ที่ user ทำต่อได้ไหม?
- [ ] Error message บอกว่า "เกิดอะไร" และ "ทำอะไรต่อ"?
- [ ] Loading state มี progress signal ที่ชัดไหม?
- [ ] ทุก primary action มี label ที่ใช้ verb (ไม่ใช่ "OK", "Submit" เฉย ๆ)?

---

## Common Mistakes

- ทำ hi-fi ก่อน wireframe → lock ตัวเองที่ visual ก่อนคิด flow
- ใช้ generic component name → vibe code ใน Stage 5 จะ map ไม่ตรง DS
- Skip empty/error state → bug factory ใน Stage 5
- ไม่ annotate behavior → Stage 5 ต้องเดา interaction
- Prototype สวยแต่ test flow ไม่ได้ → Stage 3 ไม่มีอะไรให้ persona ลองทำ

---

## Owner

| Role | Responsibility |
|---|---|
| Claude | Generate IA + Wireframe + AI Prototype |
| Level 1 Designer | Iterate, critique, validate against research |
| Level 2 Lead | Review for L-card หรือ pattern ที่กระทบ DS |
