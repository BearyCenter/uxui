# Tech Stack Guide — Project

> Decision tree สำหรับเลือก stack ที่ Stage 1 — ใช้ได้กับ Project track (รวม option client stack)

---

## Quick decision tree

```
                ┌─ Client มี existing codebase / component lib เป็นของตัวเอง?
                │       ├─ YES + we must integrate → use CLIENT STACK
                │       └─ YES but greenfield UI → consider both, default DS
                │
                ├─ Client เป็น Sellsuki ecosystem (white-label, partner) ?
                │       ├─ YES → use DS 2.0 (brand variant per their tier)
                │       └─ NO ─┐
                │              │
                │              ├─ Project lifetime + maintenance owner?
                │              │       ├─ Sellsuki long-term → DS 2.0 (current standard)
                │              │       ├─ Client takes over → DS 2.0 OR client stack (their choice)
                │              │       └─ One-and-done → DS 2.0 (we know it best)
                │              │
                │              └─ Default → DS 2.0 with patona brand
```

---

## Option A — DS 1.0

**When to use:**
- Client = Sellsuki internal team extension
- Continuation of an old DS1-based project
- Specific request for "match existing Sellsuki product look"

**Stack:** React + Sellsuki DS components
**MCP:** `Sellsuki Design System` (load via tool_search)

**Key MCP tools:**
- `get_brand_rules` — call first
- `get_component` — per component
- `get_color_palette`, `get_design_tokens`
- `get_feature_template` — page scaffold with API/state pattern
- `generate_page_layout`

**Brand:** Sky (single brand)

**Avoid for project work unless:** explicit reason. DS2 is the current standard.

---

## Option B — DS 2.0 (Default for project work)

**When to use:**
- Default choice unless other signal stronger
- New product/page for any client
- Multi-framework compatibility needed (ssk-* Lit components)

**Stack:** ssk-* Lit Web Components (React, Vue, Vanilla compatible)
**MCP:** `Sellsuki Design System3`

**Key MCP tools:**
- `get_brand_rules` — call with brand= param FIRST
- `get_component` — per ssk-* component
- `get_color_palette` — per brand
- `get_design_tokens` — font-size, spacing, radius, semantic
- `generate_page_layout` — dashboard / list / detail / settings / landing
- `generate_form` — form scaffold
- `validate_usage` — ESSENTIAL after generate
- `list_icons` — icon catalog
- `list_country_icons` — country codes

### Brand variants

ต้องเลือก ONE per project:

| Brand | Project context |
|---|---|
| **patona** | Default — Sellsuki merchant-facing tone — most client projects |
| **ccs3** | (call `get_brand_rules` brand=ccs3 to see current applicable scope) |
| **oc2plus** | (call `get_brand_rules` brand=oc2plus to see current applicable scope) |

> ALWAYS call `get_brand_rules` for the selected brand BEFORE writing code — Claude doesn't memorize brand specifics, and they evolve

---

## Option C — Client's Stack

**When to use:**
- Client has existing codebase ที่งานต้อง integrate
- Client mandates specific framework / library
- Client team will maintain long-term and wants their stack
- Stack of client is mature + standard (React + popular lib, Vue + Vuetify, etc.)

**Approach:**

1. **Read their conventions:**
   - Clone repo if access provided
   - Read their existing components (top 5-10)
   - Check ESLint / Prettier / TypeScript config
   - Observe naming conventions
   - Note utility/helper functions to reuse

2. **Map design intent → their components:**
   - Our `ssk-button` → their `<MyButton>`
   - Our `ssk-input` → their `<Input>` or their form component
   - Document mapping in `vibe-design-spec.md` Section 5

3. **Don't bloat their stack:**
   - ห้าม introduce new dependency unless absolutely necessary
   - Use what they have, even if it's slightly worse than what we'd pick fresh
   - If we MUST add: document why, in handoff doc Section C

4. **Tokens:**
   - If they have a design system → use their tokens
   - If they have CSS variables → use those
   - If neither → propose minimal token layer, document

**Risk areas to flag:**
- Stack we've never used (e.g., obscure framework) → Stage 1 feasibility check
- Client lib without good docs → time risk → document
- Client demands stack that's deprecated → push back via PM (we own quality bar)

---

## Mixing rules

| Situation | Rule |
|---|---|
| Mix DS1 + DS2 in same project | ❌ Never |
| Mix DS + client stack in same project | ❌ Never (pick one) |
| Mix DS2 brand variants | ❌ Never within one project |
| Multi-project for one client, different stacks | ⚠ OK if rationale per project |
| DS2 + tiny client utility (e.g., their fetch wrapper) | ✓ OK — utility ≠ component lib |

---

## Decision worksheet (use at Stage 1)

| Question | Answer | Implication |
|---|---|---|
| Who maintains after handoff? | Client / Sellsuki / TBD | Client → favor client stack; Sellsuki → DS2 |
| Existing codebase? | yes / no | yes → likely client stack |
| Multi-framework need? | yes / no | yes → DS2 (Lit works everywhere) |
| Special brand? | yes / no | yes → DS2 with brand variant |
| Compliance / regulatory? | yes / no | yes → use most-audited stack (DS2 likely) |
| Long-term commitment? | yes / no | yes → DS2; no → either |
| Vibe-code productivity priority? | yes / no | yes → DS2 (best MCP support) |

After answering: pick stack, document rationale in `project-card.md` Section 4

---

## After Stage 1: LOCKED

Stack is **locked** after Stage 1. Changing mid-project = scope event:
- Trigger scope conversation (Stage 5 rule)
- Update timeline + cost
- Re-baseline `project-card.md`

ห้าม switch silently. If client requests change mid-project → escalate to Lead.

---

## Stage 3 prompt snippet

When filling `templates/vibe-code-prompt.md`:

**DS 1.0:**
```
STACK: DS 1.0
→ Use `Sellsuki Design System` MCP.
→ Call `get_brand_rules` first.
→ `get_component` per component used.
```

**DS 2.0:**
```
STACK: DS 2.0 (brand: patona)
→ Use `Sellsuki Design System3` MCP.
→ Call `get_brand_rules` with brand=patona first.
→ `get_component` per ssk-* component.
→ After generating: call `validate_usage`.
```

**Client stack:**
```
STACK: Client's React + [their library]
→ Reference: [their Storybook URL / docs / repo path]
→ Follow naming convention, lint config, folder structure of [path]
→ Map our design intent to their components per `vibe-design-spec.md` Section 5
→ Do NOT add dependencies unless documented + approved
```

---

## Common Mistakes

- ❌ Pick stack at Stage 2 instead of Stage 1 → wasted variants
- ❌ Mix DS + client lib because "one component is missing"
- ❌ Use Claude's memory for DS specifics — always call MCP `get_brand_rules`
- ❌ Pick client stack without checking client's docs first → assumptions break in Stage 3
- ❌ Skip `validate_usage` on DS2 → hardcoded tokens slip through
- ❌ Add npm packages to client repo without note → bloat, maintenance pain
