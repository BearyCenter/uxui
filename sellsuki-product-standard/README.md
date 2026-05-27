# Sellsuki Product Standard

Standard workflow สำหรับทีม UXUI/Product Design ของ Sellsuki — Card-to-Ship flow ที่ AI-first และ orchestrate ผ่าน Claude

---

## ทำไมต้องมีมาตรฐานนี้

ทีมรับงานเป็น **Jira card** จาก PO/AI → ต้องวิ่ง flow ครบตั้งแต่ research จนถึง vibe code โดยใช้ Sellsuki Design System (DS 1.0 หรือ DS 2.0)

มาตรฐานเดิมเป็น generic 5-phase design flow — ไม่ตรงกับงานจริง, ไม่มี AI prototype/usability test, ไม่มี hook สำหรับ vibe code

มาตรฐานใหม่นี้:
- เริ่มจาก **Jira card** (trigger จริง)
- มี **AI Usability Test** เป็น stage แยก (มาตรฐาน persona library)
- จบที่ **Vibe Code DS1/DS2** ผ่าน Claude MCP
- Claude **เรียก skill เองอัตโนมัติ** เมื่อเจอ card — วาง plan, run flow, สรุปออกมา

---

## File map

```
sellsuki-product-standard/
├── SKILL.md                         ← entry point ของ Claude (โหลดอัตโนมัติเมื่อเจอ Jira card)
├── DESIGN.md                        ← เอกสารอธิบาย "ทำไม" skill ออกแบบมาแบบนี้
├── README.md                        ← ไฟล์นี้
│
├── workflow/                        ← 6 stages
│   ├── stage-0-intake.md            Parse Jira card, classify, plan
│   ├── stage-1-research.md          User journey, IA, persona signals
│   ├── stage-2-design.md            IA → Wireframe → AI Prototype
│   ├── stage-3-ai-usability.md      Persona AI runs the prototype
│   ├── stage-4-refine.md            Apply findings, finalize spec
│   └── stage-5-vibe-code.md         Generate DS1/DS2 code via Claude
│
├── templates/                       ← Output ของแต่ละ stage
│   ├── intake-brief.md              Stage 0 output
│   ├── research-journey.md          Stage 1 output
│   ├── ia-wireframe-spec.md         Stage 2 output
│   ├── persona-ai-script.md         Prompt template for Stage 3
│   ├── persona-test-result.md       Stage 3 output (one per persona)
│   ├── design-spec.md               Living spec, final at Stage 4
│   ├── vibe-code-prompt.md          Prompt for Stage 5
│   └── design-retro.md              Post-launch (Product track)
│
├── rules/                           ← Quality gates
│   ├── standard-team.md             Level 1 designer rules
│   └── standard-master.md           Level 2 lead rules
│
└── references/                      ← Decision support
    ├── card-classification.md       S/M/L sizing + Product/Project track
    ├── ai-persona-library.md        4 baseline personas + customization guide
    ├── ds-selection-guide.md        DS 1.0 vs DS 2.0 decision tree
    └── jira-parsing.md              How Claude extracts info from Jira
```

---

## Flow ที่ Claude run อัตโนมัติ

```
[Jira Card] → Stage 0 Intake → Stage 1 Research → Stage 2 Design → Stage 3 AI Usability → Stage 4 Refine → Stage 5 Vibe Code (DS1/DS2)
                                                                                                                    │
                                                                            ┌── (Product track: loop back) ─────────┘
                                                                            └── (Project track: hard stop)
```

แต่ละ stage มี:
- **Trigger** — เริ่มเมื่อไหร่
- **Input** — ต้องมีอะไรก่อน
- **Activities** — Claude ทำอะไร / กับ user
- **Output** — ไฟล์ที่ผลิต
- **Gate** — ต้องผ่านก่อนไป stage ถัดไป

---

## วิธีเริ่มใช้

### สำหรับ Designer

1. **พูดถึง Jira card** ใน chat กับ Claude — paste URL, key, หรือ content
   - ตัวอย่าง: "ช่วยทำ SUKI-234 ให้หน่อย"
   - หรือ: "PO ส่งมา https://sellsuki.atlassian.net/browse/SUKI-234"
2. Claude จะ **auto-trigger skill นี้** และเริ่ม Stage 0
3. Claude **post plan summary** ให้ดู — review/adjust ตามต้องการ
4. Claude **run flow** ทีละ stage — confirm ที่จุดสำคัญ (ก่อน Stage 3, ก่อน Stage 5)

### สำหรับ Lead

1. Review skill output ที่ Stage 4 (L-card) และ Stage 5 (major deviation)
2. Maintain `references/ai-persona-library.md` — quarterly review
3. Maintain `references/ds-selection-guide.md` — update when DS evolves
4. Update SKILL.md/DESIGN.md เมื่อ workflow ของทีมเปลี่ยน

---

## เกี่ยวกับการ "เรียก skill อัตโนมัติ"

Claude (ในระบบที่รองรับ skill) จะ **auto-trigger** มาตรฐานนี้เมื่อ:
- เห็น Jira URL หรือ key
- ผู้ใช้พูดถึง card, ticket, story, epic
- ผู้ใช้ขอ wireframe / prototype / usability test / vibe code

ไม่ต้องสั่ง "ใช้ standard นี้" ทุกครั้ง — มันจะ kick in เอง

---

## Backwards compatibility note

ของเดิม (`workflow/phase-*.md`, `templates/problem-brief.md`, etc.) ถูก **แทนที่ทั้งหมด** ด้วยมาตรฐานใหม่ — ดู `DESIGN.md` Section 10 สำหรับ mapping ระหว่างเก่า/ใหม่

---

## Iteration

มาตรฐานนี้เป็น **v1.0** — คาดว่าจะปรับ:
- Quarterly: persona library, DS selection guide
- Per release: stage activities ตามที่ทีมเรียนรู้
- Major: เมื่อ workflow ของทีมเปลี่ยน หรือ DS major version

Track changes ใน DESIGN.md
