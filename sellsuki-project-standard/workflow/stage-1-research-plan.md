# Stage 1 — Research & Plan

**Position:** `Brief Intake → RESEARCH & PLAN → Vibe Design`

---

## Purpose

วาง **research foundation + milestone plan** ที่ทีมและลูกค้าใช้ตามกันได้ — ก่อนเริ่ม design

---

## Trigger

- Stage 0 ผ่าน gate — มี PM Card + size classified

---

## Input

- `project-card.md` (draft)
- Open questions (ที่ PM กำลังถามลูกค้า — ไม่ต้องรอครบ, start ที่ตอบได้)
- Brand assets ที่ลูกค้าให้ (ถ้ามี)

---

## Activities

| Activity | S | M | L/Enterprise | Description |
|---|---|---|---|---|
| Domain research | inline (5-10 min) | 30-60 min | 2-4 hours | เข้าใจ industry ของลูกค้า |
| Reference scan | 1-2 refs | 3-5 refs | 5-10 refs | ดู product/service ที่คล้ายกัน |
| User mental model | quick note | dedicated section | full persona doc | end user คือใคร, mindset อย่างไร |
| Tech feasibility | skip | quick check | full audit | API, stack, integration constraints |
| Brand assimilation | use what's given | extract style tokens | full brand audit | logo, color, font, voice |
| Milestone plan | bullet list | gantt-style table | full timeline + buffer | when stage transitions, when client checkpoints |
| Risk identification | inline | risk list (3-5) | risk register | what could go wrong + mitigation |

---

## How to do research (AI-first)

Claude ทำ research ก่อน — designer review:

1. **Domain scan** — search "what does [industry] look like online", competitor list, common patterns
2. **Reference site analysis** — Claude visit + summarize 3-5 sites
3. **User model derivation** — จาก domain + brief, infer who uses it and why
4. **Pattern shortlist** — list common UI patterns for this domain (e.g., "B2B portal → typically has dashboard + list view + detail + filters + bulk actions")

Use these tools when available:
- `web_search` — pattern research
- `web_fetch` — deep dive on specific reference site
- `image_search` — visual reference for design inspiration

---

## Milestone plan structure

แต่ละ project มี **milestone plan** ที่ลูกค้าเห็นได้:

```
Week 1
  Day 1: Stage 0 — PM Card
  Day 2-3: Stage 1 — Research + Plan + Style direction
  Day 4-5: Stage 2 — Vibe Design (2 variants)
  → Client checkpoint #1: variant pick (end of Day 5)

Week 2
  Day 6-9: Stage 3 — Vibe Code chosen variant
  Day 10: Stage 4 — Deploy staging
  → Client checkpoint #2: UAT round 1 (Day 10)

Week 3
  Day 11-12: Stage 5 — Improve from UAT round 1
  Day 13: Client UAT round 2
  Day 14: Stage 5 — Final fixes
  Day 15: Stage 6 — Handoff package
  → Client checkpoint #3: Sign-off (Day 15)

Buffer: 2 days (for unforeseen UAT round)
```

---

## Stack decision (locked here)

Stage 1 = **the gate** ที่ตัดสินใจ stack final:
- **Client's existing stack** → must integrate (read their codebase + conventions)
- **Modern default** → Next.js + TypeScript + Tailwind CSS + shadcn/ui (greenfield, client neutral)
- **Custom modern** → specific framework per project need (Nuxt, Astro, SvelteKit, Vite, etc.)

> ⚠ **ห้ามใช้ Sellsuki DS 1.0 / DS 2.0** — DS เป็นของ Sellsuki internal product เท่านั้น (ใช้ skill `sellsuki-product-standard`)

Decision recorded ใน `project-card.md` Section 4. After Stage 1, **lock — ห้ามเปลี่ยน** (unless major escalation)

อ้าง `references/tech-stack-guide.md`

---

## Output

- `research-plan.md` ครบทุก section
- Milestone plan (เป็น artifact ที่ share ให้ลูกค้าได้)
- Tech stack locked
- Risk list (M/L only)
- Updated `project-card.md` (add Section 4-5)

---

## Gate to Stage 2

- [ ] Research foundation ครบ (domain, refs, user model)
- [ ] Milestone plan มี date + checkpoint
- [ ] Tech stack locked พร้อม rationale
- [ ] Client checkpoint #1 (variant pick) date confirmed กับ PM
- [ ] Brand assets ครบหรือ workaround agreed (e.g., "use neutral palette until brand kit arrives")

---

## Client checkpoint (optional ที่ Stage 1)

ส่งให้ PM forward ลูกค้า:

> ผมวาง plan ของ project พร้อมแล้ว มี milestone และจุดที่ขอ feedback ของคุณตามนี้:
> [milestone list]
>
> รบกวนเช็คว่า:
> 1. Date checkpoint สะดวก/ไม่สะดวก
> 2. ทีมที่จะ review อยู่ใครบ้าง
> 3. มี hard constraint อะไรที่ยังไม่ได้บอกไหม (เช่น ต้อง launch วันเฉพาะ)

จะ proactive ได้ — ลูกค้าเห็น process ตั้งแต่ต้น

---

## Common Mistakes

- ข้าม research เพราะ "เห็น brief แล้วเข้าใจ" → assumption ผิดเจอตอน UAT
- วาง plan ไม่มี buffer → 1 issue = timeline พัง
- Stack ไม่ lock → designer/dev เปลี่ยน mid-project → rework
- Client checkpoint ไม่ระบุ date → checkpoint เกิดช้า → blocker
- Research แค่ Google → ไม่ดู reference ลึกพอจะเห็น pattern

---

## Owner

| Role | Responsibility |
|---|---|
| Claude | Generate research, draft plan, propose stack |
| Level 1 Designer | Validate research, finalize plan, lock stack |
| Level 2 Lead | Approve plan for L/Enterprise |
| PM | Sync milestone กับ client expectation |
