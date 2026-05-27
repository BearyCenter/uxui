# Project Card

> Output ของ Stage 0 — structured version ของ raw PM brief

---

## Section 1 — Project Identity

**Project name:** `[ชื่อ project]`
**Client:** `[ชื่อบริษัท / ลูกค้า]`
**PM:** `[ชื่อ PM]`
**Designer (lead):** `[ชื่อ]`
**Date received:** `YYYY-MM-DD`
**Brief source:** `email / Slack / meeting / Word doc / voice note`

---

## Section 2 — Tier & Classification

**Project tier:**
- [ ] S — landing page / single screen / < 1 week
- [ ] M — multi-screen / 1-3 weeks
- [ ] L — multi-module / 1-3 months
- [ ] Enterprise — large scope / 3+ months / multiple teams

**Tier rationale:**
`[1-2 บรรทัด — อ้าง signals จาก references/project-sizing.md]`

**Client relationship:**
- [ ] First-time client
- [ ] Returning client (ครั้งที่ N)
- [ ] Long-term retainer

**Urgency:**
- [ ] Hard deadline: `YYYY-MM-DD` (reason: `[...]`)
- [ ] Soft deadline / flexible
- [ ] No deadline (timeline TBD)

---

## Section 3 — Objective & Deliverable

**Client's objective (in their words):**
> `[paste / summarize what client said]`

**Translated objective (1 line):**
`[Designer's interpretation, agreed with PM]`

**End users:**
`[ใครใช้ — describe role, frequency, context]`

**Deliverable list (in scope):**
- [ ] Design system mapping / brand alignment
- [ ] [Screen 1]
- [ ] [Screen 2]
- [ ] [...]
- [ ] Code repo + README
- [ ] Staging deploy
- [ ] Handoff doc

**Out of scope (explicit):**
- `[item]`
- `[item]`

---

## Section 4 — Tech Stack (locked at Stage 1)

**Stack choice:**
- [ ] **Client's existing stack** — must integrate with their codebase
  - Describe: `[framework + component library + key dependencies]`
  - Repo / docs reference: `[link]`
- [ ] **Modern default** (greenfield, client neutral): Next.js + TypeScript + Tailwind CSS + shadcn/ui
- [ ] **Custom modern stack** (specific project need):
  - Framework: `[Next.js / Nuxt / Astro / Vite / SvelteKit / etc.]`
  - Language: `[TypeScript / JavaScript]`
  - Styling: `[Tailwind / CSS Modules / styled-components / other]`
  - Component primitives: `[shadcn/ui / Radix / Headless UI / PrimeVue / other]`
  - Other key deps: `[forms, state, data fetching, etc.]`

> ⚠ **ห้ามใช้ Sellsuki DS 1.0 / DS 2.0** ใน project track — DS เป็นของ Sellsuki internal product เท่านั้น (ใช้ skill `sellsuki-product-standard`)

**Rationale:**
`[1-2 บรรทัด — อ้าง references/tech-stack-guide.md]`

**Deploy target:**
- [ ] Vercel (default)
- [ ] Netlify
- [ ] Sellsuki cloud
- [ ] Client infrastructure
- [ ] Other: `[describe]`

---

## Section 5 — Milestone (filled at Stage 1)

**Total estimated timeline:** `[N days/weeks]`

| Stage | Day(s) | Deliverable | Client checkpoint? |
|---|---|---|---|
| 0 Brief Intake | Day 1 | PM Card | — |
| 1 Research & Plan | Day 2-3 | research-plan + milestone | optional |
| 2 Vibe Design | Day 4-6 | 2 variants | ✓ variant pick |
| 3 Vibe Code | Day 7-10 | working code | — |
| 4 Deploy | Day 11 | staging URL | — |
| 5 Test & Improve | Day 12-17 | iterated build | ✓ UAT round 1, ✓ UAT round 2 |
| 6 Handoff | Day 18 | handoff package | ✓ sign-off |

**Buffer:** `[N days for unforeseen]`

---

## Section 6 — UAT Round Budget

**Budgeted rounds:** `1 (S) / 2 (M) / 3 (L) — adjustable`

| Round | Status | Date | Findings (B/I/CR/OOS) |
|---|---|---|---|
| 1 | not started / in progress / done | | bug / improve / change request / out of scope |
| 2 | | | |

**Overage policy:** Round N+1 triggers scope conversation with PM

---

## Section 7 — Open Questions

> ที่ต้องถาม PM/client ก่อนหรือระหว่าง flow

| # | Question | Owner | Asked by | Status |
|---|---|---|---|---|
| 1 | | PM / Client | YYYY-MM-DD | open / answered |
| 2 | | | | |

---

## Section 8 — Risks (M/L only)

| # | Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|---|
| 1 | | low / med / high | low / med / high | |

---

## Section 9 — Links

- Brief source (original): `[link]`
- Research plan: `[file path]`
- Design spec: `[file path]`
- Code repo: `[URL]`
- Staging URL: `[URL]`
- Handoff doc: `[file path]`
- Slack/Notion channel: `[link]`

---

## Status

- [ ] Stage 0 — Brief Intake
- [ ] Stage 1 — Research & Plan
- [ ] Stage 2 — Vibe Design
- [ ] Stage 3 — Vibe Code
- [ ] Stage 4 — Deploy
- [ ] Stage 5 — Test & Improve
- [ ] Stage 6 — Handoff
- [ ] Closed
- [ ] Blocked — reason: `[...]`

**Last updated:** `YYYY-MM-DD HH:MM`
