---
name: sellsuki-project-standard
description: Sellsuki standard workflow for PROJECT track (client work, agency-style delivery) — Client Brief → PM Card → Research+Plan → Vibe Design → Vibe Code → Deploy → Test & Improve → Handoff. ALWAYS trigger this skill when a PM forwards a client brief or requirement, when phrases like "ลูกค้าส่งมา", "PM ส่ง brief", "เริ่ม project ใหม่", "client requirement", "วาง plan ให้ลูกค้า", "deploy ให้ดู", "ส่งงานลูกค้า", or "handoff" appear, or when a client/project name (non-Sellsuki internal) is mentioned with delivery intent. Also trigger for vibe design, vibe code, staging deploy, client UAT, or design handoff requests in a non-internal context. Do NOT confuse with sellsuki-product-standard (internal product work via Jira) — Project work comes from external clients via PM, not from internal PO via Jira. This skill orchestrates the full Client-Brief-to-Handoff pipeline with explicit deploy and handoff stages, and leaves hooks for future Backend and QA phases (currently out of scope, design team hands off after final improve).
---

# Sellsuki Project Standard

> Standard workflow สำหรับทีม Project (client work) ของ Sellsuki — ตั้งแต่ PM brief จากลูกค้าจนถึง handoff

---

## When this skill activates

Trigger ทันทีเมื่อเจอ signal เหล่านี้:

| Signal | Example |
|---|---|
| PM forwards brief | "PM ส่ง brief มา", "PM ส่ง requirement มา" |
| Client mention | "ลูกค้า X ส่งมา", "client Y อยาก..." |
| Project intent | "เริ่ม project ใหม่", "ทำ landing ให้ลูกค้า" |
| Delivery phase | "deploy ให้ดู", "ส่งงานให้ลูกค้า", "handoff" |
| Vibe workflow | "vibe design ตัวนี้", "vibe code ตัวนี้" |
| External requirement source | Email/Slack/meeting note paste, not Jira card |

**Important — when NOT to use this skill:**
- ถ้า card มาจาก Jira (`*.atlassian.net/browse/XXX-NNN`) → ใช้ `sellsuki-product-standard` แทน
- ถ้าเป็น internal Sellsuki product work → ใช้ `sellsuki-product-standard`

Project skill นี้สำหรับ **client work** เท่านั้น (agency-style, deliverable-focused, จบที่ handoff)

---

## The Flow (7 stages)

```
┌──────────┐   ┌───────────┐   ┌──────────┐   ┌──────────┐   ┌────────┐   ┌─────────────┐   ┌─────────┐
│ 0.BRIEF  │ ─▶│ 1.RESEARCH│ ─▶│ 2.VIBE   │ ─▶│ 3.VIBE   │ ─▶│4.DEPLOY│ ─▶│ 5.TEST &    │ ─▶│ 6.HAND  │
│ INTAKE   │   │  & PLAN   │   │  DESIGN  │   │  CODE    │   │ stage  │   │   IMPROVE   │   │  OFF    │
│ PM Card  │   │ with AI   │   │  via AI  │   │ via AI   │   │ URL    │   │ UAT + fix   │   │ docs    │
└──────────┘   └───────────┘   └──────────┘   └──────────┘   └────────┘   └─────────────┘   └─────────┘
                                                                                                  │
                                                                       ┌── (future) BE Phase ────┤
                                                                       └── (future) QA Phase ────┘
```

Each stage has Input → Activities → Output → Gate. Full docs: `workflow/stage-0-*.md` through `workflow/stage-6-*.md`.

---

## How Claude runs the flow

1. **Receive PM brief** — Word/Slack/meeting note/voice note transcript/email forward
2. **Build PM Card** — structure raw brief into `project-card.md`
3. **Classify** — client tier (S/M/Enterprise), urgency, tech-stack target
4. **Plan stages** — milestone + timeline + checkpoint with client
5. **Post plan summary** in chat — 8-12 lines
6. **Execute stage-by-stage** — confirm at named gates (before deploy, before handoff)
7. **Deliver handoff package** — final stage

User can interrupt with "skip", "deep-dive on N", "redo N", "client wants change at stage N".

---

## Project vs Product — key differences

| Aspect | Product (`sellsuki-product-standard`) | Project (this skill) |
|---|---|---|
| Source of work | Internal PO via Jira | External client via PM |
| Trigger | Jira card | PM brief (unstructured) |
| Iteration model | Loop forever (Stage 5 → 0) | Linear with hard stop at handoff |
| Stakeholder gates | Internal lead approve | Client UAT + sign-off |
| Tech stack | Sellsuki DS1/DS2 mandatory | DS1/DS2 *or* client's stack |
| End state | Live in production, measured | Deployed, signed off, handed off |
| AI Usability | Required (M/L card) | Optional — client UAT replaces it |
| Deploy stage | Implicit (in vibe code) | Explicit (Stage 4) |
| Handoff | To Sellsuki team | To client OR future internal BE/QA |

---

## Stage selection matrix

| Project size | Stage 0 | Stage 1 | Stage 2 | Stage 3 | Stage 4 | Stage 5 | Stage 6 |
|---|---|---|---|---|---|---|---|
| **S** (landing page, single screen, <1 wk) | Quick PM card | Light desk research | Direct vibe — 1 variant | Direct vibe code | Single deploy | Light UAT, 1 round | Lean handoff doc |
| **M** (multi-screen, 1-3 wks) | Full PM card | Research + milestone plan | Vibe — 2 variants client picks | Component-by-component | Deploy + access | UAT + 2 round improve | Full handoff package |
| **L / Enterprise** (multi-module, 1-3 mo) | Full PM card + epic split | Full research + tech feasibility | Multi-iteration | Full vibe code | Staging + prod | Multiple UAT cycles | Comprehensive handoff + BE/QA prep |

