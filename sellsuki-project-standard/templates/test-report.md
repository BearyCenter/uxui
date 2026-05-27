# Test Report

> One file per UAT round in Stage 5

---

## Meta

**Project:** `[name]`
**Round:** `1 / 2 / 3`
**Build version:** `[git SHA or version tag]`
**Staging URL:** `[link]`
**Date opened:** `YYYY-MM-DD`
**Date closed:** `YYYY-MM-DD`

---

## Round scope

**Test scenarios sent to client:**
1. `[scenario 1]`
2. `[scenario 2]`
3. `[scenario 3]`

**Test environment:**
- Browser(s) requested: `[Chrome / Safari / mobile / ...]`
- Test data: `[mock / sample / real]`

---

## Internal pre-UAT test result

| Test | Status | Note |
|---|---|---|
| Smoke (from deploy) | ☐ pass | |
| All AC scenarios | ☐ pass | |
| Cross-browser (Chrome, Safari, Firefox) | ☐ pass | |
| Mobile viewport | ☐ pass | |
| Accessibility (keyboard, contrast) | ☐ pass | |
| No console error | ☐ pass | |

**Internal verdict:** `READY FOR CLIENT / NOT READY (reason)`

---

## Client UAT findings

> Log every piece of feedback — even minor

| # | Source | Finding | Severity | Category | Status |
|---|---|---|---|---|---|
| 1 | Client name / role | description | blocker / major / minor | Bug / Improvement / Change request / Out of scope | Open / Fixed / Deferred / Closed |
| 2 | | | | | |

**Category definitions:**
- **Bug** — Implementation doesn't match agreed spec
- **Improvement** — Matches spec, but client wants better
- **Change request** — Client wants something different from spec
- **Out of scope** — Beyond agreed deliverable

---

## Triage decisions

| # | Decision | Owner | Action |
|---|---|---|---|
| | Fix in this round / Defer to next / Out of scope (change order) | | |

---

## Scope conversation (if triggered)

> If any "Change request" or "Out of scope" finding

**Discussed with PM on:** `YYYY-MM-DD`
**Items in question:**
- `[finding #N — description]`

**Outcome:**
- [ ] Accept (in scope, no change)
- [ ] Eat cost (do it without formal change order — document why)
- [ ] Change order (timeline + scope adjust, written agreement)
- [ ] Defer to v2 (out of this project)

**Change order ref (if applicable):** `[link]`

---

## Fixes applied in this round

| # (from findings) | Fix description | Files changed | Re-test result |
|---|---|---|---|
| | | | pass / fail |

---

## Re-deploy

**Re-deployed version:** `[git SHA or tag]`
**Re-deploy date:** `YYYY-MM-DD HH:MM`
**Smoke test after re-deploy:** `PASS / FAIL`

---

## Communication log

| Date | From → To | Channel | Summary |
|---|---|---|---|
| | Designer → PM | Slack | Send round 1 results |
| | PM → Client | Email | UAT instructions |
| | Client → PM | Email | Feedback batch |
| | | | |

---

## Round verdict

- [ ] ✓ All findings closed → ready for next round / sign-off
- [ ] ⚠ Findings pending → schedule next round
- [ ] 🔴 Major issue → escalate

**Decision:** `proceed to next round / proceed to sign-off / re-deploy + extend round`

---

## Time used

| Activity | Hours |
|---|---|
| Internal test | |
| Triage | |
| Fix | |
| Re-deploy + re-test | |
| Comms / coordination | |
| **Total** | |
