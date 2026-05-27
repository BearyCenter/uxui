# Vibe Code Prompt — Project

> Template prompt สำหรับ Stage 3 — Project flow
>
> Project ใช้ **client's existing stack** หรือ **modern framework choice** — **ห้ามใช้ Sellsuki DS 1.0/2.0** (DS เป็นของ Sellsuki internal product, ใช้ `sellsuki-product-standard` skill)
>
> Fill variables → use as first message of vibe-code session

---

## Template

```
Implement project [{project_name}] for client [{client_name}].

STACK: {stack_choice}
{ถ้า "Client's existing stack"}
→ Client uses: {framework + component library + key deps}
→ Their repo / docs: {repo_path or docs_url}
→ MUST follow their conventions:
   - File naming + folder structure
   - Lint + Prettier config
   - State management pattern
   - Naming conventions (camelCase / kebab / PascalCase)
→ Map our design intent → client's components per vibe-design-spec.md Section 5
→ Reuse their utility/helper functions (look in /utils, /lib, /helpers)
→ Do NOT introduce new dependencies unless absolutely necessary + documented

{ถ้า "Modern default" (Next.js + TS + Tailwind + shadcn/ui)}
→ Initialize: Next.js 14 App Router, TypeScript strict, Tailwind CSS
→ Component primitives: shadcn/ui (copy into /components/ui)
→ Forms: react-hook-form + Zod for validation
→ State: useState by default; Zustand only if cross-component complexity
→ Data fetching: TanStack Query or native fetch
→ Follow Next.js App Router conventions (server/client components, route handlers)

{ถ้า "Custom modern stack"}
→ Framework: {framework — e.g., Nuxt 3 / Astro / SvelteKit / Vite + React}
→ Language: {TypeScript / JavaScript}
→ Styling: {Tailwind / CSS modules / styled-components / other}
→ Component primitives: {shadcn / Radix / PrimeVue / other}
→ Specific patterns to follow: {e.g., "Astro islands for interactivity", "Composition API for Vue"}

FRAMEWORK / OUTPUT TYPE:
- Output: {full app / single page / component library / Storybook stories}
- Repo location: {fresh scaffold / existing repo at path}

---

DESIGN SPEC SOURCE:
{paste vibe-design-spec.md OR link}

KEY POINTS:
- Screens to implement: {list from spec}
- Component inventory: {paste from spec Section 5}
- API contracts: {paste from spec Section 6 — note if mocking}
- Cross-screen rules: {paste from spec Section 7}
- Responsive: {breakpoints — typically Tailwind sm/md/lg/xl or matching client breakpoints}
- Brand tokens: {color, typography, spacing — from research-plan Section 4}

---

CONSTRAINTS (non-negotiable):
1. Use tokens / design variables only — no hardcoded colors, sizes, spacing
2. All 6 states must render per screen (default, loading, empty, error, success, disabled)
3. Match component inventory exactly — don't substitute
4. Accessibility: keyboard navigation, ARIA labels, semantic HTML
5. If you would deviate from the spec, STOP and ask — don't silently change
6. Mock API where real API isn't ready; mark every mock with `// TODO: BE-INTEGRATION`
7. For client stack: do NOT introduce new dependencies without explicit approval

---

PROCESS:
1. Read context:
   {ถ้า client stack} → Read client's existing components, lint config, conventions
   {ถ้า modern default / custom} → Initialize project scaffold + base dependencies
2. Scaffold repo if needed (build tool, dependencies, env)
3. Generate code screen-by-screen
4. Each screen: implement all 6 states
5. Wire data: real API if available, mock otherwise (with TODO markers)
6. After all screens:
   - Audit token usage (no hardcoded values)
   - Verify accessibility (keyboard, contrast, ARIA)
   - Check responsive breakpoints
7. Write README:
   - Stack + dependencies
   - Install + run instructions
   - Env vars + .env.example
   - Known limitations
   - Where mock data lives (for Stage 4 deploy + Section F1 of handoff)
8. Report:
   - What was implemented
   - Any deviations from spec + reason
   - Any places where spec was ambiguous
   - Any new dependencies added (if any) + justification

