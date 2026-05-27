# Stage 3 — Vibe Code

**Position:** `Vibe Design → VIBE CODE → Deploy`

---

## Purpose

แปลง picked variant → working code ที่ deploy ได้ — ใช้ Claude เป็น primary coder

---

## Trigger

- Stage 2 gate ผ่าน — client picked variant, spec final, stack locked

---

## Input

- `vibe-design-spec.md` (final)
- Picked variant artifacts
- Stack: DS1 / DS2 (brand variant) / client stack
- Repo location
- API contracts (ถ้ามี — หรือใช้ mock)

---

## Activities

### 3.1 Prep

| Activity | Description |
|---|---|
| Repo setup | Create / clone repo, scaffold per stack |
| Dependency install | Per stack — DS1: React + DS1 pkg / DS2: load ssk-* / client: their setup |
| Env config | API endpoints, env vars, secrets (ใช้ .env.example) |
| Fill prompt | Use `templates/vibe-code-prompt.md` |

### 3.2 Generate (component-by-component)

**For DS 1.0:**
1. Call `Sellsuki Design System:get_brand_rules` (MCP — load via tool_search first)
2. Call `Sellsuki Design System:get_component` for each component in inventory
3. Optional: `Sellsuki Design System:generate_page_layout` for scaffold
4. Generate code per screen
5. Wire data + state per spec

**For DS 2.0:**
1. Call `Sellsuki Design System3:get_brand_rules` with chosen brand (patona/ccs3/oc2plus)
2. Call `Sellsuki Design System3:get_component` for ssk-* components
3. `Sellsuki Design System3:generate_page_layout` for boilerplate
4. Generate code
5. Call `Sellsuki Design System3:validate_usage` after each major chunk

**For Client Stack:**
1. Read client's component library docs / Storybook
2. Map design spec components → client stack components
3. Generate code per spec
4. Self-audit: token usage, naming convention match client codebase

### 3.3 QA per component

After each component:
- Visual diff vs design
- Behavior check (events, state, API calls)
- Accessibility (keyboard, ARIA)
- Responsive check

### 3.4 Wire data

| Scenario | Approach |
|---|---|
| API ready | Connect with proper error handling |
| API pending | Mock service (JSON server / msw / fixtures) |
| No backend | Static data + clear "// TODO: replace with API call" markers |

---

## Output

- Working code in repo
- README in repo with: stack, install, run, env vars, known limitations
- Storybook stories (ถ้าทีมใช้)
- Mock data layer (ถ้า API ยังไม่พร้อม)
- Deviation log (สิ่งที่ implement ต่างจาก spec + reason)

---

## Gate to Stage 4 (Deploy)

- [ ] Code builds without error
- [ ] All screens implemented
- [ ] All 6 states render per screen
- [ ] DS validation passed (DS2: validate_usage; DS1/client: manual audit)
- [ ] Visual QA passed (vs picked variant)
- [ ] Behavior QA passed (happy + edge paths)
- [ ] Accessibility check
- [ ] Responsive verified
- [ ] README ครบ
- [ ] Code ready to deploy (build artifact exists)

---

## Client stack constraints

ถ้าใช้ stack ของลูกค้า:
- **ห้าม** introduce new dependency เกินจำเป็น (ทำให้ maintain ยาก)
- ทำตาม code convention ของลูกค้า (file naming, folder structure, lint rules)
- ใช้ utility/helper ที่มีอยู่แล้ว
- ถ้าจำเป็นต้องเพิ่ม pattern → document ใน README + handoff

---

## Common Mistakes

- Vibe code โดยไม่อ่าน DS brand rules / client component docs → hardcode token
- Skip QA แต่ละ component → bug สะสม
- Ignore deviation log → handoff ขาด context
- Wire data ด้วย hardcoded value แล้วลืมเปลี่ยน
- ไม่ทำ README → คนถัดมาต้องเดา
- Build artifact ขาด → Stage 4 deploy ไม่ได้

---

## Owner

| Role | Responsibility |
|---|---|
| Claude (Claude Code or chat) | Generate code, run DS validate, QA |
| Level 1 Designer | Direct prompt, review code output, visual QA |
| Level 2 Lead | Validate stack consistency, approve client stack divergence |
| Engineer (if exists) | Code review, env setup help |
