# Project Sizing

> How to classify project: S / M / L / Enterprise — used in Stage 0

---

## Why size matters

Project size **drives plan, budget, team allocation, and effort per stage**. Mis-classify → either over-engineer (waste) or under-deliver (broken trust).

Different from product card sizing — project signals include **client tier**, **commercial commitment**, **deliverable count**, not just feature complexity.

---

## Signal matrix

Each signal points S / M / L / Enterprise — รวมแล้ว pick bucket ที่ majority

| Signal | S | M | L | Enterprise |
|---|---|---|---|---|
| **Deliverable count** | 1 (single page) | 2-5 screens | 6-15 screens / multi-module | 16+ / multi-product |
| **Timeline** | < 1 week | 1-3 weeks | 1-3 months | 3+ months |
| **Client tier** | One-off / SME | Mid-market / repeat | Mid-market enterprise | Large enterprise / strategic |
| **Decision makers** | 1 | 1-2 | 2-4 | 5+ / committee |
| **Stack complexity** | Static / single SPA | SPA with mock | SPA + real API integration | Multi-system, custom infra |
| **Brand specificity** | Loose / use ours | Brand kit given | Strict brand guide | Full brand system + governance |
| **UAT round budget** | 1 | 2 | 3 | 3+ (or staged) |
| **Variant count (Stage 2)** | 1-2 | 2 | 2-3 | 3+ |
| **Internal team** | 1 designer | 1 designer + 1 reviewer | 2 designers + lead | Full pod (multiple roles) |
| **Brief depth** | < 100 words | 100-500 words | 500-2000 words / + meeting | RFP / multi-doc |
| **Commercial value** | Lowest tier | Standard | Strategic value | Account-defining |
| **Compliance / regulatory** | none | none | maybe | yes (e.g., HIPAA, fintech) |

---

## Bucket rules

| Bucket | Decision rule |
|---|---|
| **S** | 6+ signals in S column |
| **M** | Mixed S+M majority, OR M majority alone |
| **L** | 5+ signals in L column AND ≥1 signal in Enterprise |
| **Enterprise** | 4+ signals in Enterprise OR explicit RFP/contract signal |

**Ambiguous → default UP** (M instead of S, L instead of M) — under-scoping kills more projects than over-scoping

---

## Examples

### Example 1 — Clear S

**Brief:** "ลูกค้าอยากได้ landing page บริษัท 1 หน้า มี contact form deadline 5 วัน budget เล็ก ๆ"

- Deliverable: 1 page ✓ S
- Timeline: 5 days ✓ S
- Decision: 1 maker ✓ S
- Stack: static ✓ S
- Budget: small ✓ S

→ **S**

### Example 2 — Clear M

**Brief:** "B2B partner portal — 4 screens (login, dashboard, order list, order detail) — 2.5 weeks — Acme Corp, returning client (3rd project) — brand kit ส่งแล้ว — frontend only, BE ต่อให้ทีหลัง"

- Deliverable: 4 screens ✓ M
- Timeline: 2.5 wks ✓ M
- Decision makers: 2 ✓ M
- Stack: SPA + mock ✓ M
- Brand: kit provided ✓ M
- Returning client (mid-market) ✓ M

→ **M**

### Example 3 — Clear L

**Brief:** "Internal admin tool 12 screens, integrate ระบบเก่า client มี 4 stakeholders, brand kit + tone guide เต็ม, 2 months, strict compliance"

- Deliverable: 12 screens ✓ L
- Timeline: 2 months ✓ L
- Decision makers: 4 ✓ L
- Stack: real API integration ✓ L
- Brand: strict guide ✓ L
- Compliance: yes ✓ Enterprise
- Internal team: lead + 2 designers ✓ L

→ **L** (with Enterprise flavor on compliance — surface in risk)

### Example 4 — Enterprise

**Brief:** RFP for 50-page enterprise B2B platform, 4 stakeholders + procurement, multi-quarter, custom DS adaptation, fintech regulatory, integrate with 6 internal systems

- All Enterprise signals across the board

→ **Enterprise** — escalate to Lead immediately

---

## Special cases

### "Rush" project — short timeline but big scope
**Don't downsize because of timeline.** Size by scope, then have scope conversation with PM about feasibility within timeline.

Rush project = **explicit risk** → document in `project-card.md` Section 8

### Repeat client → re-use scope from past project
ทำเหมือนใหม่จะ over-cost client. Instead:
- Pre-research from past project deliverable (read prior `handoff-doc.md` if available)
- Some stages compress (Stage 1 research lighter, brand already known)
- BUT size based on **this project's scope**, not relationship history

### Pilot / POC
- Pilot = explicitly time-boxed S/M to prove direction
- Often follow-on to larger project — flag as such

### Maintenance / Iteration on past handoff
- = sub-project — usually S
- Reference original `handoff-doc.md` heavily
- Stage 1 compress to "delta research"

---

## Pricing implications (informational)

Sellsuki Project team should size for **delivery effort**, but Lead may map to pricing tier. Rough association:

| Size | Effort hours (rough) | Typical engagement |
|---|---|---|
| S | 20-40 | Fixed price, single deliverable |
| M | 60-200 | Fixed price w/ change order budget |
| L | 200-600 | Phased / milestone billing |
| Enterprise | 600+ | Retainer / staged / SOW |

Pricing is PM/Lead's call — designer's role = accurate size assessment

---

## Anti-patterns

- ❌ Size down because client says "small project" — use signals, not client framing
- ❌ Size up for prestige client — effort cost more, but bucket should match scope
- ❌ Resize mid-project because UAT findings — surface as **scope conversation**, not silent re-tier
- ❌ Use timeline alone to size — fast big project is high risk, not actually S
- ❌ Forget Enterprise signals (compliance, multi-stakeholder, strategic) — these change everything

---

## Cross-check: what stage selection looks like

After sizing, refer to Stage selection matrix in SKILL.md:

| Stage | S | M | L/Enterprise |
|---|---|---|---|
| 0 | Quick card | Full card | Full + risk register |
| 1 | Light desk research | Standard + milestone | Full + tech feasibility |
| 2 | 1-2 variants direct | 2 variants | 2-3 variants + mini AI usability |
| 3 | Direct DS swap | Component-by-component | Full vibe code |
| 4 | Single deploy | Deploy + access | Staging + prod prep |
| 5 | 1 round | 2 rounds | 3+ rounds, formal UAT |
| 6 | Lean handoff | Full handoff | Comprehensive + Section F deep |
