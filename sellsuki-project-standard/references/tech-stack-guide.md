# Tech Stack Guide — Project

> Decision tree สำหรับเลือก stack ของ project — ใช้ที่ Stage 1
>
> **Important:** Project = **client work**. ห้ามใช้ Sellsuki DS 1.0 / DS 2.0 ใน project skill นี้ — DS เป็นของ Sellsuki internal product เท่านั้น (ดู `sellsuki-product-standard` skill)
>
> Project ใช้ stack ของ **ลูกค้า** หรือ **modern stack ที่เหมาะกับงาน**

---

## Quick decision tree

```
                ┌─ Client มี existing codebase / component library อยู่แล้ว?
                │       ├─ YES + งานต้อง integrate → use CLIENT STACK (top priority)
                │       └─ YES แต่ greenfield UI / แยก app → discuss กับ client
                │              ├─ Client wants their stack → CLIENT STACK
                │              └─ Client OK with new stack → NEW STACK
                │
                ├─ ไม่มี existing codebase / greenfield?
                │       ├─ Client มี framework preference ระบุไว้ → use that
                │       ├─ Client neutral → pick BEST FIT per project requirement
                │       └─ Client ขอให้แนะนำ → use DEFAULT stack
                │
                └─ ตัดสินใจ stack ต้อง LOCK ที่ Stage 1 — ห้ามเปลี่ยน mid-project
```

---

## Option A — Client's Existing Stack

**When to use:**
- Client มี codebase ที่งานต้อง integrate (most common)
- Client mandate framework / library specific
- Client team จะ maintain ต่อ + ต้องการ stack ของตัวเอง

**Approach:**

1. **Read client's conventions ก่อน Stage 3:**
   - Clone repo ถ้ามี access
   - Read existing top-level components (5-10 ตัว) เพื่อ pattern matching
   - Check ESLint / Prettier / TypeScript / build config
   - Observe naming conventions (camelCase vs kebab vs PascalCase)
   - Note utility/helper functions ที่ reuse ได้
   - Identify state management pattern (Redux / Zustand / Context / etc.)

2. **Map design intent → client's components:**
   - Identify equivalent components ใน client's library
   - Document mapping ใน `vibe-design-spec.md` Section 5
   - ถ้า component หายไป — propose แต่ document why

3. **Don't bloat their stack:**
   - ห้าม introduce new dependency เกินจำเป็น
   - ใช้สิ่งที่เขามี แม้จะ slightly worse than fresh pick
   - ถ้าจำเป็นต้องเพิ่ม: document ใน README + handoff doc Section C
   - Get PM/client approval ถ้า new dep > minor

4. **Tokens:**
   - ถ้ามี design system → ใช้ tokens ของเขา
   - ถ้ามี CSS variables → ใช้ตามนั้น
   - ถ้าไม่มี → propose minimal token layer ใน Stage 1, document

**Risk areas to flag at Stage 1:**

| Risk | Action |
|---|---|
| Stack ที่ Sellsuki ไม่เคยใช้ (obscure framework) | Feasibility check at Stage 1 |
| Client library no good docs | Time risk → document in `project-card.md` Section 8 |
| Client demands deprecated stack | Push back via PM — we own quality bar |
| Client codebase legacy + tightly coupled | Propose isolated module/widget approach |
| Client wants stack but no codebase | Confirm reason — may be misplaced preference |

---

## Option B — New Stack (Greenfield, Client Neutral)

**When to use:**
- ไม่มี existing codebase
- Client OK กับ stack ที่ Sellsuki แนะนำ
- Project standalone, no integration

### Default modern stack (Sellsuki Project team preference)

> นี่คือ **suggested defaults** — adapt ตาม project requirement

| Layer | Default choice | Reason |
|---|---|---|
| **Framework** | Next.js (App Router) | SSR + static + API routes, mature, well-supported |
| **Language** | TypeScript | Type safety, better AI vibe-code accuracy |
| **Styling** | Tailwind CSS | Utility-first, fast, AI-friendly |
| **Component primitives** | shadcn/ui หรือ Radix | Accessible, headless, copy-paste ownership |
| **Forms** | react-hook-form + Zod | Validation + types |
| **State** | useState / Zustand (if needed) | Simple → scale |
| **Data fetching** | TanStack Query / native fetch | Cache + retry |
| **Hosting** | Vercel (default) | Auto preview, simple |

### Alternative stacks (per project type)

| Project type | Recommended stack |
|---|---|
| Landing page / marketing | Next.js + Tailwind + Framer Motion |
| Web app (SPA-ish) | Next.js / Vite + React + Tailwind |
| Internal admin / dashboard | Next.js + Tailwind + shadcn/ui |
| Mobile-first web | Next.js + Tailwind (mobile-optimized) |
| Static content + form | Astro + Tailwind |
| Real-time app | Next.js + Pusher / Ably / native WS |

### Variant for non-React projects

ถ้าลูกค้ามี preference อื่น:

| Framework | Suggested companion stack |
|---|---|
| **Vue** | Nuxt + Tailwind + VueUse |
| **Svelte** | SvelteKit + Tailwind |
| **Angular** | Angular + Tailwind + Angular Material |
| **Plain HTML/JS** | Vite + Tailwind + vanilla JS modules |

---

## Option C — Client mandates specific framework but no codebase

**Scenario:** ลูกค้าบอก "ต้องใช้ Vue" หรือ "ต้องใช้ WordPress block" แต่ไม่มี existing code

