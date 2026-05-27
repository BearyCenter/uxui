# Stage 3 — AI Usability Test

**Position:** `Design → AI USABILITY → Refine`

---

## Purpose

ทดสอบ prototype กับ **AI personas** ที่ simulate user จริง — หา friction ก่อน vibe code

---

## Why AI persona (ไม่ใช่ real user)

- **Speed** — รัน 3 personas ใน 10 นาที, real user ใช้ 1-2 สัปดาห์
- **Iteration cost ต่ำ** — ปรับ prototype แล้ว rerun ทันที
- **Standardize ได้** — persona library version-controlled ใน repo
- **Catch obvious friction** — 70-80% ของ usability issues หยิบได้แค่ heuristic + persona simulation

**ไม่ได้แทน real user research** — สำหรับ L-card หรือ feature ใหม่ที่กระทบ revenue, ควร validate กับ real user หลัง launch (อยู่ใน design retro)

---

## Trigger

- Stage 2 gate ผ่าน — prototype + spec draft พร้อม
- Persona shortlist จาก Stage 1 ระบุไว้แล้ว

---

## Input

- Prototype (HTML artifact หรือ wireframe spec)
- Persona shortlist (จาก Stage 1)
- `references/ai-persona-library.md` — base persona prompts
- AC ของ card — ใช้เป็น task ให้ persona ทำ

---

## How to run a test

### Step 1: Pick personas

จาก library:
- **Power user** — ใช้บ่อย, เร็ว, รู้ shortcut, frustrated กับ extra clicks
- **New user** — เพิ่งเริ่ม, สับสนกับ jargon, ต้องการ hint
- **Mobile-first** — ใช้มือถือเป็นหลัก, touch target สำคัญ
- **Edge-case user** — data เยอะมาก (1000+ items), permission แปลก, edge persona

**Number of personas by card size:**
| Size | Min personas | Recommended |
|---|---|---|
| S | 0 (skip ถ้า flow ไม่เปลี่ยน) | 1 |
| M | 1 | 2 |
| L | 2 | 3-4 |

### Step 2: Compose persona prompt

ใช้ template ใน `templates/persona-ai-script.md`:

```
You are [persona name]. Your background: [...]. Your goal: [...]. Your frustrations: [...].

You're going to walk through this prototype to accomplish: [task from AC].

For each screen/step:
1. Describe what you see (in your own words)
2. State what you'd click/tap next, and why
3. Note anything confusing or annoying
4. If you'd give up, say so and why

Stay in character. Be honest. Don't try to "succeed" — try to use it like you actually would.
```

### Step 3: Run

- Paste prototype description + persona prompt → ask Claude (in a separate context or sub-task) to roleplay
- หรือถ้ามี persona ที่ specific, ใช้ in current chat ก็ได้
- **Run แต่ละ persona separate** — อย่าให้ persona รู้กันและกัน

### Step 4: Log findings

กรอก `templates/persona-test-result.md`:

```
Persona: [name]
Task attempted: [...]
Time-on-task (estimated): [...]
Outcome: ✓ completed / ⚠ completed with friction / ✗ gave up

Friction points:
  1. [screen/step] — [what happened] — [severity: blocker/major/minor]
  2. ...

Direct quotes (จาก persona):
  - "..."

Suggested fix (Claude's interpretation):
  - ...
```

### Step 5: Synthesize

รวม findings จากทุก persona:
- Common friction (เจอจาก 2+ personas) → must-fix
- Persona-specific friction → fix ถ้าตรงกับ target user
- Nice-to-have insight → log ใน design retro

---

## Output

- `persona-test-result.md` (1 ไฟล์ต่อ persona หรือรวมก็ได้)
- Friction list ที่จัด severity แล้ว
- Updated open issues ใน `design-spec.md`

---

## Gate to Stage 4 (Refine)

- [ ] Minimum personas รัน ครบ (ดู table ด้านบน)
- [ ] Friction points มี severity (blocker / major / minor)
- [ ] Must-fix list ระบุ — สิ่งที่ต้อง fix ก่อน vibe code
- [ ] Nice-to-have list ระบุ — สิ่งที่ note ไว้ ไม่ block

---

## Confirmation gate กับ user

**ก่อน run Stage 3:**
Claude ถาม:
> ผมจะ run persona test ด้วย [persona A] และ [persona B] — เห็นด้วยไหม หรืออยากปรับ?

ถ้า user OK → run
ถ้า user เสนอ persona ใหม่ → adjust → confirm → run

---

## Common Mistakes

- เลือก persona แบบ generic → findings ไม่ specific
- Run แค่ persona "เก่ง" → ไม่เจอ friction ที่ new user เจอ
- ให้ persona "succeed" — persona ต้องประพฤติแบบจริง รวมถึงสับสน, ผิด, ยอมแพ้
- ไม่จด severity → ทุก finding ถูก fix หมด → over-engineering ใน Stage 4
- Ignore findings ที่ "ไม่ตรงกับ design intent" — บางทีนั่นแหละคือสัญญาณว่า intent ผิด

---

## Owner

| Role | Responsibility |
|---|---|
| Claude | Compose persona prompts, run simulation, log findings |
| Level 1 Designer | Choose personas, interpret findings, decide fix priority |
| Level 2 Lead | Review findings for L-card, validate persona realism |
