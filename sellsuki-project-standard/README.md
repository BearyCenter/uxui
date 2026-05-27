# Sellsuki Project Standard

Standard workflow สำหรับทีม **Project** (client work) ของ Sellsuki — Brief-to-Handoff pipeline, AI-first, ออกแบบให้ extension-ready สำหรับ future BE/QA phase

---

## ทำไมแยกจาก product standard

| | `sellsuki-product-standard` | `sellsuki-project-standard` (this) |
|---|---|---|
| Source | Jira card จาก PO/AI build | PM brief (Word/Slack/voice/email) |
| Iteration | Loop — Stage 5 → 0 | Linear — จบที่ Stage 6 Handoff |
| Stakeholder | Internal lead | External client + PM |
| Variant thinking | 1 solution | 2+ variants client picks |
| Deploy | Implicit ใน vibe code | Explicit Stage 4 |
| Stack | DS1/DS2 mandatory | DS1/DS2 หรือ client stack |
| AI Usability | Required (M/L) | Optional — client UAT แทน |
| End state | Live in production, measured | Signed off, handed off |
| Future hooks | n/a | Section F สำหรับ Phase 7/8 |

---

## File map

```
sellsuki-project-standard/
├── SKILL.md                         ← entry point ของ Claude (โหลดอัตโนมัติเมื่อเจอ PM brief)
├── DESIGN.md                        ← เอกสารอธิบาย "ทำไม" skill ออกแบบมาแบบนี้
├── README.md                        ← ไฟล์นี้
│
├── workflow/                        ← 7 stages
│   ├── stage-0-brief-intake.md      Parse PM brief → project card
│   ├── stage-1-research-plan.md     Research + milestone + stack lock
│   ├── stage-2-vibe-design.md       AI-driven hi-fi 2+ variants
│   ├── stage-3-vibe-code.md         Code via Claude + DS/client stack
│   ├── stage-4-deploy.md            Staging deploy + access setup
│   ├── stage-5-test-improve.md      Smoke + UAT loop (round budget)
│   └── stage-6-handoff.md           Final delivery + Section F hooks
│
├── templates/                       ← Output ของแต่ละ stage
│   ├── project-card.md              Stage 0 output (structured from raw brief)
│   ├── research-plan.md             Stage 1 output (research + milestone)
│   ├── vibe-design-spec.md          Stage 2 output (variants + picked)
│   ├── vibe-code-prompt.md          Prompt template for Stage 3
│   ├── deploy-checklist.md          Stage 4 checklist
│   ├── test-report.md               Stage 5 — one per UAT round
│   ├── improvement-log.md           Stage 5 — cumulative finding tracker
│   ├── handoff-doc.md               Stage 6 — comprehensive final deliverable (with Section F)
│   └── design-retro.md              Internal post-project retro
│
├── rules/                           ← Quality gates
│   ├── standard-team.md             Level 1 designer rules
│   └── standard-master.md           Level 2 lead rules (incl. future phase governance)
│
└── references/                      ← Decision support
    ├── client-brief-parsing.md      Extract requirements from messy PM brief
    ├── project-sizing.md            S/M/L/Enterprise classification
    ├── tech-stack-guide.md          DS1/DS2/client stack decision tree
    ├── client-comm-templates.md     Checkpoint messages (Thai + English)
    └── handoff-extension-plan.md    Phase 7 BE + Phase 8 QA future plan
```

---

## Flow ที่ Claude run อัตโนมัติ

```
[PM Brief] → Stage 0 Brief Intake → Stage 1 Research & Plan → Stage 2 Vibe Design (2+ variants) 
            → Stage 3 Vibe Code → Stage 4 Deploy → Stage 5 Test & Improve → Stage 6 Handoff
                                                                                  │
                                                          (future) BE Phase  ─────┤
                                                          (future) QA Phase  ─────┘
```

