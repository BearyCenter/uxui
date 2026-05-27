# DS Selection Guide

> Decision tree สำหรับเลือก DS 1.0 vs DS 2.0 — สำหรับ Stage 4-5

---

## Quick decision tree

```
                ┌─ Is the target module already on DS 2.0?
                │       ├─ YES → use DS 2.0 (same brand variant)
                │       └─ NO ──┐
                │                │
                │                ├─ Is this a NEW module / NEW product area?
                │                │       ├─ YES → use DS 2.0 (pick brand variant)
                │                │       └─ NO ─┐
                │                │              │
                │                │              ├─ Is migration to DS 2.0 already planned for this module?
                │                │              │       ├─ YES → use DS 2.0 (start migration here)
                │                │              │       └─ NO → use DS 1.0 (don't add migration scope to this card)
                │                │              │
                │                │              └─ Default → use DS 1.0 (match existing module)
```

---

## DS 1.0 (Legacy)

**When to use:**
- Working in a module that's still on DS 1.0
- Bug fix or small change in legacy code
- Card explicitly scoped to "don't migrate, just fix"

**Stack:** React + Sellsuki DS components
**MCP:** `Sellsuki Design System`

**Key MCP tools (call via tool_search first):**
- `Sellsuki Design System:list_components` — see all components
- `Sellsuki Design System:get_component` — component detail
- `Sellsuki Design System:get_brand_rules` — DO/DON'T
- `Sellsuki Design System:get_color_palette` — Sky brand colors
- `Sellsuki Design System:get_design_tokens` — typography, spacing, radius
- `Sellsuki Design System:get_feature_template` — page template with API/state pattern
- `Sellsuki Design System:generate_page_layout` — scaffold

**Brand:** Sky (single brand)

---

## DS 2.0 (Current Standard)

**When to use:**
- New module / new product area
- Module that's already migrated to DS 2.0
- Card with explicit migration scope

**Stack:** ssk-* Lit Web Components (works in React, Vue, Vanilla)
**MCP:** `Sellsuki Design System3`

**Key MCP tools (call via tool_search first):**
- `Sellsuki Design System3:list_components` — ssk-* components
- `Sellsuki Design System3:get_component` — props, slots, events
- `Sellsuki Design System3:get_brand_rules` — per-brand guidelines + use case
- `Sellsuki Design System3:get_color_palette` — per brand
- `Sellsuki Design System3:get_design_tokens` — font-size, spacing, radius, semantic
- `Sellsuki Design System3:generate_page_layout` — scaffold (dashboard, list, detail, settings, landing)
- `Sellsuki Design System3:generate_form` — form scaffold
- `Sellsuki Design System3:validate_usage` — verify HTML/JSX uses ssk-* correctly
- `Sellsuki Design System3:list_icons` — icon catalog
- `Sellsuki Design System3:list_country_icons` — country icon codes

### Brand variants

Pick ONE per card:

| Brand | Use case | Visual identity |
|-------|----------|----------------|
| **patona** | Sellsuki merchant-facing — main platform | Default Sellsuki branding |
| **ccs3** | (call `get_brand_rules` brand=ccs3 for current scope) | (per guidelines) |
| **oc2plus** | (call `get_brand_rules` brand=oc2plus for current scope) | (per guidelines) |

> Always call `get_brand_rules` for the selected brand BEFORE writing code — Claude does not memorize brand specifics

---

## Mixing rules

| Situation | Rule |
|---|---|
| Mix DS1 + DS2 in same feature | ❌ Never — design debt |
| Mix DS1 + DS2 in same module (different pages) | ⚠ Only with migration plan documented |
| Mix two DS2 brand variants in same feature | ❌ Never |
| Mix DS2 brand variants in same module | ⚠ Only if module spans multiple products (rare) |

---

## When DS doesn't have what you need

If the design needs a pattern that doesn't exist in DS:

1. **First** — check if existing component can be composed to achieve it (consult `list_components` + `suggest_components`)
2. **Second** — check the contract changelog (`get_contract_changelog`) — maybe a new component is in progress
3. **Third** — if truly missing, **STOP vibe-code** and:
   - Document the gap in design-spec.md
   - Open a DS request ticket
   - Escalate to L2 Lead
   - DO NOT create a one-off custom component

L2 Lead decides: ship with closest DS component (accept design debt) or wait for DS update

---

## Stage 5 prompt snippet

When filling `templates/vibe-code-prompt.md`, the DS section should look like:

**For DS 1.0:**
```
DESIGN SYSTEM: DS 1.0
→ Call `Sellsuki Design System:get_brand_rules` first.
→ Then `Sellsuki Design System:get_component` for each component in inventory.
→ Use React + Sellsuki DS imports.
```

**For DS 2.0:**
```
DESIGN SYSTEM: DS 2.0 (brand: patona)
→ Call `Sellsuki Design System3:get_brand_rules` with brand=patona first.
→ Then `Sellsuki Design System3:get_component` for each ssk-* component used.
→ After generating, call `Sellsuki Design System3:validate_usage` to verify.
```

---

## Common Mistakes

- ❌ ใช้ DS1 component memory ที่ Claude เคยเรียน — ต้องเรียก MCP เสมอ (อาจ outdated)
- ❌ Pick DS2 brand "default" โดยไม่ดู module context
- ❌ Mix DS1 + DS2 ใน single PR
- ❌ สร้าง custom component "เพราะ DS ไม่มี" โดยไม่ escalate
- ❌ Skip `validate_usage` ใน DS2 — เปิดทางให้ hardcode หลุดผ่าน
