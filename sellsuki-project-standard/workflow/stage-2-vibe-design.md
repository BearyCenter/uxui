# Stage 2 — Vibe Design

**Position:** `Research & Plan → VIBE DESIGN → Vibe Code`

---

## Purpose

สร้าง **hi-fi design variants** ด้วย AI ให้ลูกค้าเลือก — ไม่ใช่ wireframe ก่อน hi-fi แบบ product flow

---

## Trigger

- Stage 1 ผ่าน gate — research + plan + stack locked

---

## Input

- `project-card.md` (Section 1-5 complete)
- `research-plan.md`
- Brand assets (logo, color palette, font)
- Stack decision (locked)
- Reference site list

---

## Activities

### 2.1 Generate variants (the core of this stage)

| Size | # Variants | Time |
|---|---|---|
| S | 1-2 | 1-2 hours |
| M | 2 | 0.5-1 day |
| L/Enterprise | 2-3 | 1-2 days |

**Variant rules:**
1. ทุก variant ต้อง **defendable** — ไม่มี "weak option" ทำขึ้นเป็น contrast
2. แต่ละ variant มี **distinct direction** — ไม่ใช่ "variant A สีฟ้า variant B สีเขียว"
3. Direction มี name — ตัวอย่าง: "Variant A — Dashboard-first", "Variant B — Workflow-first"

### 2.2 How to generate

**Tool options:**
1. **Claude HTML artifact** — interactive, paste-able, client can click through
2. **Claude SVG widget** — static screen mockups, fast
3. **Figma Make / Figma AI** — if higher fidelity needed
4. **Visualize widget** (visualize:show_widget) — for inline preview

**Recommended:** HTML artifact ที่ใช้ stack จริง (DS components หรือ client lib) — `validate_usage` ได้ใน Stage 3

### 2.3 Annotate each variant

Per variant:
- Direction name + 1-line description
- 3-5 screens minimum (or all required screens for S)
- Click-through flow (happy path)
- Trade-off note: "Variant A optimizes for X but costs Y"

### 2.4 Optional: mini AI usability test (L/Enterprise)

ก่อน present variants ให้ client:
- ใช้ persona จาก `references/ai-persona-library.md`
- Run quick walk-through ของแต่ละ variant
- Identify obvious friction → fix before client sees

---

## Client checkpoint #1 — Variant pick

**Critical gate** — ห้าม proceed Stage 3 จนกว่าจะมี explicit pick

**Format ที่ส่งให้ PM forward client:**

```
นำเสนอ design 2 variants:

A) [Direction A] — [1-line summary]
   Screenshot/link: [...]
   Trade-off: [...]

B) [Direction B] — [1-line summary]
   Screenshot/link: [...]
   Trade-off: [...]

ลูกค้ารบกวนเลือก:
1. Variant A หรือ B (หรือ hybrid)
2. ส่วนใดที่ชอบจาก variant อื่น (ถ้ามี)
3. ส่วนใดที่อยากปรับ (ถ้ามี)

Deadline: [date จาก milestone plan]
```

ถ้าลูกค้าตอบไม่ชัด:
- Ask PM to facilitate decision call
- Don't proceed with "default" guess

---

## Output

- 2+ variant artifacts (HTML/SVG/Figma link)
- `vibe-design-spec.md` ครบสำหรับ variant ที่ลูกค้าเลือก
- Client pick documented (ใน vibe-design-spec)
- Hybrid notes (ถ้าลูกค้าขอผสม)

---

## Gate to Stage 3

- [ ] Client explicitly picked a variant (หรือ hybrid)
- [ ] `vibe-design-spec.md` final สำหรับ picked variant
- [ ] All screens designed (ไม่ใช่แค่ hero)
- [ ] States ครบ: default, loading, empty, error, success, disabled
- [ ] Responsive ระบุ
- [ ] Component inventory พร้อม (สำหรับ Stage 3)
- [ ] Stack consistency check — design ใช้แค่ component ของ stack ที่ lock ไว้

---

## Common Mistakes

- สร้าง 1 variant แล้ว iterate กับ client → loop ยาว, no closure
- สร้าง "weak variant" เป็น filler → client เห็นทะลุ, ทีมเสีย credibility
- Direction variant ใกล้กันเกินไป → ไม่ช่วยลูกค้าตัดสินใจ
- Variant สวยแต่ flow ขาด — focus หา hero, ลืม empty/error state
- ไม่ระบุ trade-off → ลูกค้าเลือกแบบไม่รู้ implication
- Proceed Stage 3 โดย "เดา" สิ่งที่ลูกค้าน่าจะเลือก

---

## Owner

| Role | Responsibility |
|---|---|
| Claude | Generate variants, draft spec, present trade-off |
| Level 1 Designer | Curate variants, validate brand alignment, present to PM |
| Level 2 Lead | Review variants before client sees (L/Enterprise) |
| PM | Channel variants to client, facilitate decision |
