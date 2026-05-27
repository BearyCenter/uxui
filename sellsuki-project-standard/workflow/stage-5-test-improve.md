# Stage 5 — Test & Improve

**Position:** `Deploy → TEST & IMPROVE → Handoff`

---

## Purpose

Iterate ผ่าน UAT cycle จนลูกค้า sign-off — ใน budget ที่ตั้งไว้

---

## Trigger

- Stage 4 ผ่าน gate — staging URL พร้อม, ลูกค้าได้ access แล้ว

---

## Input

- Staging URL
- UAT round budget (จาก project-card)
- Test scenarios (จาก research-plan หรือ AC)
- Client feedback channel agreed

---

## Activities (looping)

```
┌──────────────┐    ┌────────────┐    ┌──────────────┐    ┌──────────────┐
│ Test (internal│ ─▶ │ Client UAT │ ─▶ │ Triage findings│ ─▶ │ Improve     │
│  + automated) │    │            │    │ + scope check │    │ + redeploy  │
└──────────────┘    └────────────┘    └──────────────┘    └──────┬───────┘
                                                                  │
                                  ┌───────────────────────────────┘
                                  ▼
                            (next round หรือ exit ถ้า sign-off)
```

### 5.1 Internal test (ก่อน client UAT)

| Test type | Coverage |
|---|---|
| Smoke (from Stage 4) | URL, routes, no console err |
| Functional | All AC scenarios pass |
| Cross-browser | Chrome, Safari, Firefox minimum |
| Cross-device | Mobile + desktop, ขั้นต่ำ |
| Accessibility | Keyboard nav, ARIA, contrast |
| Performance | Lighthouse score (ถ้ามี budget) |

### 5.2 Client UAT (per round)

PM facilitates — designer pre-loads scenarios:
- Send test scenario list to client
- Client tests within timebox (default 2-3 days)
- Feedback returns via agreed channel

### 5.3 Triage findings

แต่ละ feedback item → จัด category:

| Category | Definition | Action |
|---|---|---|
| **Bug** | Doesn't match spec | Fix in next round |
| **Improvement** | Matches spec, lukewarm | Negotiate priority |
| **Change request** | Doesn't match spec but client wants new | **Scope check** |
| **Out of scope** | Beyond agreed deliverable | Document, defer |

Track ใน `templates/improvement-log.md`

### 5.4 Scope conversation (when needed)

ถ้า "change request" / "out of scope" findings ปรากฏ:
- Trigger conversation with PM ทันที — ไม่รอ accumulate
- Options:
  - **In scope, do** — if minor, eat the cost, document
  - **Change order** — written agreement, timeline + cost adjust
  - **Defer to v2** — agree to revisit post-handoff

ไม่มี scope conversation = scope creep = project ไม่จบ

### 5.5 Improve + redeploy

- Fix bug + agreed improvements
- Re-test internally
- Redeploy
- Note in changelog what changed (so client knows what to verify)

### 5.6 Round budget tracking

Track in `project-card.md`:

```
UAT Round Budget: 2
Used:
  ✓ Round 1: complete (date) — 5 bugs, 3 improvements, 1 deferred
  ✓ Round 2: complete (date) — 1 bug, 0 improvements
  
Status: BUDGET MET ✓ → proceed Stage 6
```

ถ้าเกิน budget:
- Round N+1 = scope conversation required
- ไม่ silent absorb

---

## Output

- `test-report.md` (per UAT round)
- `improvement-log.md` (cumulative)
- Updated deploy URL (latest version)
- Client sign-off message
- Scope change documentation (ถ้ามี)

---

## Gate to Stage 6 (Handoff)

- [ ] All "Bug" category findings fixed
- [ ] All "Improvement" in scope: done
- [ ] All "Change request": closed (done / change order / deferred to v2)
- [ ] Internal test passed on final version
- [ ] Client explicit sign-off received
- [ ] UAT round budget tracked and respected (or scope conversation closed)

---

## Client checkpoint #3 — Sign-off request

Final ping:

```
Final version deployed สำหรับ project [name]

🔗 URL: [link] (latest build [date])

Last round จัด feedback:
  ✓ [N] bugs fixed
  ✓ [N] improvements applied
  ⏸ [N] deferred to v2 (agreed)

ขอ formal sign-off:
  - Reply กลับมาว่า "approved" / "sign-off" / "ผ่าน"
  - หรือบอกประเด็นที่ยัง pending (ถ้ายังมี)

หลัง sign-off ผมจะส่ง handoff package — design doc + code repo + access — ภายใน [N days]
```

ห้าม proceed Stage 6 จนกว่าจะมี **written sign-off** (Slack message, email, chat reply ทาง PM)

---

## Common Mistakes

- ไม่ track round budget → project ลากยาว
- Triage ไม่ตรง category → bug รวมกับ change request → confused fix
- Improve โดยไม่ใส่ใน changelog → client เจอเปลี่ยนแล้วงง
- Internal test ไม่ทำก่อน UAT → bug ที่ทีมรู้ได้เอง ถูก client เจอ → trust damage
- Proceed handoff โดยไม่มี explicit sign-off → ลูกค้ากลับมาบอก "ยังไม่ ok"
- Scope creep ผ่านโดยไม่ flag → ทีมเสียเวลาฟรี

---

## Owner

| Role | Responsibility |
|---|---|
| Claude | Run internal tests, triage findings, suggest fix priority |
| Level 1 Designer | Improve + redeploy, draft scope conversation triggers |
| Level 2 Lead | Approve scope change, escalation point |
| PM | Facilitate client UAT, scope negotiation, get sign-off |
