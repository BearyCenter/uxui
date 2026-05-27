# Handoff Doc

> Final deliverable ของ Stage 6 — เป็น **single source of truth** สำหรับ post-handoff
> ออกแบบให้ extension-ready — future BE/QA phase plug in ผ่าน Section F

---

## Cover

**Project:** `[name]`
**Client:** `[company]`
**Handoff date:** `YYYY-MM-DD`
**Designer (lead):** `[name]`
**PM:** `[name]`
**Status:** `Ready for receiver / Acknowledged / Closed`

---

# Section A — Project Summary

**Objective (final):**
`[1-2 paragraphs — what was built and why]`

**Scope (final):**
- Deliverable 1
- Deliverable 2
- Deliverable 3

**Out of scope (confirmed):**
- Item 1
- Item 2

**Timeline (actual):**
| Stage | Plan | Actual |
|---|---|---|
| 0 Brief Intake | Day 1 | Day 1 |
| 1 Research & Plan | Day 2-3 | Day 2-3 |
| 2 Vibe Design | Day 4-6 | Day 4-7 (+1) |
| 3 Vibe Code | Day 7-10 | Day 8-11 (+1) |
| 4 Deploy | Day 11 | Day 12 |
| 5 Test & Improve | Day 12-17 | Day 13-18 |
| 6 Handoff | Day 18 | Day 19 |

**Sign-off reference:** `[link to client sign-off message]`

---

# Section B — Design

**Design system used:** `DS 1.0 / DS 2.0 (variant) / Client stack`
**Rationale:** `[from research-plan]`

**Style tokens:**
| Token | Value |
|---|---|
| Primary color | `#...` |
| Secondary color | `#...` |
| Accent | `#...` |
| Heading font | `[font + weight]` |
| Body font | `[font + weight]` |
| Spacing base | `[N px]` |
| Border radius | `[N px]` |
| Shadow | `[token]` |

**Component inventory:**
| Component | Variants used | Count |
|---|---|---|
| | | |

**Design files:**
- Final design spec: `[link to vibe-design-spec.md]`
- Variants (Stage 2): `[archive link]`
- Figma file (if any): `[link]`
- Live prototype: `[staging URL]`

**Brand asset mapping:**
- Logo: `[where used in code]`
- Color tokens: `[file path]`
- Font: `[loaded from where]`

---

# Section C — Code

**Repository:**
- URL: `[repo link]`
- Default branch: `[main / master]`
- License: `[if applicable]`

**Stack:**
- Framework: `[Next.js / Vite / Vue / ...]`
- Language: `[TypeScript / JavaScript]`
- Component library: `[DS1 / DS2 / client lib]`
- State management: `[useState / Redux / Pinia / ...]`
- Routing: `[Next.js / React Router / ...]`
- Build tool: `[Vite / Webpack / ...]`

**Dependencies of note:**
| Package | Purpose | Notes |
|---|---|---|
| | | |

**Install & run:**
```bash
git clone {repo-url}
cd {repo}
{install command}     # e.g., npm install
{dev command}         # e.g., npm run dev
{build command}       # e.g., npm run build
```

**Environment variables:**
| Var | Required? | Example | Notes |
|---|---|---|---|
| API_URL | yes | https://api.example.com | staging vs prod |
| AUTH_TOKEN | yes | jwt... | |
| | | | |

**Folder structure (top-level):**
```
src/
├── components/    — UI components
├── pages/         — route pages
├── api/           — API client + mock layer
├── styles/        — global styles + tokens
├── utils/         — helpers
└── ...
```

**Known limitations / TODOs:**
- `[ ]` `[TODO ที่ marked ใน code]` — file: `[path:line]`
- `[ ]` `[limitation 2]`

**Test coverage:**
- Unit tests: `[yes / no / partial]`
- Integration tests: `[yes / no]`
- E2E tests: `[yes / no]`

---

# Section D — Deployment

**Current staging URL:** `[link]`
**Access type:** `Public / Password / SSO / IP allowlist`
**Hosted on:** `Vercel / Netlify / Sellsuki cloud / Client infra`

**Production deploy guide:**

ถ้ายังไม่ deploy production:
1. Step 1
2. Step 2
3. ...

**Domain / DNS:**
- Staging: `[domain]`
- Production: `[planned domain]`
- DNS provider: `[where to manage]`

**Rollback procedure:**
- Vercel/Netlify: rollback via dashboard (last N deploys retained)
- Cloud: `[specific procedure]`

**Credentials transfer:**
- Method: `[1Password vault shared / secure email / in-person]`
- Receiver: `[name + email]`
- Confirmation: `[receiver acknowledged on YYYY-MM-DD]`

---

# Section E — Maintenance

**Who can do what:**
| Action | Who | How |
|---|---|---|
| View staging | Client team | URL + creds |
| Update content | `[client role]` | `[CMS / direct edit]` |
| Deploy new version | `[role]` | `[CI/CD / manual]` |
| Manage env vars | `[role]` | `[dashboard]` |

