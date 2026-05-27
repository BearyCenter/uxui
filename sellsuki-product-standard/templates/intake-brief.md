# Intake Brief

> Output ของ Stage 0 — กรอกทันทีหลัง parse Jira card. ครบ Section 1-2 ก่อน proceed Stage 1

---

## Section 1 — Card

**Jira key:** `XXX-NNN`
**Jira URL:** `https://...atlassian.net/browse/XXX-NNN`
**Title:** `[summary]`
**Type:** `Epic / Story / Task / Bug`
**Date received:** `YYYY-MM-DD`
**Designer:** `[ชื่อ]`

**Parent Epic (ถ้า card เป็น Story):**
- Key: `XXX-NNN`
- Title: `[epic title]`
- Related stories: `XXX-NNN, XXX-NNN`

---

## Section 2 — Classification

**Track:**
- [ ] Product (internal Sellsuki)
- [ ] Project (client / external)

**Size:**
- [ ] S — bug fix, copy change, single field, < 1 day
- [ ] M — new flow, multi-screen feature, 3-7 days
- [ ] L — new product area, multi-epic, 2-4 weeks

**Rationale (ทำไม size นี้):**
`[1-2 บรรทัด, อ้าง signals เช่น "5 story points, 4 ACs, ต้องแก้ DB schema"]`

**DS choice (initial):**
- [ ] DS 1.0 — legacy product/module
- [ ] DS 2.0 — current standard
  - Brand variant: `patona / ccs3 / oc2plus`
- [ ] To be confirmed at Stage 4

---

## Section 3 — Problem & Goal

**Problem Statement:**
> Users ไม่สามารถ [X] เพราะ [Y] ส่งผลให้ [Z]

**User Goal:**
`[user ต้องการทำอะไร]`

**Business Goal:**
`[ทำไม Sellsuki ต้องแก้ — impact, metric]`

---

## Section 4 — Acceptance Criteria (จาก card)

> Copy ตรงจาก Jira card — อย่าตีความใหม่

1. `[AC 1]`
2. `[AC 2]`
3. ...

---

## Section 5 — Scope

**In scope:**
-
-

**Out of scope (ระบุชัด):**
-
-

**Success metric:**
| Metric | Baseline | Target |
|---|---|---|
| | | |

---

## Section 6 — Plan (auto-filled by Claude)

```
Stage 0 ✓ — Intake brief drafted
Stage 1 → Research: [light / full]
Stage 2 → Design: [wireframe only / wire + proto]
Stage 3 → AI Usability: [N personas]
Stage 4 → Refine: [N iterations expected]
Stage 5 → Vibe Code: [DS1 / DS2]

Confirm gates: ก่อน Stage 3, ก่อน Stage 5
```

---

## Section 7 — Open Questions

> ระบุก่อน Stage 1 — ถ้ามีคำถามถาม PO ก่อน

- [ ] `[question]` — owner: PO / Designer / Eng — due: `YYYY-MM-DD`

---

## Status

- [ ] Draft
- [ ] In progress (Stage __)
- [ ] Approved → Stage 1
- [ ] Blocked — reason: `[...]`

**Last updated:** `YYYY-MM-DD HH:MM`
