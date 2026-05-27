# IA & Wireframe Spec

> Output ของ Stage 2 — ทำซ้ำ Screens section ต่อแต่ละ screen ใน flow

---

## Meta

**Card:** `XXX-NNN`
**Date:** `YYYY-MM-DD`
**Designer:** `[ชื่อ]`
**Prototype link/artifact:** `[link หรือ note ว่าอยู่ที่ไหน]`
**DS target (tentative):** `DS1 / DS2` — final ที่ Stage 4

---

## Sitemap / Flow Map

```
[ASCII หรือ Mermaid diagram ของ flow]

Example:
Home → OrderList → [Filter] → OrderList(filtered) → [Export button]
                                                    └→ ExportDialog
                                                       ├─ Success → Download
                                                       └─ Error → Retry
```

---

## Screens

### Screen 1 — `[ชื่อ screen]`

**Purpose:** `[ทำไม screen นี้มี]`
**Entry point:** `[user มาที่นี่จากไหน]`
**Exit points:** `[user ออกไปที่ไหนได้บ้าง]`

#### Layout (wireframe)

```
[ASCII wireframe หรือ markdown table หรือ component list]

ตัวอย่าง:
┌─────────────────────────────────┐
│ ssk-header                       │
├─────────────────────────────────┤
│ ssk-page-title  ssk-button:primary│
│                                  │
│ ssk-table                        │
│   ├─ col 1, col 2, col 3        │
│   ├─ row data                   │
│                                  │
│ ssk-pagination                   │
└─────────────────────────────────┘
```

#### States

| State | What user sees | DS component(s) |
|---|---|---|
| Default | | |
| Loading | | ssk-skeleton / ssk-spinner |
| Empty | | ssk-empty-state |
| Error | | ssk-alert + ssk-button:retry |
| Success | | ssk-toast |
| Disabled | | |

#### Interactions

| Element | Trigger | Action | Notes |
|---|---|---|---|
| | click / hover / type | | |

#### Responsive

| Breakpoint | Layout change |
|---|---|
| Mobile (< 768px) | |
| Tablet (768-1024px) | |
| Desktop (> 1024px) | |

#### Accessibility

- **Contrast:** `[pass AA?]`
- **Keyboard:** `[tab order, enter/space behavior]`
- **ARIA:** `[labels, roles, live regions]`
- **Focus indicator:** `[visible? how?]`

#### Edge cases

| Scenario | Expected behavior |
|---|---|
| Text ยาวเกิน N chars | |
| Data = 0 | |
| User ไม่มี permission | |
| Network error | |

---

### Screen 2 — `[ชื่อ]`

`[repeat block]`

---

## Cross-screen rules

- Header behavior: `[เหมือนทุก screen หรือไม่]`
- Loading consistency: `[ใช้ pattern เดียวกันไหม]`
- Error pattern: `[centralized error message หรือ per-screen]`

---

## Component inventory (สำหรับ Stage 5)

| Component | Where used | DS source | Notes |
|---|---|---|---|
| ssk-button | Screen 1, 2 | DS2 | primary variant |
| ssk-input | Screen 1 | DS2 | with validation |
| | | | |

---

## Self-critique checklist

- [ ] ทุก screen ครบ 6 states (default, loading, empty, error, success, disabled)
- [ ] ใช้ DS component name (ไม่ใช่ generic)
- [ ] Edge case ครบ
- [ ] Responsive ระบุครบ
- [ ] Accessibility annotated
- [ ] ไม่มี dead-end ใน flow
- [ ] Primary action ใช้ verb label
- [ ] Empty state มี actionable next step

---

## Gate to Stage 3

- [ ] Self-critique ผ่านทุกข้อ
- [ ] Prototype runable (run happy path ไม่ break)
- [ ] Edge case ครบ
- [ ] Component inventory เสร็จ