Begin.
```

---

## Filling guide

| Variable | Source |
|---|---|
| `{project_name}` | `project-card.md` Section 1 |
| `{client_name}` | `project-card.md` Section 1 |
| `{stack_choice}` | `project-card.md` Section 4 (locked at Stage 1) |
| `{framework + lib + deps}` | If client stack — describe their setup |
| `{repo_path / docs_url}` | Client's Storybook, design system doc, or repo URL |
| `{output type}` | Per project scope |
| `{paste spec}` | `vibe-design-spec.md` finalized |

---

## Variant A — Mock data layer (recommended for M/L when API not ready)

Add to PROCESS step 5:
```
5. Wire data using mock layer:
   - Create `mocks/` folder with JSON fixtures per endpoint
   - Use msw (Mock Service Worker) for runtime intercept, OR simple fetch wrapper returning fixture data
   - Mark every mock call in code: `// TODO: BE-INTEGRATION — replace with API call to {endpoint}`
   - In README, list every TODO marker so BE phase can grep for them
   - This directly feeds Section F1 of handoff doc
```

---

## Variant B — Working in client's existing codebase

Add to PROCESS step 1:
```
1. Read client's existing code FIRST:
   - Examine folder structure deeply (3-5 levels)
   - Read 5-10 existing components for patterns
   - Check eslintrc, prettierrc, tsconfig
   - Identify naming conventions (file, variable, component)
   - List utility functions to reuse (don't duplicate)
   - Note state management pattern (Redux/Zustand/Context/etc.)
   - Look for existing form patterns
   - Check their CSS approach (Tailwind / CSS-in-JS / modules / styles folder)
   → Take notes BEFORE writing any code
```

---

## Variant C — Greenfield Next.js + shadcn

Add to PROCESS step 2:
```
2. Scaffold Next.js project:
   - npx create-next-app@latest --typescript --tailwind --app
   - npx shadcn@latest init
   - Install: react-hook-form, zod, @hookform/resolvers, @tanstack/react-query (if needed)
   - Setup folder structure:
     /app           — routes (App Router)
     /components    — feature components
     /components/ui — shadcn primitives
     /lib           — utilities
     /hooks         — custom hooks
     /mocks         — mock API responses (if API not ready)
   - Config: env.mjs for type-safe env vars
```

---

## Variant D — Vue / Nuxt project

Replace stack section with:
```
STACK: Nuxt 3 + TypeScript + Tailwind CSS + {Vue UI lib if any}
→ Composition API throughout (no Options API)
→ VueUse for composables
→ Forms: vee-validate + Zod
→ State: Pinia (only if needed across components)
→ Follow Nuxt directory conventions (pages/, components/, composables/, server/)
```

---

## After code is generated

Run **Stage 3 gate checklist** (see `workflow/stage-3-vibe-code.md`):

- [ ] Build succeeds
- [ ] All screens render
- [ ] All 6 states per screen
- [ ] Token / design variable usage validated (no hardcoded values)
- [ ] Visual QA passed (compare to picked variant from Stage 2)
- [ ] Behavior QA passed (happy + edge paths)
- [ ] Accessibility check (keyboard, contrast, ARIA)
- [ ] Responsive verified (mobile / tablet / desktop)
- [ ] README ครบ
- [ ] Mock data documented + TODO markers in place
- [ ] No unauthorized new dependencies (for client stack)
- [ ] Deviation log filled (if any)

If any fail → iterate prompt + regenerate failing piece

---

## Tips for AI-assisted vibe code

| Tip | Why |
|---|---|
| Show Claude sample component from client codebase | Pattern-match conventions accurately |
| Provide web_fetch link to client's Storybook | Claude can read component docs |
| Include spec Section 5 (component inventory) verbatim | Reduces guessing |
| Specify breakpoints explicitly (not "responsive") | Claude defaults vary by stack |
| For client stack: include their package.json snippet | Avoids adding incompatible deps |

---

## When to NOT use this template

- Brief design tweak only (no implementation work) → skip Stage 3
- Vibe coding without final design-spec → go back to Stage 2
- Pattern doesn't exist in chosen stack and can't be composed → STOP, escalate to Lead (don't create one-off custom)
- **For Sellsuki internal product work** → ใช้ `sellsuki-product-standard` skill's vibe-code-prompt.md แทน (มี DS 1.0/2.0 integration)
