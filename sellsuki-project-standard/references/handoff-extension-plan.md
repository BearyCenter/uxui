# Handoff Extension Plan

> Future-state document — อธิบาย Phase 7 (Backend) และ Phase 8 (QA) ที่ Sellsuki Project team จะขยายไปในอนาคต
> ปัจจุบัน skill **จบที่ Stage 6 Handoff** — Section นี้คือ blueprint สำหรับ extension

---

## Current state (today)

Sellsuki Project team scope:
- ✓ Design (Stage 0-2)
- ✓ Frontend implementation via Vibe Code (Stage 3)
- ✓ Deploy staging (Stage 4)
- ✓ UAT + Improve (Stage 5)
- ✓ Handoff (Stage 6)
- ❌ Backend (handed off to client OR future Sellsuki BE team)
- ❌ Formal QA (handed off to client OR future Sellsuki QA team)

**Implication:**
- Handoff doc Section F1 (Backend pickup) และ F2 (QA pickup) ทำหน้าที่ bridge ให้ future phase plug in ได้
- Design + FE work ต้อง self-contained พอที่ทีมต่อ pickup โดยไม่ต้อง redesign

---

## Future state — Phase 7 Backend

### Trigger to activate

Phase 7 จะ online เมื่อ:
- Sellsuki มี dedicated BE team พร้อม
- BE team trained ใน workflow ที่ integrate กับ design phase
- Standard ของ BE team (code, API design, security) documented

### Workflow ที่ projected

```
[FE Handoff] → Phase 7.0 Pickup → 7.1 API Design → 7.2 Implementation → 7.3 Integration → [QA Phase หรือ Re-deploy]
```

| Stage | Activity | Owner |
|-------|----------|-------|
| 7.0 Pickup | Read Section F1 of handoff doc, identify swap points | BE Lead |
| 7.1 API Design | Build OpenAPI spec from FE's expected contracts | BE team |
| 7.2 Implementation | Build endpoints, auth, business logic | BE team |
| 7.3 Integration | Replace FE mock with real API, verify | BE + Design team (light involvement) |

### Handoff doc Section F1 → Phase 7 mapping

| F1 content | Phase 7 use |
|---|---|
| Mock data location | 7.0 — find swap points |
| API contract docs | 7.1 — build to spec |
| Auth integration point | 7.2 — implement auth |
| State management style | 7.3 — wire correctly |
| TODO BE-INTEGRATION markers | 7.0 + 7.3 — verify all swapped |

### Pre-requisites design team prepares NOW

ทั้งหมดเข้าใน Section F1 ของ handoff doc:

- [ ] Mock data ทุก endpoint marked + filed
- [ ] API contract documented as TypeScript types / OpenAPI / Postman / written spec
- [ ] Auth pattern stub + expected behavior
- [ ] All `// TODO: BE-INTEGRATION` markers searchable in code
- [ ] State management pattern doc'd (where API calls live)
- [ ] Error response format expected

ทำให้ BE team **search "// TODO: BE-INTEGRATION"** แล้วเจอทุกจุดที่ต้องเชื่อม

---

## Future state — Phase 8 QA

### Trigger to activate

Phase 8 จะ online เมื่อ:
- Sellsuki มี dedicated QA team พร้อม
- QA framework / process documented
- Browser / device matrix standard agreed

### Workflow ที่ projected

```
[Phase 7 complete OR FE-only handoff] → 8.0 Plan → 8.1 Manual QA → 8.2 Bug bash → 8.3 Sign-off
```

| Stage | Activity | Owner |
|-------|----------|-------|
| 8.0 Plan | Read Section F2, build full test plan | QA Lead |
| 8.1 Manual QA | Run all scenarios + matrix | QA team |
| 8.2 Bug bash | Cross-team coverage of edge cases | QA + Design + BE |
| 8.3 Sign-off | Formal QA sign-off → production | QA Lead + PM |

### Handoff doc Section F2 → Phase 8 mapping

| F2 content | Phase 8 use |
|---|---|
| Test scenarios list | 8.0 + 8.1 — formal test plan basis |
| Manual test checklist | 8.1 — execution checklist |
| Known edge cases | 8.2 — bug bash starting point |
| Browser/device support claim | 8.1 — coverage matrix |
| Accessibility audit result | 8.1 — re-verify + extend |
| Performance baseline | 8.1 — measure regression |

### Pre-requisites design team prepares NOW

ทั้งหมดเข้าใน Section F2:

