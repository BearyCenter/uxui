# Standard Team — Level 1 (Junior → Senior)

**Purpose:** ส่งงานได้ตรง spec, คุณภาพสม่ำเสมอ, ใช้ AI tooling ให้คุ้มค่า, เริ่ม own งานของตัวเอง

---

## Card Handling Rules

| # | Rule | Pass | Fail |
|---|---|---|---|
| C1 | ทุก card ต้องผ่าน Stage 0 (intake brief) — ไม่ว่าใหญ่หรือเล็ก | มี intake brief ทุก card | จับ card แล้วลุย Stage 2 เลย |
| C2 | Classify size + track ก่อนเริ่ม Stage 1 | มี rationale | ไม่ classify หรือเดา |
| C3 | Plan ของ Claude ต้องผ่านสายตาก่อน run ต่อ | อ่าน plan, confirm/adjust | ปล่อย run อัตโนมัติโดยไม่ดู |

---

## Design Quality Rules

| # | Rule | Pass | Fail |
|---|---|---|---|
| Q1 | ทุก screen ต้องมีครบ 6 states: default, loading, empty, error, success, disabled | ครบ | ขาด state ใด |
| Q2 | ใช้ DS component name (ssk-* หรือ DS1 component) ตั้งแต่ wireframe | ไม่มี generic name | "Button A", "input field" |
| Q3 | ใช้ DS token เท่านั้น — ไม่ hardcode | ไม่มี one-off | hardcode color/size |
| Q4 | Responsive ระบุครบ mobile/tablet/desktop | มี rule ทุก breakpoint | ไม่ระบุ |
| Q5 | Accessibility: WCAG AA contrast, keyboard nav, ARIA | documented | ไม่ระบุ |
| Q6 | Edge case ครอบคลุม: long text, data = 0, no permission, network error | มี spec | ไม่ระบุ |

---

## AI Usability Rules

| # | Rule | Pass | Fail |
|---|---|---|---|
| A1 | ทุก M/L card ต้องผ่าน Stage 3 ก่อน vibe code | มี persona-test-result | skip Stage 3 |
| A2 | Persona ที่ใช้ต้อง map กับ user segment จริงของ card | rationale ระบุใน research-journey | ใช้ generic persona |
| A3 | ห้ามให้ persona "succeed" — ต้องประพฤติแบบจริง | persona แสดง confusion/failure ถ้ามี | persona ทำสำเร็จเสมอ |
| A4 | Severity จัดอย่างน้อย: blocker / major / minor | severity ทุก finding | ไม่จัด priority |
| A5 | Must-fix list (blocker + major) ต้อง close ก่อน Stage 5 | spec final ไม่มี open blocker | vibe code ด้วย known blocker |

---

## Vibe Code Rules

| # | Rule | Pass | Fail |
|---|---|---|---|
| V1 | DS selection (DS1 vs DS2) explicit ก่อน Stage 5 — มี rationale | documented in spec | ไม่ระบุหรือเลือกตอน vibe |
| V2 | ใช้ DS MCP — เรียก `get_brand_rules` + `get_component` ก่อน generate | tool call log | hardcode pattern จากความจำ |
| V3 | DS2: รัน `validate_usage` หลัง generate | validation passed | ไม่รัน validate |
| V4 | Visual QA + Behavior QA หลัง vibe code | QA checklist signed | ไม่ QA |
| V5 | Deviation จาก spec ต้อง log | deviation log filled | hidden deviation |

---

## Delivery Rules

| # | Rule | Pass | Fail |
|---|---|---|---|
| D1 | Self-review ก่อน share ทุก stage output | ผ่าน self-checklist | ส่งของที่ตัวเองไม่ผ่าน |
| D2 | File naming consistent: `{card-key}_{stage}_v{n}` | consistent | "final_final_new" |
| D3 | Spec มี annotation พอที่ Claude อ่านแล้ว vibe code ได้โดยไม่ถาม | dev/AI ไม่ต้องถาม | ขาด annotation |
| D4 | Post-launch QA ที่ N+1, N+7 วัน | ทำ QA | ship แล้วจบ |

---

## Collaboration Rules

| # | Rule | Pass | Fail |
|---|---|---|---|
| L1 | Loop dev เข้ามาตั้งแต่ Stage 2 (ก่อน proto สุดท้าย) | dev เห็น direction ก่อน Stage 5 | dev เห็นครั้งแรกตอน vibe code |
| L2 | ตั้งคำถาม AC ที่ไม่ชัดที่ Stage 0 — ไม่เดา | open question ใน brief | เดาแล้วทำ |
| L3 | ตอบคำถามทีมภายในวันเดียวกัน | SLA: same day | ค้างข้ามวัน |
| L4 | Share artifact ที่ stage transition — async ใน Slack/Confluence | ทีมตามได้ | งานเงียบจน final |

---

## Ownership Rules *(แยก Junior → Senior)*

| # | Rule | Pass | Fail |
|---|---|---|---|
| O1 | รู้ success metric ของทุก card ที่ทำ | บอก metric ได้ | ไม่รู้ |
| O2 | Track metric หลัง launch — 7/14/30 วัน | มี measure record | ship แล้วจบ |
| O3 | เปิด follow-up card เองเมื่อเห็น gap | proactive | รอ PM assign |
| O4 | เสนอ update persona library / DS เมื่อเห็นว่าควรเพิ่ม | มี proposal | เห็นแล้วเฉย |
| O5 | Mentor junior ผ่าน critique stage output | มี critique session | ไม่ share knowledge |

---

## Hard No

- ❌ Vibe code โดยไม่มี final design-spec.md
- ❌ Skip Stage 3 (AI usability) สำหรับ M/L card ด้วยเหตุผลว่า "ไม่มีเวลา"
- ❌ ใช้ component นอก DS โดยไม่ปรึกษา Lead
- ❌ Hardcode color/size — แม้แค่ครั้งเดียว
- ❌ ไม่ log deviation — design debt ไม่มี trace
- ❌ Persona ที่ "succeed" ทุก test — ไม่ใช่ test ของจริง
- ❌ Run skill แบบ blind (ไม่ดู plan ของ Claude)

---

## Mindset

```
Junior  → "ฉัน execute Sellsuki standard ได้ถูกต้องทุก stage"
Mid     → "ฉัน customize stage ตามขนาด card และ direct Claude ได้"
Senior  → "ฉันเห็น gap ของ standard เอง และเสนอ update — ทั้ง process, persona, DS"
```
