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
- Stack: Client's existing / Modern default / Custom modern (locked at Stage 1)
- Repo location
- API contracts (ถ้ามี — หรือใช้ mock)

> ⚠ Project skill **ห้ามใช้ Sellsuki DS 1.0 / DS 2.0** — ใช้ใน `sellsuki-product-standard` skill เท่านั้น

---

## Activities

### 3.1 Prep

| Activity | Description |
|---|---|
| Repo setup | Create fresh scaffold OR clone client's existing repo |
| Dependency install | Per stack — modern default: Next.js + Tailwind + shadcn / Vue: Nuxt + Tailwind / Client stack: their package.json |
| Env config | API endpoints, env vars, secrets (ใช้ .env.example) |
| Fill prompt | Use `templates/vibe-code-prompt.md` (project version) |

### 3.2 Generate (component-by-component)

**For Client's Existing Stack:**
1. Read client's component library docs / Storybook (web_fetch ถ้ามี URL)
2. Read client's existing components (5-10 ตัวเพื่อ pattern match)
3. Map design spec components → client's components
4. Generate code per spec following client conventions
5. Self-audit:
   - ใช้ token / CSS variables ของ client (no hardcode)
   - Naming convention match
   - No unauthorized new dependencies
   - File structure ตาม client repo

**For Modern Default (Next.js + TS + Tailwind + shadcn):**
1. Scaffold: `npx create-next-app@latest --typescript --tailwind --app`
2. Init shadcn: `npx shadcn@latest init`
3. Generate code per spec using shadcn primitives
4. Setup folder structure: /app, /components, /components/ui, /lib, /hooks, /mocks
5. Self-audit: Tailwind tokens only, no inline styles, App Router conventions

**For Custom Modern Stack (Nuxt / Astro / SvelteKit / etc.):**
1. Initialize per framework: `npx nuxi@latest init`, `npm create astro@latest`, etc.
2. Setup Tailwind หรือ stack-appropriate styling
3. Install chosen component library
4. Generate per framework conventions
5. Self-audit per stack's best practices

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
| API pending | Mock service (msw / JSON fixtures / fetch wrapper) + `// TODO: BE-INTEGRATION` markers |
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
- [ ] Token / design variable usage validated (no hardcoded colors, sizes, spacing)
- [ ] No unauthorized new dependencies (especially when using client stack)
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

- Vibe code โดยไม่อ่าน client's component docs / framework conventions → naming + pattern ไม่ match codebase
- ใช้ Sellsuki DS 1.0/2.0 ใน project (ผิด skill — ใช้ `sellsuki-product-standard` สำหรับงาน Sellsuki internal product)
- Skip QA แต่ละ component → bug สะสม
- Ignore deviation log → handoff ขาด context
- Wire data ด้วย hardcoded value แล้วลืมเปลี่ยน
- ไม่ทำ README → คนถัดมาต้องเดา
- Build artifact ขาด → Stage 4 deploy ไม่ได้

---

## Owner

| Role | Responsibility |
|---|---|
| Claude (Claude Code or chat) | Generate code, audit tokens, QA |
| Level 1 Designer | Direct prompt, review code output, visual QA |
| Level 2 Lead | Validate stack consistency, approve any dependency additions |
| Engineer (if exists) | Code review, env setup help |