**Update procedure:**
- For content: `[how]`
- For code: `[how]`

**Component update sources:**
- DS: when Sellsuki releases DS update, follow `[link to migration docs]`
- Other libraries: standard `npm update`

**Issue reporting:**
- Post-handoff support: `[N days from handoff, per contract]`
- Channel: `[email / Slack / ticket system]`
- SLA: `[response time]`
- After support window: `[what then]`

---

# Section F — Future Phase Hooks

> 🔑 **IMPORTANT** — Section นี้สำคัญสำหรับ future Sellsuki BE/QA team หรือทีมต่อ pickup ได้

## F1 — Backend Phase Pickup

**Mock data location:**
- Folder: `[src/mocks/ or wherever]`
- Format: `[JSON fixtures / msw handlers / inline data]`

**Swap points (replace mock with real API):**

| Endpoint | Method | Currently | Mock file | Target |
|---|---|---|---|---|
| `/api/orders` | GET | mock | `mocks/orders.json` | `[real endpoint]` |
| `/api/orders/:id` | GET | mock | `mocks/order-detail.json` | |
| `/api/auth/login` | POST | mock | `mocks/auth.js` | |
| | | | | |

**API contract (expected by frontend):**

> Document expected request/response shape — BE team builds to this

```typescript
// GET /api/orders
type OrdersResponse = {
  data: Order[];
  total: number;
  page: number;
};

type Order = {
  id: string;
  // ...
};
```

หรือ link ไป OpenAPI / Swagger / Postman collection

**Auth integration point:**
- Current: `[mock auth / no auth]`
- Future: `[expected — JWT / OAuth / session]`
- File: `[where to plug auth in]`

**State management style:**
- Current: `[pattern used]`
- BE integration: `[where API calls live, where state syncs]`

**Pre-marked TODO in code:**
- Search for `// TODO: BE-INTEGRATION` to find all swap points
- Each marked with: endpoint, expected behavior, mock currently returning

---

## F2 — QA Phase Pickup

**Test scenarios:**
> Full list of scenarios that should be covered in formal QA

| # | Scenario | Type | Last verified by | Status |
|---|---|---|---|---|
| 1 | User login | Functional | Designer (Stage 5) | pass |
| 2 | View order list | Functional | Designer (Stage 5) | pass |
| 3 | Export to CSV | Functional | Designer (Stage 5) | pass |
| 4 | Search by ID | Functional | Designer (Stage 5) | pass |
| 5 | Permission denied state | Edge | Designer (Stage 5) | pass |
| | | | | |

**Manual test checklist:**

ใช้ภายใต้ formal QA pipeline:
- [ ] All scenarios above
- [ ] All forms validation
- [ ] All error states
- [ ] All loading states
- [ ] Empty states
- [ ] Long content handling
- [ ] Network failure handling
- [ ] Browser back/forward
- [ ] Page refresh state preservation
- [ ] Concurrent edit
- [ ] Permission boundary

**Known edge cases (documented):**
- `[edge case 1]` — behavior: `[...]`
- `[edge case 2]` — behavior: `[...]`

**Browser / device support claim:**
| Browser/Device | Tested? | Status |
|---|---|---|
| Chrome desktop | yes | pass |
| Safari desktop | yes | pass |
| Firefox desktop | yes | pass |
| Edge desktop | partial | minor issues |
| Mobile Chrome (Android) | yes | pass |
| Mobile Safari (iOS) | yes | pass |
| Tablet | yes | pass |

**Accessibility audit:**
- WCAG level claimed: `AA / AAA / partial`
- Tools used: `[Lighthouse / axe / manual]`
- Results: `[summary]`
- Known issues: `[list]`

**Performance baseline:**
- Lighthouse desktop: `[score]`
- Lighthouse mobile: `[score]`
- Page weight: `[KB]`
- TTI: `[ms]`

---

# Section G — Handoff Verification

**Receiver verification checklist:**

- [ ] Repo access verified (receiver can clone)
- [ ] Fresh clone + install + run works
- [ ] All links in this doc resolve
- [ ] Credentials received via secure channel
- [ ] Staging URL accessible
- [ ] Design files accessible
- [ ] Section F understood (especially TODO markers)

**Receiver acknowledgment:**
- Receiver: `[name + email]`
- Date acknowledged: `YYYY-MM-DD`
- Method: `[Slack / email / signed doc]`

---

# Section H — Project Close

**Closed by:** `[name]`
**Date closed:** `YYYY-MM-DD`
**Total cost (hrs):** `[N]` — vs estimate: `[N]`
**Sign-off message:** `[link / quote]`

**Retro:** see `templates/design-retro.md`

---

## Appendix

**Original PM Card:** `[link]`
**Research Plan:** `[link]`
**Vibe Design Spec:** `[link]`
**Test Reports:** `[links]`
**Improvement Log:** `[link]`
**Change Orders:** `[links]`
**Communication log archive:** `[link]`