---

## Default plan summary template

After parsing the brief, Claude posts:

```
📋 Project: [client] — [project name]
🏷  Tier: M-size / 2 weeks / Client UAT every 3 days
🛠  Stack: React + DS 2.0 (patona) — to be confirmed at Stage 1
🎯 Objective: [1 บรรทัด]

แผนการรัน:
  ✓ Stage 0 — PM Card built (project-card.md)
  → Stage 1 — Research & Plan: domain scan, user model, milestone (1 day)
  → Stage 2 — Vibe Design: 2 hi-fi variants for client to pick (2 days)
  → Stage 3 — Vibe Code: build picked variant (3 days)
  → Stage 4 — Deploy to staging: shareable URL
  → Stage 5 — Test & Improve: smoke test + client UAT (2 rounds budget)
  → Stage 6 — Handoff: design doc + code repo + access transfer

🗓 Milestone:
  Week 1: Stage 0-2 → client review variant
  Week 2: Stage 3-5 → UAT + improve
  End of Week 2: Stage 6 handoff

🛑 Client checkpoints (Claude wait):
  - After Stage 2 (variant pick)
  - After Stage 5 (UAT sign-off)

🚀 ผม run ต่อเลยนะ ถ้าอยากปรับ plan บอกได้
```

Then **proceed to Stage 0**.

---

## File map

```
sellsuki-project-standard/
├── SKILL.md                         (this file)
├── workflow/
│   ├── stage-0-brief-intake.md      Parse PM brief → project card
│   ├── stage-1-research-plan.md     Research + milestone plan with AI
│   ├── stage-2-vibe-design.md       AI-driven hi-fi design (2+ variants)
│   ├── stage-3-vibe-code.md         Code via Claude + DS/client stack
│   ├── stage-4-deploy.md            Staging deploy, access setup
│   ├── stage-5-test-improve.md      Smoke test + client UAT loop
│   └── stage-6-handoff.md           Handoff doc + sign-off + future hooks
├── templates/
│   ├── project-card.md              Output of Stage 0
│   ├── research-plan.md             Output of Stage 1
│   ├── vibe-design-spec.md          Output of Stage 2
│   ├── vibe-code-prompt.md          Prompt template for Stage 3
│   ├── deploy-checklist.md          Stage 4 checklist
│   ├── test-report.md               Stage 5 output (one per UAT cycle)
│   ├── improvement-log.md           Stage 5 bug/change tracker
│   ├── handoff-doc.md               Stage 6 — final deliverable
│   └── design-retro.md              Post-handoff retro (internal)
├── rules/
│   ├── standard-team.md             Level 1 project designer rules
│   └── standard-master.md           Level 2 project lead rules
└── references/
    ├── client-brief-parsing.md      Extract requirements from messy PM brief
    ├── project-sizing.md            S/M/L/Enterprise classification
    ├── tech-stack-guide.md          DS1/DS2 vs client stack decision
    ├── client-comm-templates.md     How to ask client at checkpoints
    └── handoff-extension-plan.md    Future BE/QA phase hooks
```

---

## Quick rules Claude follows

Non-negotiable across stages:

1. **No design without PM Card** — even rush S-projects need 10-line card
2. **Client checkpoints are hard gates** — never proceed past Stage 2 variant or Stage 5 UAT without explicit OK
3. **Variant thinking** — Stage 2 produces 2+ options for client to pick (not 1 "correct" answer)
4. **Deploy on staging first** — never deploy to client's prod without staging round
5. **Improvement budget is finite** — set UAT round limit upfront; overage triggers scope conversation
6. **Handoff is shippable** — design doc + code + access in one bundle, client can act on it without follow-up
7. **Future BE/QA hooks must be present** — handoff doc has placeholder sections so future phases plug in
8. **Track stack consistency** — pick DS1/DS2/client-stack at Stage 1 and lock it; don't mix during the project

Full Level 1 rules: `rules/standard-team.md`. Level 2: `rules/standard-master.md`.

---

## When to read which reference

- **Parsing messy PM brief** → `references/client-brief-parsing.md`
- **Sizing the project** → `references/project-sizing.md`
- **Stack decision (DS vs client's own)** → `references/tech-stack-guide.md`
- **Drafting client checkpoint message** → `references/client-comm-templates.md`
- **Building handoff that BE/QA can pick up later** → `references/handoff-extension-plan.md`

Always read the relevant `workflow/stage-N-*.md` **before executing that stage** — gates and example outputs are stage-specific.

---

## What to say when the skill kicks in

A good opener:

> รับ brief จาก PM แล้ว ผมจะ run ตาม Sellsuki project standard นะ — เริ่มจากสร้าง PM Card ก่อน แล้วจะวาง plan ทั้ง flow + milestone ให้ดู ค่อยตัดสินใจ run ต่อหรือปรับ

Then move straight to Stage 0.

---

## Note on BE/QA phases (future)

Workflow ปัจจุบันจบที่ **Stage 6 Handoff** — ทีม design ส่งงานต่อให้ client หรือทีมที่จะ maintain

**Planned future phases** (ยังไม่ใน scope):
- Phase 7 — Backend (when Sellsuki BE team integrated)
- Phase 8 — QA (when QA team integrated)

Handoff doc (Stage 6) **ออกแบบให้ extension ได้** — มี section placeholder สำหรับ BE/QA pickup เมื่อ phase เหล่านั้น online

ดู `references/handoff-extension-plan.md` สำหรับ detail