**Approach:**
1. Confirm with PM ว่า requirement นี้ hard requirement หรือ preference
2. ถ้า hard → adopt that framework + use modern companion (Tailwind + their ecosystem)
3. ถ้า preference → present options + trade-off (e.g., "Vue ได้, แต่ team Sellsuki productive กว่าใน React — เลือกได้")
4. Lock at Stage 1, document rationale

---

## Mixing rules

| Situation | Rule |
|---|---|
| Mix multiple frameworks in single project | ❌ Never |
| Mix client stack + Sellsuki picked stack | ❌ Pick one |
| Add small utility lib to client's stack | ✓ OK if needed + documented |
| Component lib + utility (Tailwind + shadcn) | ✓ Designed to coexist |
| Pure CSS + utility framework | ⚠ Pick one approach |

---

## Decision worksheet (at Stage 1)

| Question | Answer | Implication |
|---|---|---|
| Has client codebase project must integrate with? | yes / no | yes → Client stack |
| Who maintains after handoff? | Client / Sellsuki / TBD | Client → favor their stack; Sellsuki → modern default |
| Client framework preference? | specified / open / no preference | specified → match; open → recommend default |
| Multi-page / single page / static? | — | drives framework choice |
| SEO matters? | yes / no | yes → Next.js / Nuxt / Astro (SSR/SSG) |
| Real-time / interactive heavy? | yes / no | yes → SPA-leaning |
| Sellsuki team familiar with proposed stack? | yes / no | no → risk flag at Stage 1 |
| Long-term project (months/years)? | yes / no | yes → stable, well-supported tech |

หลังตอบ: pick stack, document rationale ใน `project-card.md` Section 4

---

## After Stage 1: LOCKED

Stack lock หลัง Stage 1. เปลี่ยน mid-project = scope event:
- Trigger scope conversation (Stage 5 rule)
- Update timeline + cost
- Re-baseline `project-card.md`

ห้าม switch silently. Client request เปลี่ยน mid-project → escalate to Lead.

---

## Stage 3 prompt snippet examples

When filling `templates/vibe-code-prompt.md`:

### Example A — Client's existing React stack

```
STACK: Client's existing React + their internal component library
→ Reference: [their Storybook URL OR repo path /design-system]
→ Read their conventions: file naming, folder structure, lint config
→ Map design intent to their components per vibe-design-spec.md Section 5
→ Do NOT add new dependencies unless approved
→ Reuse their utility functions (look in /utils or /lib)
```

### Example B — Sellsuki picks default stack (greenfield)

```
STACK: Next.js (App Router) + TypeScript + Tailwind CSS + shadcn/ui
→ Initialize: npx create-next-app + setup Tailwind + shadcn init
→ Component primitives from shadcn/ui (copy into /components/ui)
→ Forms: react-hook-form + Zod for validation
→ State: useState by default, Zustand only if cross-component complexity
→ Follow Next.js App Router conventions
```

### Example C — Client mandates Vue

```
STACK: Vue 3 (Composition API) + Nuxt 3 + Tailwind CSS
→ Use VueUse for composables
→ Forms with vee-validate + Zod
→ Follow Nuxt directory conventions
→ Component library: client preference, fallback to PrimeVue if neutral
```

---

## How AI helps Stage 3 with project stacks

Claude สามารถ generate code ใน stack ใดก็ตามที่ Stage 1 lock — ไม่ต้องมี MCP เฉพาะ:

| Stack | AI strength | What to provide AI |
|---|---|---|
| React + Tailwind + shadcn | Very strong | Spec + standard patterns |
| Next.js | Very strong | Spec + App Router knowledge |
| Vue / Nuxt | Strong | Spec + Vue patterns |
| Svelte | Moderate | Spec + extra examples |
| Client's custom lib | Variable | Repo path + component docs + examples |
| Obscure framework | Weak — risk | Confirm at Stage 1 feasibility |

**Tip สำหรับ client stack:**
- Show Claude a sample component from client's codebase ใน vibe-code prompt
- Claude จะ pattern-match convention ได้ดีขึ้น
- ถ้ามี Storybook URL → web_fetch ให้ Claude อ่าน

---

## Common Mistakes

- ❌ Pick stack at Stage 2/3 instead of Stage 1 → wasted variants/code
- ❌ Mix client stack + "just adding React" because Sellsuki ถนัด → frankenstein codebase
- ❌ Pick client stack without checking client's docs first → assumptions break ใน Stage 3
- ❌ Add npm packages to client repo without approval → bloat, maintenance pain
- ❌ Use unfamiliar stack without Stage 1 feasibility check → late discovery of blockers
- ❌ Default to React/Next.js automatically — ดู client signal ก่อน
- ❌ ใช้ Sellsuki DS 1.0/2.0 ใน project skill — DS เป็นของ Sellsuki internal product เท่านั้น

---

## Quick reference

| Scenario | Stack |
|---|---|
| Client has React codebase | Their React stack |
| Client has Vue codebase | Their Vue stack |
| Client neutral, generic web | Next.js + TS + Tailwind + shadcn/ui |
| Client neutral, marketing site | Next.js / Astro + Tailwind |
| Client neutral, simple form | Vite + React + Tailwind |
| Client mandate WordPress | WordPress block / theme stack |
| Sellsuki internal product | ❌ ใช้ skill อื่น (sellsuki-product-standard) |

---

## See also

- `references/project-sizing.md` — sizing affects stack complexity choice
- `templates/project-card.md` Section 4 — where stack decision is recorded
- `templates/vibe-code-prompt.md` — uses locked stack for code generation
- `templates/handoff-doc.md` Section C — stack documented for handoff