- [ ] Test scenarios documented (not just "AC")
- [ ] Manual test checklist sample
- [ ] Edge cases identified during Stage 5
- [ ] Browser / device matrix tested + claimed
- [ ] Accessibility audit run (Lighthouse / axe / manual)
- [ ] Performance baseline captured (Lighthouse score, page weight)

ทำให้ QA team **run scenarios from doc** โดยไม่ต้องเดา

---

## Integration: how design team work TODAY supports future phases

| What we do today | Why it matters for future |
|---|---|
| Mock data marked clearly | BE phase finds swap points fast |
| API contract written down | BE phase doesn't reverse-engineer |
| README ครบ | BE/QA onboard in hours, not days |
| Section F1/F2 complete in handoff | Future team picks up clean |
| Cross-browser tested by design team | QA phase has baseline, not from-scratch |
| Accessibility checked | QA phase extends, not starts |

**Cost today:** 1-2 extra hours per project to fill Section F properly
**Benefit when Phase 7/8 online:** prevent days/weeks of reverse engineering per project

---

## Skill evolution roadmap

### v1.0 (current)
- 7 stages (0-6)
- จบที่ handoff
- Section F is **prepare** for future, not active

### v2.0 (when BE Phase ready)
- 8 stages (0-7)
- Stage 7 = Backend Phase
- Section F1 becomes **active input** to Stage 7
- Likely new skill: `sellsuki-project-backend-standard` หรือ integrated

### v3.0 (when QA Phase ready)
- 9 stages (0-8)
- Stage 8 = QA Phase
- Section F2 becomes **active input** to Stage 8
- Production deploy after Stage 8 sign-off

### Architectural decision deferred

**Question:** Phase 7/8 จะอยู่ใน skill เดียวกัน หรือแยก skill?

**Considerations:**
- **Same skill:** Single source of truth, full project flow visible
- **Separate skill:** BE/QA team has own trigger, own context, own evolution

**Tentative direction:** **Separate skills**, but referenced from `sellsuki-project-standard` SKILL.md trigger section. Reason:
- BE/QA team activates from different trigger (handoff doc received, not PM brief)
- Each phase can evolve independently
- Skill file size manageable

แต่ decision จริงตอน team พร้อม

---

## What to communicate to client TODAY about future phases

ลูกค้าควรรู้:
- Sellsuki ตอนนี้ส่งงาน Design + Frontend → handoff
- Backend / QA จะเป็น phase ต่อเมื่อ Sellsuki team พร้อม (estimated [timeframe])
- Handoff doc Section F = ready for plug-in
- ตอนนี้ ลูกค้า / ทีมลูกค้า สามารถใช้ Section F1/F2 ทำเอง หรือรอ Sellsuki Phase 7/8 launch

ใส่ใน Stage 6 Handoff delivery message (ดู `references/client-comm-templates.md`)

---

## Maintenance ของ Section F

> Section F คือสัญญาที่ design team ทำกับ future team

Lead ควร audit เป็นระยะ:

| Cadence | Activity |
|---|---|
| Per project | Verify F1/F2 complete in handoff doc (Stage 6 gate) |
| Quarterly | Sample 3-5 handoff docs — assess if BE/QA team can pick up |
| Pre-Phase 7/8 launch | Walk through real handoff doc กับ BE/QA Lead — find gaps, update template |
| Post-Phase 7/8 launch | First 5 transitions — track friction, iterate Section F template |

---

## Anti-patterns to avoid NOW (so future phases work)

- ❌ "F1 ทำตอน Phase 7 มา" — too late, design context หาย
- ❌ "Mock data inline" — future team หาไม่เจอ → mark with TODO
- ❌ "API contract obvious from code" — assume nothing, document
- ❌ "Browser support claim verbal" — write it in F2
- ❌ Skip accessibility audit because "no current QA" — future QA will trust the audit
- ❌ Generic Section F template not adapted to this project — adapt per project

---

## Forward-looking note

Skill นี้ออกแบบ **deliberately scoped to Stage 6**. ไม่ได้แปลว่า Sellsuki Project team หยุดที่นั่นถาวร — แปลว่าตอนนี้ teams downstream ยังไม่ formed

เมื่อ BE/QA online → skill evolution จะรับ:
- new stages
- new templates
- new rules
- new references

**Backwards compatibility maintained:** Section F format ตอนนี้จะ map ตรงกับ Phase 7/8 input ตอน launch — handoff docs ที่ทำใน v1.0 ใช้ได้กับ Phase 7/8 ใน v2.0/v3.0
