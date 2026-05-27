---
name: sellsuki-product-standard
description: Sellsuki standard product/project workflow — Jira Card → Research → IA → Wireframe → AI Prototype → AI Usability Test → Refine → Vibe Code (DS 1.0/DS 2.0). ALWAYS trigger this skill the moment a Jira Card, Epic, or Story is shared, mentioned, or pasted (URL like *.atlassian.net/browse/XXX-123, key like PROJ-123, or phrases like "ได้ card มา", "PO ส่ง story มา", "เริ่มงาน card นี้", "design ตัวนี้ให้หน่อย", "ทำ feature ใหม่"). Also trigger when the user asks Claude to plan a design flow, build a wireframe from requirements, run AI usability tests, simulate user personas, or vibe-code an interface using Sellsuki Design System (DS1 / DS2). Do NOT skip this skill just because the request "looks small" — every card goes through this flow even if some stages are compressed. This skill orchestrates the full Card-to-Ship pipeline and auto-plans which stages to run based on card type (Product track vs Project track) and card size (S/M/L).
---

# Sellsuki Product Standard

> Standard workflow สำหรับทุก Card ที่ Designer/UXUI ของ Sellsuki ได้รับ — ตั้งแต่ Jira Card จนถึง Vibe Code ส่งเข้า production

---

## When this skill activates

Claude activates this skill **the moment a card or design task appears**. Signals to watch for:

| Signal | Example |
|---|---|
| Jira URL | `https://*.atlassian.net/browse/PROJ-123` |
| Jira key | `PROJ-123`, `SUKI-45`, `OC-2` |
| Phrase | "ได้ card มา", "PO ส่ง story", "เริ่มงาน X", "ทำ feature นี้" |
| Pasted content | Epic description, User Story, Acceptance Criteria |
| Intent | ขอ wireframe / prototype / usability test / vibe code |

If you see any of these, **start the flow** — don't ask "want me to use the standard?" Just say "ผมจะ run ตาม Sellsuki standard นะ" and begin Stage 0.

---

## The Flow (6 Stages)

```
┌──────────┐   ┌───────────┐   ┌────────┐   ┌─────────────┐   ┌────────┐   ┌────────────┐
│ 0.INTAKE │ ─▶│ 1.RESEARCH│ ─▶│ 2.DESIGN│ ─▶│ 3.AI USABILITY│ ─▶│ 4.REFINE│ ─▶│ 5.VIBE CODE│
│ Jira→AI  │   │ User      │   │ IA →    │   │ Persona AI  │   │ Final  │   │ DS1 / DS2  │
│ build    │   │ Journey   │   │ Wire →  │   │ runs flow   │   │ version│   │ via Claude │
│ Card     │   │ + IA prep │   │ Proto   │   │ → friction  │   │        │   │            │
└──────────┘   └───────────┘   └────────┘   └─────────────┘   └────────┘   └────────────┘
     │              │               │              │                │              │
     ▼              ▼               ▼              ▼                ▼              ▼
intake-     research-       design-spec.md    persona-test-     design-spec    code in
brief.md    journey.md      + wireframe       result.md         FINAL          repo +
                                                                                deviation log
                                                                                       │
                                                       (Product track) ◀──── loop ─────┘
```

Each stage has:
- **Input** — what must exist to start
- **Activities** — what Claude does (auto or with user)
- **Output** — file(s) produced
- **Gate** — must pass before next stage

Full stage docs: `workflow/stage-0-intake.md` through `workflow/stage-5-vibe-code.md`.

---

## How Claude runs the flow (automation level)

This skill is **AI-first**. Claude does as much as possible without waiting on the user. The default behavior:

1. **Parse the card** → extract title, description, acceptance criteria, attachments
2. **Classify** → Product track or Project track? S / M / L size? (see `references/card-classification.md`)
3. **Plan stages** → which stages run full, which compress, which skip (see decision matrix below)
4. **Summarize the plan** → 5-10 lines, show the user before executing
5. **Execute stage-by-stage** → produce file outputs in `/templates/`, await user confirmation only at named gates
6. **Hand off** → final spec + vibe-code-ready prompt for DS1 or DS2

The user can interrupt anytime with "skip", "deep-dive on X", or "redo stage N".

---

## Stage selection matrix

Not every card needs every stage in full. Claude picks depth automatically using this matrix:

| Card size | Stage 0 Intake | Stage 1 Research | Stage 2 Design | Stage 3 AI Usability | Stage 4 Refine | Stage 5 Vibe Code |
|---|---|---|---|---|---|---|
| **S** (bug fix, copy change, single field) | Quick parse | Skip — reuse existing journey | Wireframe only | Skip unless flow changed | Inline | Direct DS component swap |
| **M** (new flow, multi-screen feature) | Full parse | Journey + IA | Wire + Hi-fi Proto | 1-2 personas | 1 iteration | Full vibe code |
| **L** (new product area, multi-epic) | Full parse + Epic split | Full research + competitive | IA + Wire + Hi-fi Proto | 3+ personas | 2+ iterations | Vibe code per screen |

