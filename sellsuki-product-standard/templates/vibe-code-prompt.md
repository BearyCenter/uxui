# Vibe Code Prompt

> Template prompt สำหรับ Stage 5 — Claude ใช้กับตัวเอง (ใน Claude Code) หรือใน chat
> Fill variables, then use as the first message of a vibe-code session

---

## Template

```
Implement the design spec for {card_key}: {feature_name}.

DESIGN SYSTEM: {DS1 / DS2 + brand variant}
{ถ้า DS1}
→ Use the `Sellsuki Design System` MCP. Call `get_brand_rules` first, then `get_component` for each component used.

{ถ้า DS2}
→ Use the `Sellsuki Design System3` MCP. Call `get_brand_rules` first to load the {brand} guidelines, then `get_component` for each ssk-* component. After generating code, call `validate_usage` to verify.

STACK: {React / Vue / Vanilla — depending on target repo}
LOCATION: {file path or repo)
OUTPUT: {single component / full page / story file}

---

SPEC SOURCE:
{paste design-spec.md OR link to it}

KEY POINTS:
- Screens to implement: {list}
- States required (per screen): default, loading, empty, error, success, disabled
- DS components used: {list from spec inventory}
- API: {endpoint contracts or "use mock for now"}
- Responsive: {breakpoints}

---

CONSTRAINTS (non-negotiable):
1. Use DS tokens only — no hardcoded colors, sizes, spacing
2. All 6 states must render (even if empty/success are trivial)
3. Match the spec's component inventory exactly — don't substitute components
4. Accessibility: keyboard navigation, ARIA labels per spec
5. If you would deviate from the spec, STOP and ask — don't silently change

---

PROCESS:
1. Read the relevant MCP tools (list_components, get_brand_rules)
2. Review the spec section by section
3. Generate code for one screen at a time
4. For each screen: implement all 6 states
5. After all screens: run `validate_usage` (DS2) or spot-check tokens (DS1)
6. Report:
   - What was implemented
   - Any deviations + reason
   - Any places where the spec was ambiguous

Begin.
```

---

## Filling guide

| Variable | Where to find it |
|---|---|
| `{card_key}` | Intake brief Section 1 |
| `{feature_name}` | Intake brief Section 1 |
| `{DS choice}` | Design spec DS Selection section |
| `{brand}` (DS2 only) | Design spec DS Selection section |
| `{stack}` | Repo conventions or PO's spec |
| `{file path / repo}` | Engineering input or PO instruction |
| `{output type}` | Depends on card scope |
| `{paste spec}` | Copy the final design-spec.md |
| `{components}` | Component inventory section of design-spec.md |
| `{API contracts}` | Vibe Code Notes section of design-spec.md |
| `{breakpoints}` | Responsive section of design-spec.md |

---

## Variants of the prompt

### Variant A — Storybook story only
Replace OUTPUT with: `OUTPUT: Storybook story (.stories.tsx) showing all states`
Skip the API contract section.

### Variant B — Inline artifact for demo
Replace LOCATION with: `LOCATION: Claude HTML artifact for inline demo`
Replace OUTPUT with: `OUTPUT: single-file HTML using ssk-* via CDN`

### Variant C — Full page in repo
Add: `Follow the page-layout pattern — call generate_page_layout to scaffold first`

---

## After the code is generated

Run the **Stage 5 gate checklist** (see `workflow/stage-5-vibe-code.md`):

- [ ] Code renders without error
- [ ] All states render correctly
- [ ] DS tokens only (validate_usage for DS2)
- [ ] Visual QA — matches wireframe
- [ ] Behavior QA — happy + edge paths
- [ ] Accessibility — keyboard, contrast, ARIA
- [ ] Responsive — mobile/tablet/desktop
- [ ] Deviation log filled (if any)

If any item fails: iterate the prompt and re-generate the failing screen.

---

## When to NOT use this template

- Card is S-size and just needs a copy change → direct edit, no prompt needed
- Vibe coding a brand-new pattern that doesn't exist in DS → STOP, escalate to Lead (this means DS needs a new component first)
- Spec is incomplete → go back to Stage 4, don't vibe code from a draft
