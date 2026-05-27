# Stage 6 — Handoff

**Position:** `Test & Improve → HANDOFF → (Project end OR future BE/QA phase)`

---

## Purpose

ส่ง deliverable package **ที่ลูกค้า/ทีมต่อใช้ได้ทันที** — design + code + access + docs — และ **เตรียมการ extension** ให้ future BE/QA phase plug in ได้

---

## Trigger

- Stage 5 ผ่าน gate — client sign-off ได้แล้ว

---

## Input

- Final code repo
- Final design spec (`vibe-design-spec.md`)
- Final staging URL
- Improvement log (closed)
- Test reports
- Original PM Card

---

## Activities

### 6.1 Build handoff package

ใช้ `templates/handoff-doc.md` — มี section:

**Section A — Project summary**
- Objective + scope
- Final deliverable list
- Timeline + actual dates
- Sign-off reference

**Section B — Design**
- Design system used (DS1/DS2/client stack) + reason
- Style tokens (color, typography, spacing)
- Component inventory + variant usage
- Design files (Figma link, artifact links)
- Final design-spec.md
- Brand asset mapping

**Section C — Code**
- Repo URL + access
- Stack + dependencies
- Build / run instructions
- Folder structure overview
- Environment variables list
- Known limitations / TODOs
- Test coverage note

**Section D — Deployment**
- Current staging URL
- Production deploy guide (if not yet deployed to prod)
- Access credentials (handed off via secure channel, not in doc)
- Domain / DNS notes
- Rollback procedure

**Section E — Maintenance**
- Who can do what (read-only / edit / admin)
- Update procedure
- Component update sources (DS, libraries)
- Issue reporting channel (post-handoff support, if any)

**Section F — Future Phase Hooks (NEW)**

**Section F1 — Backend phase pickup**
- Mock data location → swap point
- API contract documented (endpoints expected)
- Auth integration point
- State management style + where BE plugs in
- Pre-marked TODO comments in code

**Section F2 — QA phase pickup**
- Test scenarios documented
- Manual test checklist
- Known edge cases
- Browser/device support claim
- Accessibility audit result

> Section F = สิ่งที่ทำให้ future Sellsuki BE/QA team หรือทีมลูกค้าทำ phase ถัดไปได้โดยไม่ติดต่อ design team กลับ

### 6.2 Verify handoff completeness

Run checklist (in `templates/handoff-doc.md`):

- [ ] Design docs accessible
- [ ] Code repo accessible to receiver
- [ ] Build/run instructions verified (fresh clone test)
- [ ] All credentials transferred via secure channel
- [ ] README in repo updated
- [ ] Future phase hooks documented
- [ ] Receiver acknowledged receipt

### 6.3 Final delivery message

Send via PM:

```
🎉 Project [name] — handoff package พร้อม

📦 Deliverable:
  • Design: [link to handoff doc / Figma]
  • Code: [repo URL]
  • Live: [staging URL]
  • Docs: [link to handoff-doc.md]
  
🔑 Access:
  • ส่งผ่าน [1Password / Bitwarden / secure email]
  • Receiver: [name + email]
  
🔄 Post-handoff:
  • Bug ที่เกิดจากเหตุที่ Sellsuki รับผิดชอบ: support N วัน (per contract)
  • Future iteration: เปิด project ใหม่
  
🚀 Future BE / QA phase:
  • Hook สำหรับ pickup documented ใน Section F ของ handoff doc
  • เมื่อ Sellsuki พร้อม BE/QA team, plug-in ได้ทันที
  
ขอบคุณที่ work ด้วยกันครับ!
```

### 6.4 Internal retro

หลัง handoff:
- Fill `templates/design-retro.md`
- Capture lessons → feed back into next project
- Update `references/ai-persona-library.md` หรือ `references/tech-stack-guide.md` ถ้ามี insight

---

## Output

- `handoff-doc.md` final, comprehensive
- Repo handed over (access transferred)
- Credentials transferred (secure channel)
- Receiver acknowledgment
- Internal retro completed

---

## Gate (end of flow)

- [ ] Handoff doc complete (all sections including F)
- [ ] Repo access verified by receiver
- [ ] Credentials transferred + acknowledged
- [ ] Final delivery message sent
- [ ] Internal retro filled
- [ ] Project marked Closed (PM updates project tracker)

---

## After handoff

### Default (current scope)
- **Hard stop** — design team's work ends here
- Post-handoff support per contract (typically 7-14 days for bug from design team's side)
- No automatic loop

### Future BE phase (planned)
- เมื่อ Sellsuki BE team online:
  - Receive handoff doc Section F1
  - Build backend per API contract documented
  - Connect to FE per swap-point markers
  - Run own iteration (might trigger design re-engagement for edge cases)

### Future QA phase (planned)
- เมื่อ Sellsuki QA team online:
  - Receive handoff doc Section F2
  - Run full QA per scenarios + browser/device matrix
  - Open bugs back to BE/Design as needed
  - Sign-off for production

---

## Why Handoff Doc Section F matters

ตอนนี้ทีม Sellsuki Project ทำแค่ design + frontend vibe code → handoff = work transfer ที่ "incomplete" (BE/QA ต้องทำต่อ)

ในอนาคต Sellsuki จะมี BE + QA → workflow จะขยายเป็น Phase 7-8

**Section F คือ bridge** — design team ทำตอนนี้ → future team plug in ได้ทันที โดยไม่ต้อง redesign handoff process

อ้าง `references/handoff-extension-plan.md` สำหรับ detail ของ future phases

---

## Common Mistakes

- ส่ง handoff โดยไม่ verify repo accessible → receiver ติดขัด → support call
- Credentials via Slack/email plain text → security issue
- ขาด Section F → future BE/QA ต้อง reverse engineer
- ไม่ทำ internal retro → lesson หาย
- ส่งแล้วเงียบ — ไม่ confirm receiver acknowledged
- "Sign-off" จาก Stage 5 ไม่ explicit แต่ proceed handoff → reopened ภายหลัง

---

## Owner

| Role | Responsibility |
|---|---|
| Claude | Generate handoff doc, verify completeness, run final QA |
| Level 1 Designer | Compile package, transfer access, send delivery |
| Level 2 Lead | Approve L/Enterprise handoff, validate Section F |
| PM | Confirm receiver, facilitate acknowledgment, project close |
