# Vibe Code Prompt — Project

> Template prompt สำหรับ Stage 3 — Project flow (รวม DS1/DS2 + client stack option)
> Fill variables, use as first message of vibe-code session

---

## Template

```
Implement project [{project_name}] for client [{client_name}].

STACK: {DS1 / DS2 (brand) / client stack}

{ถ้า DS1}
→ Use the `Sellsuki Design System` MCP. Call `get_brand_rules` first, then `get_component` for each component used.

{ถ้า DS2}
→ Use the `Sellsuki Design System3` MCP. Call `get_brand_rules` with brand={brand} first. Then `get_component` for each ssk-* component. After generating, call `validate_usage`.

{ถ้า client stack}
→ The client uses {stack_description}. Component library docs: {docs_link or "follow conventions from existing repo at {repo_path}"}.
→ Map our design components to client's library:
  - Our `ssk-button` equivalent → client's `{their_button}`
  - Our `ssk-input` equivalent → client's `{their_input}`
  - [...]
→ Do NOT introduce new dependencies unless absolutely necessary
→ Follow client's code conventions (file naming, folder structure, lint rules)

FRAMEWORK: {React / Vue / Next.js / etc.}
REPO: {repo_path or "fresh scaffold"}
OUTPUT: {full app / single page / component library / Storybook}

---

DESIGN SPEC SOURCE:
{paste vibe-design-spec.md OR link}

KEY POINTS:
- Screens to implement: {list from spec}
- Component inventory: {paste from spec Section 5}
- API contracts: {paste from spec Section 6 — note if using mock}
- Cross-screen rules: {paste from spec Section 7}
- Responsive: {breakpoints}
- Brand tokens: {color, typography, spacing — from research-plan Section 4}

---

CONSTRAINTS (non-negotiable):
1. Use chosen stack's tokens only — no hardcoded colors, sizes, spacing
2. All 6 states must render per screen (default, loading, empty, error, success, disabled)
3. Match component inventory exactly — don't substitute components
4. Accessibility: keyboard navigation, ARIA labels per spec
5. If you would deviate from the spec, STOP and ask — don't silently change
6. Mock API where real API isn't ready; mark with `// TODO: replace with real endpoint`

---

PROCESS:
1. Read relevant MCP tools (DS1 / DS2) OR client lib docs
2. Scaffold repo if needed (build tool, dependencies, env)
3. Generate code screen-by-screen
4. Each screen: implement all 6 states
5. Wire data: real API if available, mock otherwise
6. After all screens: 
   - DS2: call `validate_usage`
   - DS1 / client: manual audit for token consistency
7. Write README:
   - Stack + dependencies
   - Install + run instructions
   - Env vars
   - Known limitations
   - Where mock data lives (so Stage 4 deploy + Section F of handoff doc reference is straightforward)
8. Report:
   - What was implemented
   - Any deviations + reason
   - Any places where spec was ambiguous

Begin.
```

---

## Filling guide

| Variable | Source |
|---|---|
| `{project_name}` | `project-card.md` Section 1 |
| `{client_name}` | `project-card.md` Section 1 |
| `{stack}` | `project-card.md` Section 4 (locked at Stage 1) |
| `{brand}` (DS2) | `project-card.md` Section 4 |
| `{stack_description}` | If client stack, describe their setup |
| `{docs_link}` | Client's Storybook URL, design system doc, or repo |
| `{framework}` | From research-plan or client repo |
| `{repo_path}` | Stage 3 setup |
| `{output type}` | Per project scope |
| `{paste spec}` | `vibe-design-spec.md` finalized |

---

## Variant A — Mock data layer

ใช้สำหรับ M/L project ที่ API ยังไม่พร้อม:

Add this to PROCESS step 5:
```
5. Wire data using mock layer:
   - Create `mocks/` folder with JSON fixtures per endpoint
   - Use msw (Mock Service Worker) for runtime intercept
   - OR simple fetch wrapper that returns fixture data
   - Mark in code: `// TODO: replace mock with API call to {endpoint}`
   - In README, list every TODO so BE phase can find them
```

---

## Variant B — Client stack focus

When working in client's existing codebase:

Add this to PROCESS step 1:
```
1. Read the client's existing code:
   - Examine folder structure
   - Read existing components for pattern
   - Check lint config + tsconfig
   - Identify naming conventions
   - Check existing utility functions to reuse
```

---

## After code is generated

Run **Stage 3 gate checklist** (see `workflow/stage-3-vibe-code.md`):

- [ ] Build succeeds
- [ ] All screens render
- [ ] All 6 states per screen
- [ ] DS / stack token usage validated
- [ ] Visual QA passed
- [ ] Behavior QA passed
- [ ] Accessibility check
- [ ] Responsive verified
- [ ] README ครบ
- [ ] Mock data documented (if used)
- [ ] Deviation log filled (if any)

If any fail → iterate prompt + regenerate failing piece

---

## When to NOT use this template

- Brief design tweak only (no implementation work) → skip Stage 3
- Vibe coding without final design-spec → go back to Stage 2
- Pattern doesn't exist in stack and can't be composed → STOP, escalate to Lead (don't create custom)