Each stage has Input → Activities → Output → Gate. **Client checkpoints** เป็น hard gates:
- หลัง Stage 2: variant pick
- หลัง Stage 4: UAT round 1 invitation
- หลัง Stage 5: sign-off
- หลัง Stage 6: receiver acknowledgment

---

## วิธีเริ่มใช้

### สำหรับ Designer

1. **PM ส่ง brief มา** ใน chat — Slack paste, email forward, doc link, voice note transcript
   - ตัวอย่าง: "PM ส่ง brief ลูกค้ามาให้แล้ว: [paste]"
   - หรือ: "ลูกค้า Acme อยากได้ B2B portal — 4 screens, deadline 3 weeks"
2. Claude **auto-trigger** skill นี้ → start Stage 0
3. Claude **build project-card.md** + plan milestone
4. Claude **post plan** ให้ดู — adjust ตามต้องการ
5. Claude **run flow** ทีละ stage — confirm ที่ client checkpoints

### สำหรับ Lead

1. Review project brief ก่อน Stage 1 (โดยเฉพาะ Enterprise)
2. Review Stage 2 variants ก่อน client เห็น (L/Enterprise)
3. Approve scope change (Stage 5)
4. Audit Section F (Stage 6 handoff) — ต้อง future-phase-ready
5. Run quarterly retro on portfolio — update skill/templates

---

## ลักษณะเด่น

### 1. Variant thinking ที่ Stage 2

แตกต่างจาก product flow — Project ต้องสร้าง **2+ defendable variants** ให้ client เลือก ไม่ใช่ iterate 1 solution
- 2 variants สำหรับ S/M
- 2-3 variants สำหรับ L/Enterprise
- ไม่มี "weak option" — ทุก variant ต้อง stand on its own

### 2. UAT round budget

จำกัด round จากต้น project — เกินจะ trigger **scope conversation**:
- S = 1 round
- M = 2 rounds
- L = 3 rounds

ทำให้ project มี end state ชัดเจน, ไม่ลาก

### 3. Section F — Future Phase Hooks

Handoff doc มี **Section F1 (Backend pickup)** และ **Section F2 (QA pickup)** ที่:
- Document mock data swap points
- Document API contracts expected
- Document test scenarios + browser/device matrix
- Document accessibility + performance baseline

ทำให้ future Sellsuki BE/QA team plug in ได้โดยไม่ต้องเริ่มจาก reverse engineering

### 4. Stack flexibility

Project ใช้ stack ของลูกค้าได้ (ไม่บังคับ DS) — ดู `references/tech-stack-guide.md` สำหรับ decision tree

### 5. Client comm templates

มี template ภาษาไทย + อังกฤษสำหรับทุก checkpoint — designer ไม่ต้องเขียนข้อความใหม่ทุกครั้ง

---

## เมื่อไหร่ Claude เรียก skill นี้ (vs product skill)

| Signal | Skill |
|---|---|
| Jira URL / key | → product skill |
| PM brief, client name, "ลูกค้าส่งมา" | → project skill (this) |
| "deploy ให้ดู", "handoff", "ส่งงานลูกค้า" | → project skill |
| Ambiguous: "design ตัวนี้" | → ถามว่า "มาจาก Jira หรือ PM brief?" |

---

## Iteration

มาตรฐานนี้เป็น **v1.0** — คาดว่าจะปรับ:
- Per project retro → template / reference updates
- Quarterly → persona library (client end-user version), tech stack guide
- Major → เมื่อ Phase 7 (Backend) หรือ Phase 8 (QA) launch → skill version 2.0/3.0

Track ใน `DESIGN.md`

---

## Cross-reference กับ product skill

- ทั้ง 2 skills coexist — Claude เลือกตาม trigger
- Persona library ต่างกัน (project = client's end-user, product = Sellsuki merchant)
- DS guide ต่างกัน (project มี option client stack)
- Workflow logic แยก — แต่ rules quality ใกล้กัน

ไม่ shared file — เพื่อให้แต่ละ skill self-contained, evolve อิสระ
