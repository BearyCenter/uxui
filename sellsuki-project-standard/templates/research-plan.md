# Research & Plan

> Output ของ Stage 1 — foundation ที่ Stage 2 และทั้ง project ใช้

---

## Meta

**Project:** `[name]`
**Date:** `YYYY-MM-DD`
**Designer:** `[name]`

---

## Section 1 — Domain Research

**Industry / domain:** `[ลูกค้าอยู่ในวงการอะไร]`

**Domain norms:**
- `[pattern ที่เป็น standard ของ industry นี้]`
- `[expectation ของ user ทั่วไป]`

**Common UI patterns:**
- `[pattern 1 — e.g., "dashboard with KPI cards"]`
- `[pattern 2 — e.g., "filter + table + bulk actions"]`

---

## Section 2 — Reference Scan

| # | Reference site | URL | What we like | What we'd change |
|---|---|---|---|---|
| 1 | | | | |
| 2 | | | | |
| 3 | | | | |

**Synthesis:**
`[1-2 paragraphs — direction inspired by refs but not copying]`

---

## Section 3 — User Mental Model

**Primary user:**
- Role: `[...]`
- Frequency of use: `[daily / weekly / occasional]`
- Tech savvy: `[low / medium / high]`
- Device: `[primary device, context]`

**User's mental model:**
`[user คิดว่า product นี้คือ "X" — สำคัญที่จะ design ให้ตรงกับสิ่งที่ user mapping ในหัว]`

**Top tasks:**
1. `[task 1 — what they need to do]`
2. `[task 2]`
3. `[task 3]`

**Frustrations to avoid:**
- `[จาก domain knowledge — common gripes]`

---

## Section 4 — Brand Assimilation

**Brand assets received:**
- [ ] Logo (vector / raster)
- [ ] Color palette
- [ ] Font family
- [ ] Voice / tone guide
- [ ] Other: `[...]`

**Style tokens extracted:**
| Token | Value |
|---|---|
| Primary color | `#...` |
| Secondary color | `#...` |
| Accent color | `#...` |
| Heading font | `[font]` |
| Body font | `[font]` |
| Border radius | `[N px]` |

**Brand voice:**
`[formal / friendly / playful / professional / ...]`

**If brand assets incomplete:**
`[workaround — e.g., "use neutral palette with placeholder color tokens until brand kit arrives Day 4"]`

---

## Section 5 — Tech Feasibility (M/L only)

**API readiness:**
- [ ] Existing API documented
- [ ] API being built in parallel
- [ ] No API yet — use mock
- [ ] Unknown — risk

**Integration points:**
- `[external service, SSO, payment gateway, ...]`

**Performance considerations:**
- Expected concurrent users: `[N]`
- Data volume: `[item count / record size]`

**Browser / device support claim:**
- `[e.g., "modern browsers + iOS 14+ + Android 10+"]`

---

## Section 6 — Tech Stack (locked here)

**Choice:** `Client's existing stack / Modern default (Next.js + TS + Tailwind + shadcn) / Custom modern`

**Rationale:**
`[1 paragraph — why this stack, why not the alternatives — อ้าง references/tech-stack-guide.md]`

**Stack details:**
- Framework: `[e.g., Next.js 14 App Router]`
- Language: `[TypeScript / JavaScript]`
- Styling: `[Tailwind / CSS modules / other]`
- Component library: `[shadcn/ui / client's lib / Headless UI / other]`
- Forms: `[react-hook-form + Zod / other]`
- State: `[useState / Zustand / Redux / other]`
- Data fetching: `[TanStack Query / native fetch / SWR / other]`

> ⚠ ห้ามใช้ Sellsuki DS 1.0 / DS 2.0 ใน project track — ใช้ใน `sellsuki-product-standard` skill เท่านั้น

**Build tool:**
`[Next.js / Vite / Nuxt / Astro / other]`

---

## Section 7 — Milestone Plan

```
Week 1
  Day 1: ✓ Stage 0 — PM Card
  Day 2-3: → Stage 1 — Research & Plan (this doc)
  Day 4-6: Stage 2 — Vibe Design (2 variants)
  → Client checkpoint #1: variant pick (end of Day 6)

Week 2
  Day 7-10: Stage 3 — Vibe Code
  Day 11: Stage 4 — Deploy staging
  Day 12-13: Stage 5 — UAT round 1
  Day 14-15: Stage 5 — Improve

Week 3
  Day 16: UAT round 2
  Day 17: Final fixes
  Day 18: Stage 6 — Handoff
  → Client checkpoint #2: sign-off
```

**Buffer:** 2 days reserved

---

## Section 8 — Risks & Mitigations (M/L)

| # | Risk | Mitigation |
|---|---|---|
| 1 | Brand kit ส่งช้า | Start Stage 2 with neutral tokens, swap in Stage 3 |
| 2 | API ไม่พร้อม | Mock data layer in Stage 3, swap before Stage 4 |
| 3 | Client decision-maker on leave during UAT | PM confirm availability before Stage 5 |
| 4 | | |

---

## Section 9 — Open Questions (rolled forward from Stage 0)

`[update status here]`

---

## Gate to Stage 2

- [ ] Domain understood, references scanned
- [ ] User model documented
- [ ] Brand assets extracted (or workaround agreed)
- [ ] Stack locked + rationale
- [ ] Milestone plan with dates + checkpoints
- [ ] Risks identified (M/L) + mitigation noted
- [ ] No blocking open question
