# Design Spec

> Living document — เริ่มกรอกใน Stage 2, finalize ใน Stage 4
> เมื่อ final แล้ว → handoff ไป Stage 5 (vibe code)

---

## Meta

**Card:** `XXX-NNN`
**Title:** `[feature name]`
**Version:** `v1.0`
**Date:** `YYYY-MM-DD`
**Designer:** `[ชื่อ]`
**Status:** `Draft / In Refine / Final / Shipped`

**Linked docs:**
- Intake brief: `[link]`
- Research journey: `[link]`
- IA wireframe: `[link]`
- Persona test results: `[link]`
- Figma file (if any): `[link]`
- Prototype artifact: `[link or description]`

---

## DS Selection

**Choice:** `DS 1.0 / DS 2.0`
**Brand variant (DS2 only):** `patona / ccs3 / oc2plus`

**Rationale:**
`[1-2 บรรทัด ว่าทำไมเลือก — อ้าง references/ds-selection-guide.md]`

---

## User Flow (final)

> ลำดับ user task ตั้งแต่ trigger จนจบ

1.
2.
3.
4.

---

## Screens & States (final)

> ทำซ้ำสำหรับแต่ละ screen

### Screen: `[name]`

| State | Description | Component / Token |
|---|---|---|
| Default | | |
| Loading | | |
| Empty | | |
| Error | | |
| Success | | |
| Disabled | | |
| Hover/Focus | | |

**Notes:**

---

## Behavior & Interaction

| Element | Trigger | Action | Duration / Easing |
|---|---|---|---|
| | | | |

---

## Responsive

| Breakpoint | Layout |
|---|---|
| Mobile (< 768px) | |
| Tablet (768-1024px) | |
| Desktop (> 1024px) | |

---

## Accessibility

- **Contrast ratio:** `[pass/fail AA]`
- **Keyboard:** `[tab order, key behavior]`
- **ARIA:** `[components needing labels/roles]`
- **Focus indicator:** `[description]`
- **Screen reader behavior:** `[description]`

---

## Edge Cases

| Scenario | Expected behavior |
|---|---|
| Text > N chars | |
| Data = 0 / empty | |
| User no permission | |
| Network error / timeout | |
| Concurrent edit | |
| Localization (Thai/English) | |

---

## Findings Applied (จาก Stage 3)

> Friction ที่ fix แล้วใน Stage 4

| # | Friction | Fix applied |
|---|---|---|
| 1 | | |
| 2 | | |

---

## Findings Deferred

> Friction ที่ไม่ fix และเพราะอะไร

| # | Friction | Reason for deferral | Backlog ticket |
|---|---|---|---|
| 1 | | | |

---

## Open Decisions

> ต้องปิดก่อน Stage 5

- [ ] `[decision]` — due: `YYYY-MM-DD` — owner: `[role]`

---

## Vibe Code Notes (input to Stage 5)

**Component inventory:**
| Component | DS source | Variant / Props | Quantity |
|---|---|---|---|
| ssk-button | DS2 | primary | 3 |
| | | | |

**State management:**
`[what state lives where — local, shared, server]`

**API contracts:**
`[endpoints, payloads — link to BE spec ถ้ามี]`

**Known constraints:**
`[performance, browser support, etc.]`

---

## QA Checklist (used in Stage 5 + post-ship)

- [ ] Layout ตรง spec ทุก breakpoint
- [ ] ทุก state render ถูก
- [ ] ใช้ DS token เท่านั้น (no hardcode)
- [ ] Animation/transition ตรง spec
- [ ] Edge cases ทดสอบแล้ว
- [ ] Accessibility ผ่าน (keyboard, contrast, ARIA)
- [ ] ไม่มี console error
- [ ] Responsive ผ่านทุก breakpoint
- [ ] DS validation passed (รัน `validate_usage` สำหรับ DS2)

---

## Deviation Log (filled during Stage 5)

| # | Deviation | Reason | Severity | Approved by |
|---|---|---|---|---|
| | | | minor/moderate/major | |
