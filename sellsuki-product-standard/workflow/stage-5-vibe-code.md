# Stage 5 — Vibe Code

**Position:** `Refine → VIBE CODE → (Product loop / Project stop)`

---

## Purpose

แปลง final design-spec → working code ที่ใช้ Sellsuki Design System (DS1 หรือ DS2) — Claude เป็นคน code, designer เป็นคน direct

---

## Trigger

- Stage 4 ผ่าน gate — spec final, DS เลือกแล้ว, user confirm แล้ว

---

## Input

- `design-spec.md` (final)
- DS choice: DS1 หรือ DS2 + brand variant
- Repo / file location ที่จะ implement
- `templates/vibe-code-prompt.md` — prompt template

---

## How vibe code works

Vibe code ในที่นี้ = **Claude code follow spec** — designer ให้ direction, Claude เขียน, designer review

### Tool stack

| Where | Tool |
|---|---|
| In IDE / repo | Claude Code (CLI) — สำหรับ implement ใน codebase จริง |
| In chat / artifact | Claude.ai HTML artifact — สำหรับ demo / Storybook story |
| Design system MCP | Use `Sellsuki Design System` MCP (DS1) หรือ `Sellsuki Design System3` MCP (DS2) — Claude เรียก component spec ได้เลย |

### The vibe-code loop

1. **Prep prompt** — fill `templates/vibe-code-prompt.md` ด้วย spec + DS choice + scope
2. **Generate v1** — Claude code ออกมาเป็น working state
3. **Visual QA** — เปรียบกับ wireframe/prototype จาก Stage 4
4. **Behavior QA** — เดิน happy path + edge case
5. **DS audit** — ตรวจว่าใช้ token เท่านั้น, ไม่ hardcode
6. **Iterate** — ถ้าเจอ deviation → log แล้ว fix
7. **Final review** — designer approve, dev review (ถ้าทีมมี dev อื่น)

---

## DS-specific guidance

### DS 1.0 (legacy)
- **MCP:** `Sellsuki Design System`
- **Stack:** React + Sellsuki DS components
- **When to use:** existing product ที่ยังไม่ migrate, page ที่อยู่ใน module เดิม
- **Key MCP tools (deferred — load via tool_search):**
  - `Sellsuki Design System:list_components` — ดู component ทั้งหมด
  - `Sellsuki Design System:get_component` — รายละเอียด component
  - `Sellsuki Design System:get_feature_template` — page template + API hook + state pattern
  - `Sellsuki Design System:generate_page_layout` — scaffold ทั้ง page
  - `Sellsuki Design System:get_brand_rules` — DO/DON'T

### DS 2.0 (current)
- **MCP:** `Sellsuki Design System3`
- **Stack:** ssk-* Lit Web Components — works in React, Vue, Vanilla
- **When to use:** new product, new module, anything that should follow current standard
- **Brand variants:** patona, ccs3, oc2plus
- **Key MCP tools (deferred — load via tool_search):**
  - `Sellsuki Design System3:list_components` — ssk-* component list
  - `Sellsuki Design System3:get_component` — detailed spec
  - `Sellsuki Design System3:generate_page_layout` — boilerplate (dashboard, list, detail, settings, landing)
  - `Sellsuki Design System3:generate_form` — form scaffold
  - `Sellsuki Design System3:get_brand_rules` — guideline + use case ต่อ brand
  - `Sellsuki Design System3:validate_usage` — ตรวจ HTML/JSX ว่าใช้ ssk-* ถูกไหม

> Always call the MCP `get_brand_rules` ก่อนเขียน code — ถ้าไม่รู้ rule จะ hardcode token

---

## Output

- Code committed/produced ใน expected location
- Storybook story (ถ้าทีมใช้)
- Deviation log — อะไรที่ implement ไม่ตรง spec และทำไม
- Release notes สั้น ๆ (1-3 บรรทัด) สำหรับ Slack/Confluence

---

## Gate (end of flow)

- [ ] Code build/render ไม่มี error
- [ ] ทุก state ใน spec render ถูก
- [ ] ใช้ DS token เท่านั้น (รัน `validate_usage` ถ้าเป็น DS2)
- [ ] Visual QA ผ่าน — pixel-level เปรียบกับ wireframe (acceptable variance)
- [ ] Behavior QA ผ่าน — happy path + edge case ใน spec
- [ ] Accessibility check — contrast, keyboard, ARIA
- [ ] Responsive — mobile/tablet/desktop ผ่าน
- [ ] Deviation log filled (ถ้ามี)

---

## Deviation severity (same as old standard)

| Level | คำอธิบาย | Action |
|---|---|---|
| Minor | Visual ต่างนิดหน่อย ไม่กระทบ function | Document + accept |
| Moderate | Behavior ต่างแต่ใช้ได้ | Reason ใน deviation log + L1 approve |
| Major | กระทบ task หรือ success metric | L2 decide — fix หรือ accept with plan |

---

## After Stage 5

### Product track — loop back
- Wait 7/14/30 วันหลัง release
- Pull metric (ถ้า card มี success metric)
- Fill `templates/design-retro.md`
- ถ้า metric ไม่ขยับ → เปิด card ใหม่ → back to Stage 0

### Project track — hard stop
- Generate post-launch report
- Fill `templates/design-retro.md`
- Project close — no automatic loop

---

## Common Mistakes

- Vibe code โดยไม่ได้อ่าน DS brand rules → hardcode color
- Generate code แล้วไม่ visual QA → ship ของที่ไม่ตรง spec
- Mix DS1 + DS2 ใน feature เดียว → design debt
- Skip deviation log → ทีมหลังไม่รู้ว่าทำไม implement แบบนี้
- ไม่ check accessibility → ship แล้วเจอ a11y bug ทีหลัง
- ใช้ generic prompt ไม่ใช้ template → output ไม่ consistent

---

## Owner

| Role | Responsibility |
|---|---|
| Claude | Execute vibe code, run DS validation, generate code |
| Level 1 Designer | Direct prompt, review output, visual + behavior QA |
| Level 2 Lead | Approve major deviation, validate DS consistency |
| Engineer (if separate) | Code review, merge |
