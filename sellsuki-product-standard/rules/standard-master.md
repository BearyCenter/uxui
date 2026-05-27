# Standard Master — Level 2 (Lead → Principal)

**Purpose:** ออกแบบ system, governance, และ direction ที่ทำให้ทีมทำงานได้ดีขึ้นในระดับ scale — รวมถึง AI tooling และ DS

---

## Strategy & Direction Rules

| # | Rule | Pass | Fail |
|---|---|---|---|
| S1 | แปล business OKR → design principle ที่ทีม act on ได้ | principle มี action ชัด | แค่ statement |
| S2 | กำหนด design direction cross-product โดยไม่ขัดแย้ง | align ทุก squad | แต่ละ squad ทำต่าง |
| S3 | Align design roadmap กับ product + tech roadmap | shared roadmap | แยกกัน |
| S4 | รู้ว่า initiative ไหน invest heavy / fast & good enough | มี decision record | ทุก initiative effort เท่ากัน |

---

## System & Scale Rules

| # | Rule | Pass | Fail |
|---|---|---|---|
| Y1 | DS มี token architecture, component governance, versioning | documented + enforce | สร้างแต่ไม่ governance |
| Y2 | Impact ของการเปลี่ยน pattern ต่อ product ทั้งหมด ประเมินก่อนทำ | impact assessment | เปลี่ยนแล้วค่อยดู |
| Y3 | Standard ที่สร้างต้อง self-serve | documentation + example | ทีมต้องถามทุกครั้ง |
| Y4 | Measure DS adoption + skill usage | มี adoption metric | สร้างแล้วไม่วัด |
| Y5 | DS1 → DS2 migration plan ชัด — ไม่ migrate แบบ ad-hoc | roadmap + criterion | ใครอยากใช้ก็ใช้ |

---

## AI Governance Rules *(ใหม่ — เกิดจาก AI-first workflow)*

| # | Rule | Pass | Fail |
|---|---|---|---|
| AI1 | Persona library version-controlled + reviewed อย่างน้อย quarterly | mainainted in repo | persona เก่าใช้ไปเรื่อย |
| AI2 | Audit Stage 3 findings vs real-user findings เป็นระยะ | audit log | ไม่ตรวจสอบความแม่นยำ |
| AI3 | Skill version updates documented ใน DESIGN.md | change log | skill เปลี่ยนเงียบ |
| AI4 | AI prototype ที่ Claude สร้างต้อง map กับ DS component — ไม่ใช่ pattern ใหม่ | enforced via gate | AI สร้าง pattern เองและเล็ดลอด |
| AI5 | Vibe code output ต้องผ่าน DS validation (validate_usage หรือ manual audit) | 100% pass before merge | ปล่อย hardcode ผ่าน |

---

## Team & Process Rules

| # | Rule | Pass | Fail |
|---|---|---|---|
| T1 | Process เหมาะกับ team size + maturity | ต่างกันตาม context | one-size-fits-all |
| T2 | Critique culture — feedback เป็น norm | ทำเองได้ไม่ต้องนัด | กลัว feedback |
| T3 | Mentor ผ่าน pair design + skill walk-through | mentoring record | สอนแค่มีปัญหา |
| T4 | รู้ว่าเมื่อไหร่ push back, เมื่อไหร่ let go | decision framework | push/let go ตลอด |
| T5 | Skill misuse (เช่น skip stage บ่อย) ต้องเป็น signal ให้แก้ skill ไม่ใช่บังคับทีม | revision history | บังคับ compliance |

---

## Stakeholder & Influence Rules

| # | Rule | Pass | Fail |
|---|---|---|---|
| I1 | Present design decision ด้วย business language ต่อ C-level | impact, metric, risk | แค่ aesthetic |
| I2 | Negotiate scope กับ PM/Eng โดยไม่เสีย design quality หลัก | documented trade-off | ยอมทุกอย่าง / push back ทุกอย่าง |
| I3 | Voice of user — ในห้องที่ user ไม่อยู่ | อ้าง data / persona / research | assumption เท่านั้น |
| I4 | Co-create กับ Eng ตั้งแต่ Stage 2 | eng เข้าตั้งแต่ design | handoff culture |

---

## Approval Gates ที่ L2 ดู

| Gate | When | What to check |
|---|---|---|
| L-card Stage 0 plan | Before Stage 1 | size classification reasonable, parent epic context ครบ |
| Stage 4 final (L-card) | Before Stage 5 | findings applied, DS choice + brand variant rationale |
| Stage 5 major deviation | During vibe code | กระทบ task หรือ metric หรือไม่ — fix หรือ accept with plan |
| New pattern proposal | When team finds DS gap | should this become a DS component? Proposal to DS team |

---

## Hard No

- ❌ Micromanage pixel — ทำงานแทนทีมได้ทุกอย่าง = scale ไม่ได้
- ❌ ใช้ intuition อย่างเดียว — ต้อง data หรือ user insight
- ❌ ปกป้อง process เก่าเพราะ "เคยใช้ได้" — context เปลี่ยน process ต้องเปลี่ยน
- ❌ Own design decision ทุกชิ้นคนเดียว
- ❌ Design culture ที่ทีมกลัว critique
- ❌ Strategy ที่ดูดีแต่ทีมทำตามไม่ได้
- ❌ Ignore AI tool quality — persona library ที่ไม่ realistic = standard ที่ผลิต false confidence
- ❌ Approve DS1/DS2 mix ใน feature เดียวโดยไม่มี migration plan

---

## Mindset

```
Lead       → "ฉันออกแบบ process + AI tooling ให้ทีมทำงานได้ดีขึ้น"
Principal  → "ฉันกำหนด direction cross-product, สร้าง culture, และ steward DS evolution"
```

---

## Success Measure

| Level | วัดจาก |
|---|---|
| Lead | Team velocity, DS adoption rate, ลด design debt, skill trigger accuracy |
| Principal | Cross-product alignment, design culture health, DS evolution impact, AI-driven productivity gain |