Track differences:

| | Product track | Project track |
|---|---|---|
| Loop | Stage 5 → back to Stage 0 (continuous) | Stage 5 → hard stop, post-launch report only |
| Gate strictness | Flexible — iterate fast | Strict — sign-off every stage |
| Usability test depth | Lighter, faster | Heavier, documented |

If Claude can't classify, **ask once** with a single quick question — don't stall.

---

## Default plan summary template

After parsing the card, Claude posts a short plan like this (always in Thai or matching user's language):

```
📋 Card: PROJ-123 — [title]
🏷  Type: Product track / M-size / Epic with 3 stories
🎯 Direction: [1 บรรทัด]

แผนการรัน:
  ✓ Stage 0 — parse แล้ว (intake-brief.md draft)
  → Stage 1 — Research: journey map + IA (ผมทำเอง 1-2 รอบ)
  → Stage 2 — Wireframe + Hi-fi prototype (Claude/Figma Make)
  → Stage 3 — AI Usability: persona A (power user), persona B (new user)
  → Stage 4 — Refine: 1 iteration ตาม friction findings
  → Stage 5 — Vibe code ด้วย DS2 (suggest จาก type)

⏱  รวมเวลาประมาณ: M-card ใช้ 3-7 วันถ้า run ปกติ — ตอนนี้ผมจะ run ต่อเลย
🛑 จุดที่ต้อง confirm: ก่อน Stage 3 (persona ที่จะใช้) และก่อน Stage 5 (DS1 vs DS2)
```

Then **proceed to Stage 0** unless the user interrupts.

---

## File map

```
sellsuki-product-standard/
├── SKILL.md                         (this file)
├── workflow/
│   ├── stage-0-intake.md            Parse Jira card, build intake brief
│   ├── stage-1-research.md          User journey, IA prep, persona signals
│   ├── stage-2-design.md            IA → wireframe → AI prototype
│   ├── stage-3-ai-usability.md      Persona AI runs the prototype
│   ├── stage-4-refine.md            Apply findings, finalize spec
│   └── stage-5-vibe-code.md         Generate DS1/DS2 code via Claude
├── templates/
│   ├── intake-brief.md              Output of Stage 0
│   ├── research-journey.md          Output of Stage 1
│   ├── ia-wireframe-spec.md         Output of Stage 2
│   ├── persona-ai-script.md         Persona prompts used in Stage 3
│   ├── persona-test-result.md       Output of Stage 3
│   ├── design-spec.md               Living spec, finalized in Stage 4
│   ├── vibe-code-prompt.md          Prompt template for Stage 5
│   └── design-retro.md              Post-launch (Product track)
├── rules/
│   ├── standard-team.md             Level 1 designer rules (executor)
│   └── standard-master.md           Level 2 lead rules (gatekeeper)
└── references/
    ├── card-classification.md       How to size S/M/L and pick track
    ├── ai-persona-library.md        Persona prompts: power user, new user, ...
    ├── ds-selection-guide.md        When DS1 vs DS2 — brand/use-case mapping
    └── jira-parsing.md              How Claude extracts info from Jira cards
```

---

## Quick rules Claude follows

These are non-negotiable across every stage:

1. **No design without intake-brief** — even S-cards need 5-line brief
2. **Every screen has 6 states** — default, loading, empty, error, success, disabled
3. **Tokens only** — no hardcoded colors/sizes; use Sellsuki DS tokens
4. **AI usability test is required for M and L cards** — at least 1 persona
5. **Vibe code only after design-spec.md is final** — never generate code from a wireframe alone
6. **DS selection is explicit** — Stage 5 must state "DS1" or "DS2" with reason
7. **Deviation log** — anything that diverges from spec during vibe-code is recorded
8. **Loop the team in async** — every stage output is shareable as-is

Full Level 1 rules: `rules/standard-team.md`. Level 2: `rules/standard-master.md`.

---

## When to read which reference

- **About to classify a card** → `references/card-classification.md`
- **Need to pick a persona for Stage 3** → `references/ai-persona-library.md`
- **Deciding DS1 vs DS2 at Stage 5** → `references/ds-selection-guide.md`
- **Card looks weird / missing fields** → `references/jira-parsing.md`

Always read the relevant `workflow/stage-N-*.md` **before executing that stage** — they contain stage-specific gates and example outputs.

---

## What to say when the skill kicks in

A good opener (don't copy verbatim, adapt to context):

> รับ card มาแล้ว ผมจะ run ตาม Sellsuki standard นะ — เริ่มจาก parse card ก่อน, แล้วจะวาง plan ทั้ง flow มาให้ดู ค่อยตัดสินใจว่า run ต่อเลยหรือปรับ.

Then move straight to Stage 0.
