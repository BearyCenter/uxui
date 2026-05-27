# Standard Team — Project Track Level 1 (Junior → Senior)

**Purpose:** ส่งงาน client ตรง scope, on time, on budget, ผ่าน sign-off, ส่งต่อให้ทีมต่อ pickup ได้

---

## Brief Handling Rules

| # | Rule | Pass | Fail |
|---|---|---|---|
| B1 | ทุก project ต้องผ่าน Stage 0 — สร้าง project-card.md จาก raw brief | มี project-card | start design จาก brief ตรง ๆ |
| B2 | Classify size + tier ก่อนเริ่ม Stage 1 | rationale ระบุ | เดา |
| B3 | Plan ของ Claude ต้องผ่านสายตา + PM acknowledge ก่อน run | plan posted + confirmed | auto-run without review |
| B4 | Open questions ที่ block — รวมเป็น batch ส่ง PM ภายในวันเดียว | one batch, fast turnaround | drip-feed คำถาม |

---

## Stack & Design Quality Rules

| # | Rule | Pass | Fail |
|---|---|---|---|
| Q1 | Stack locked ที่ Stage 1 — ห้ามเปลี่ยน mid-project | unchanged through project | mid-project stack swap |
| Q2 | ทุก screen ครบ 6 states (default, loading, empty, error, success, disabled) | ครบ | ขาด state |
| Q3 | ใช้ component ของ stack ที่เลือก — ไม่ mix DS + custom | consistent | mixed |
| Q4 | ใช้ token เท่านั้น — no hardcode color/size | clean | hardcoded values |
| Q5 | Responsive ครบ mobile/tablet/desktop | spec'd ทุก breakpoint | skipped |
| Q6 | Accessibility: WCAG AA, keyboard, ARIA | documented | ไม่ระบุ |
| Q7 | Edge case: long text, empty data, no permission, network error | spec'd | skipped |

---

## Variant Rules (Stage 2)

| # | Rule | Pass | Fail |
|---|---|---|---|
| V1 | สร้าง 2+ variants ที่ defendable — ห้าม weak option | all variants viable | "throwaway" variant |
| V2 | Each variant มี distinct direction — ไม่ใช่ color swap | direction differentiated | trivial differences |
| V3 | ทุก variant มี trade-off note ที่ client เข้าใจ | clear pros/cons | "pick this one" bias |
| V4 | Client picks explicitly — ห้ามเดาเลือก | written confirmation | proceed on assumption |

---

## Client Communication Rules

| # | Rule | Pass | Fail |
|---|---|---|---|
| C1 | ทุก client checkpoint ผ่าน PM — ไม่ direct client โดยไม่บอก PM | PM in loop | direct backchannel |
| C2 | Use templates ใน `references/client-comm-templates.md` | consistent tone | ad-hoc message |
| C3 | Sign-off ต้อง explicit + written | confirmed before next stage | "I think they're OK" |
| C4 | Scope conversation เกิดทันทีเมื่อ trigger — ไม่ accumulate | same-day | wait until project end |

---

## UAT / Round Budget Rules

| # | Rule | Pass | Fail |
|---|---|---|---|
| U1 | UAT round budget ตั้งใน Stage 0/1 — track ใน project-card | tracked | unbudgeted |
| U2 | Internal test ก่อน client UAT — ทุกครั้ง | done | client เจอ bug ก่อน |
| U3 | Triage finding ตรง category (Bug/Improvement/Change/OOS) | categorized | bag of "stuff" |
| U4 | Change request → scope conversation ทันที | flagged same day | absorb silently |
| U5 | Re-deploy บันทึก version + smoke test ใหม่ | versioned + tested | unmarked overwrites |

---

## Vibe Code Rules

| # | Rule | Pass | Fail |
|---|---|---|---|
| V1 | DS choice locked ที่ Stage 1 — ใน vibe code ใช้ตามนั้น | consistent | switched |
| V2 | DS2: รัน `validate_usage` หลัง generate | passed | skipped |
| V3 | Client stack: follow client's code convention | matched | inconsistent |
| V4 | Mock data layer marked ชัด (`// TODO: BE-INTEGRATION`) | searchable | inline mock without marker |
| V5 | README สมบูรณ์ — install / run / env / TODO | complete | placeholder README |

---

## Deploy Rules

| # | Rule | Pass | Fail |
|---|---|---|---|
| D1 | Smoke test ผ่าน 100% ก่อนส่ง URL ให้ client | all pass | partial pass |
| D2 | Credentials ส่งผ่าน secure channel (1Password / etc.) | secure | Slack plain text |
| D3 | Staging มี noindex + robots disallow | hidden from search | exposed |
| D4 | Known limitations note ส่งให้ client พร้อม URL | provided | client surprised |

---

## Handoff Rules

| # | Rule | Pass | Fail |
|---|---|---|---|
| H1 | Handoff doc ครบทุก section รวม F (Future Phase Hooks) | complete | F skipped |
| H2 | Receiver acknowledge ก่อน close project | confirmed | silent close |
| H3 | Fresh clone test — repo run ได้ด้วยตัวเอง | tested | "should work" |
| H4 | All TODO BE-INTEGRATION markers documented ใน Section F1 | listed | scattered comments |
| H5 | Test scenarios + browser/device matrix ใน F2 | documented | "we tested it" |

---

## Ownership Rules

| # | Rule | Pass | Fail |
|---|---|---|---|
| O1 | รู้ project margin (time used vs budget) | actively track | unaware |
| O2 | Flag risk early — ไม่รอ stage 5 | proactive | reactive |
| O3 | Build relationship กับ client (via PM) | client repeat business signal | one-and-done feel |
| O4 | Internal retro หลัง handoff — fill template ครบ | done within 1 week | skipped |
| O5 | Update persona library / skill เมื่อ project surface gap | proposal submitted | seen but ignored |

---

## Hard No

- ❌ Proceed Stage 3 โดย client ยังไม่ pick variant explicit
- ❌ Skip Stage 4 smoke test — ส่ง URL ให้ client ก่อน internal verify
- ❌ Vibe code ด้วย stack ที่ไม่ใช่ stack ที่ lock ที่ Stage 1
- ❌ Stage 5 absorb scope creep ทั้งหมดโดยไม่ flag PM
- ❌ Handoff ขาด Section F — future BE/QA pickup ไม่ได้
- ❌ Credentials ผ่าน Slack/email plain text
- ❌ Sign-off ที่ inferred ("ผมคิดว่า client OK แล้ว")
- ❌ Project close โดยไม่ทำ retro

---

## Mindset

```
Junior  → "ฉัน execute project standard ได้ทุก stage โดยไม่ตก gate"
Mid     → "ฉัน manage client expectation + scope budget + AI tooling ได้พร้อมกัน"
Senior  → "ฉันเห็น project risk ตั้งแต่ brief, flag PM ก่อน, และ deliver value ที่ client invite Sellsuki กลับมา"
```
