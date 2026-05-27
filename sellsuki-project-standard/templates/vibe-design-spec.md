# Vibe Design Spec

> Living document — start with variants in Stage 2, finalize after client picks

---

## Meta

**Project:** `[name]`
**Version:** `v1.0`
**Date:** `YYYY-MM-DD`
**Designer:** `[name]`
**Status:** `Draft / Variants Presented / Picked / Final / In Vibe Code`

---

## Section 1 — Variants Presented (Stage 2)

### Variant A — `[Direction name]`

**1-line summary:**
`[what makes this variant different]`

**Hero screen / first impression:**
`[describe]`

**Trade-off:**
- Pros: `[...]`
- Cons: `[...]`

**Best for:** `[scenario where this variant shines]`

**Artifact link:** `[HTML artifact / Figma / Claude widget]`

**Screen list:**
1. `[screen name + 1-line purpose]`
2.

---

### Variant B — `[Direction name]`

`[same structure]`

---

### Variant C — `[if applicable, L/Enterprise]`

`[same structure]`

---

## Section 2 — Client Pick

**Picked:** `Variant A / B / C / Hybrid`

**If hybrid:** `[describe which parts from which variants]`

**Picked at:** `YYYY-MM-DD HH:MM`
**Decision context:** `[brief note — who attended decision, key reasons]`

**Adjustments requested:**
- `[change 1]`
- `[change 2]`

---

## Section 3 — Final Direction (after pick)

**Design direction (1 statement):**
> `[The product should feel X and let users do Y without Z]`

**Style identity:**
- Color: `[primary, secondary, accent]`
- Typography: `[heading + body]`
- Spacing rhythm: `[base unit]`
- Tone: `[formal / friendly / playful / ...]`

---

## Section 4 — Screen-by-screen Spec

> Repeat for each screen

### Screen: `[name]`

**Purpose:** `[why this screen]`
**Entry:** `[from where]`
**Exit:** `[to where]`

**Wireframe / structure:**
```
[ASCII or markdown table or describe layout]
```

**States:**
| State | Description | DS / client component |
|---|---|---|
| Default | | |
| Loading | | |
| Empty | | |
| Error | | |
| Success | | |
| Disabled | | |

**Interactions:**
| Element | Trigger | Action | Notes |
|---|---|---|---|
| | | | |

**Responsive:**
- Mobile: `[layout note]`
- Tablet: `[layout note]`
- Desktop: `[layout note]`

**Accessibility:**
- Contrast: `[pass AA?]`
- Keyboard: `[tab order, key behaviors]`
- ARIA: `[needed labels/roles]`

**Edge cases:**
| Scenario | Expected behavior |
|---|---|
| | |

---

## Section 5 — Component Inventory

> Used by Stage 3 vibe code prompt
>
> ตัวอย่างด้านล่างเป็น modern default stack (shadcn/ui) — ปรับตาม stack ที่ lock ใน Stage 1
> - **Client stack:** ใช้ชื่อ component ของ client's library (เช่น `<MyButton>`, `<ClientInput>`)
> - **Modern default:** shadcn (`<Button>`, `<Input>`, `<Table>`) หรือ Radix primitives
> - **Custom modern:** ตาม library ที่เลือก (PrimeVue, Headless UI, etc.)

| Component | Stack source | Variant / Props | Where used | Count |
|---|---|---|---|---|
| `<Button>` | shadcn/ui | variant=primary | every screen | 12 |
| `<Input>` | shadcn/ui | with validation | forms | 8 |
| `<DataTable>` | shadcn/ui + TanStack Table | sortable | list view | 1 |
| | | | | |

---

## Section 6 — Data & State

**State scope:**
| State | Lives in | Shared with |
|---|---|---|
| User session | global | all screens |
| Filter state | per-screen | none |
| | | |

**API endpoints needed:**
| Endpoint | Method | Used by | Mock available? |
|---|---|---|---|
| `/api/orders` | GET | Order list | yes |
| | | | |

---

## Section 7 — Cross-screen Rules

- Header behavior: `[consistent / per-screen]`
- Loading pattern: `[centralized / per-component]`
- Error pattern: `[toast / banner / modal]`
- Empty state philosophy: `[guide to action / explain context]`

---

## Section 8 — Open Decisions

> Must close before Stage 3

- [ ] `[decision]` — owner: `[role]` — due: `YYYY-MM-DD`

---

## Gate to Stage 3

- [ ] Client picked (or hybrid agreed)
- [ ] All screens spec'd (not just hero)
- [ ] States ครบ 6 ต่อ screen
- [ ] Responsive ระบุ
- [ ] Component inventory complete
- [ ] Data + API contracts documented (or mock plan)
- [ ] Open decisions = 0
