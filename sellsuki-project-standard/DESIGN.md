# DESIGN.md — Sellsuki Project Standard

> เอกสารอธิบาย **ทำไม** skill นี้ออกแบบมาแบบนี้ และทำไมแยกจาก `sellsuki-product-standard`

---

## 1. Problem this skill solves

ทีม Project ของ Sellsuki ทำ **client work** (agency-style) — รับ brief จาก PM ที่คุยกับลูกค้ามา ต้องส่งงานเป็น deliverable ให้จบ

**ปัญหาที่ skill เดิม (product-standard) ไม่ตอบ:**

| ปัญหา | เหตุผล |
|---|---|
| Source งานต่างกัน | Product = Jira; Project = PM brief (Word/Slack/voice/email) — unstructured |
| Stakeholder ต่างกัน | Product = internal stakeholder; Project = ลูกค้าภายนอก ที่ต้อง sign-off |
| Iteration model ต่างกัน | Product = loop ต่อเนื่อง; Project = linear, จบที่ handoff |
| Deploy = first-class | Product flow ฝัง deploy ใน vibe code; Project ต้อง explicit เพราะลูกค้าใช้ staging URL |
| Variant thinking | Product สร้าง 1 solution; Project สร้าง 2+ variants ให้ลูกค้าเลือก |
| Stack choice กว้างกว่า | Product ผูก DS1/DS2; Project อาจใช้ stack ของลูกค้า |
| Handoff ≠ ship | Product จบที่ ship + measure; Project จบที่ส่งงานให้ลูกค้าหรือทีมต่อไป |
| Future BE/QA hook | Project มีแผนเพิ่ม BE/QA phase — design ต้อง extension-ready |

---

## 2. ทำไมแยก skill (ไม่ใช่ flag ใน skill เดียวกัน)

พิจารณาแล้ว: **แยกเป็น 2 skill** ดีกว่า

| Option | ข้อดี | ข้อเสีย |
|---|---|---|
| **1 skill + track flag** | Code reuse, central rules | Description ยากขึ้น, trigger ปนกัน, file ใหญ่เกินไป |
| **2 skills แยก** (เลือก) | Trigger ชัด, evolve อิสระ, file size เหมาะ | ต้อง maintain ทั้งคู่, อาจ duplicate บางส่วน |

**เหตุผลที่เลือกแยก:**
- Trigger ต่างกันชัดเจน — Jira vs PM brief — model ตัดสินใจง่ายกว่า
- Workflow ต่างพอจน "track flag" ในไฟล์เดียวจะทำให้ทุก stage ต้องมี if/else
- Project skill จะ evolve เร็วกว่า (BE/QA จะมาเพิ่ม) — แยกไว้ไม่กระทบ product

**Cross-reference** ที่จงใจ:
- DESIGN docs อ้างถึงกันได้
- Persona library duplicate แต่ customize (project user = client's user, ไม่ใช่ Sellsuki merchant)
- DS guide เหมือนกัน, แต่ project มี option ใช้ client stack

---

## 3. ทำไม 7 stages

User กำหนด flow:
```
Brief PM req → PM Card → Research (plan AI) → Vibe Design → Vibe Code → Deploy → Test → Improve → Handoff
```

แปลงเป็น 7 stages โดย **รวม Test + Improve เป็น 1 stage** เพราะใน practice มันเป็น loop เดียวกัน (test → improve → re-test → improve → ...):

| User flow | Maps to stage |
|---|---|
| Brief PM req → PM Card | **Stage 0 — Brief Intake** |
| Research (plan AI) | **Stage 1 — Research & Plan** |
| Vibe Design | **Stage 2 — Vibe Design** |
| Vibe Code | **Stage 3 — Vibe Code** |
| Deploy | **Stage 4 — Deploy** |
| Test + Improve | **Stage 5 — Test & Improve** (loop) |
| Handoff | **Stage 6 — Handoff** |

7 stages — ใกล้เคียงกับ product (6 stages) แต่มี Deploy explicit

---

## 4. ทำไม Variant thinking ใน Stage 2

Product flow สร้าง 1 wireframe → iterate
Project flow สร้าง **2+ variants** → ลูกค้าเลือก → iterate ตัวที่เลือก

**เหตุผล:**
- Project = subjective taste ของลูกค้าหนักกว่า
- ลูกค้าตัดสินใจง่ายกว่าจาก "เลือก 1 จาก 2" มากกว่า "feedback บน 1"
- ลด rework — เลือกผิด direction ตั้งแต่ต้นใหญ่กว่า fix detail
- AI สร้าง variant เร็ว — cost ต่ำ, benefit สูง

**Variant guideline:**
- 2 ตัวสำหรับ S/M
- 3 ตัวสำหรับ L (ถ้าลูกค้า OK กับการเลือก)
- ห้ามมีตัวที่ "weak option" ที่สร้างมาเป็น contrast — ทุก variant ต้อง defendable

---

## 5. ทำไม Deploy เป็น stage แยก

Product flow: deploy ฝังใน vibe code (เพราะมี CI/CD ที่ Sellsuki standard)
Project flow: deploy แยก เพราะ

- Staging environment ของแต่ละลูกค้าต่างกัน
- Access setup (auth, domain, SSL) ต้องทำเอง
- Client ใช้ staging URL ให้ feedback — เป็น artifact เอกเทศ
- Sometimes deploy ไป client's own infrastructure (ไม่ใช่ Sellsuki cloud)

Stage 4 มี checklist ของ environment setup, auth, access — ไม่ assume CI/CD พร้อมเสมอ

---

## 6. ทำไม UAT round budget

Product flow: iterate ไม่จำกัด (เพราะ internal)
Project flow: **set UAT round limit upfront** (เพราะ commercial)

**Default budget:**
- S = 1 round
- M = 2 rounds
- L = 3 rounds

เกิน → trigger **scope conversation** กับ PM:
- Out of scope? → change order
- In scope but underestimated? → eat the cost, document for retro
- Scope creep? → push back

ไม่มี budget = project ไม่จบ = pain ทั้งทีม + ลูกค้า

---

## 7. ทำไม Handoff เป็น hard stop (ตอนนี้)

User บอกชัด: "phase มีแผนพัฒนาให้ทีมจบงานได้ในอนาคต ฉะนั้นตอนนี้จบที่ handoff"

**แปลว่า:**
- ตอนนี้ Sellsuki Project team = design + frontend vibe code
- BE และ QA phase ยังไม่มีในทีม → handoff ให้ client หรือทีมอื่นต่อ
- Future: BE/QA จะมาเป็น Phase 7-8 → handoff doc ต้อง extension-ready

**Design implication ของ handoff:**
- Handoff doc structure มี section placeholder สำหรับ BE/QA pickup
- Code repo organize เป็น layer-ready (FE clear, BE integration points marked)
- ทำให้ "future Sellsuki BE/QA" สามารถ plug in โดยไม่ต้อง redesign handoff

ดู `references/handoff-extension-plan.md`

---

## 8. ทำไม Variants ใน Stage 2 แต่ไม่มี AI Usability Test

Product skill มี Stage 3 AI Usability (persona-based)
Project skill **ไม่มี** stage แยก เพราะ:

1. **Client UAT ทำหน้าที่นี้แทน** — ลูกค้า test แทน persona
2. **Client knows their users** — feedback จาก client มี weight สูงกว่า simulated persona
3. **Time pressure** — project มี timeline หนักกว่า, AI usability ใช้เวลาเกิน
4. **Variant pick = แก้ direction-level friction ตั้งแต่ Stage 2** — ลด need ของ usability test

**Exception** — สำหรับ L/Enterprise project ที่ scope ใหญ่:
- สามารถ insert mini AI usability test ใน Stage 2 (ก่อน present variants ให้ client)
- ดู Stage 2 doc

---

## 9. Trade-offs ที่รับไว้

| Trade-off | เสียอะไร | ได้อะไร |
|---|---|---|
| ไม่มี AI Usability dedicated stage | บาง friction หลุดผ่าน | Speed, client UAT compensate |
| Variant thinking | Effort ใน Stage 2 หนักขึ้น | Decision คุณภาพดีขึ้น, rework ลด |
| Deploy เป็น stage แยก | One more gate | Visibility, client gets shareable URL |
| UAT round budget | Less flexibility | Scope discipline, finite project |
| Hard stop ที่ handoff | ไม่มี post-launch measure | Project economics ชัด, future phase plug-in ได้ |
| Stack flexibility (ไม่บังคับ DS) | Less DS adoption ใน project | ลูกค้าได้สิ่งที่ใช้ได้กับ infra ของเขา |

---

## 10. การตัดสินใจสำคัญ

| Decision | ทำไม |
|---|---|
| ไม่มี Backlog template | Project = linear; backlog อยู่ใน PM tool ของ Project team อยู่แล้ว |
| มี Improvement Log template | UAT cycles ต้องการ structured tracker — ลูกค้า feedback หลาย channel |
| Handoff doc รวม Design + Code + Access | One artifact ให้ลูกค้า, ลด follow-up |
| Persona library duplicate (ไม่ shared) | Persona ของ project = client's end users — context ต่างจาก product |
| DS selection guide reference ของ product | DS เหมือนกัน, ไม่ duplicate logic |

---

## 11. Open questions (iterate)

- [ ] Stack ของ client ที่นอก DS — มี allowlist ไหม? (เช่น Tailwind OK, custom CSS framework ไม่ OK)
- [ ] UAT budget default ใครเป็นคนกำหนด — PM หรือ Designer? — ตอนนี้ default Designer propose, PM confirm
- [ ] Deploy ไป client infra (vs Sellsuki cloud) — ต้องการ runbook ไหม? — ตอนนี้ใน Stage 4 มี checklist generic
- [ ] BE/QA phase จะ trigger ภายในไฟล์เดียวกับ skill นี้ หรือเป็น skill ใหม่? — ตอนนี้ assume แยก skill เมื่อ phase พร้อม
- [ ] Client communication template ภาษาอังกฤษ vs ไทย — ตอนนี้ default ไทย, user สลับเองได้

---

## 12. Migration / Coexistence กับ product-standard

ทั้ง 2 skills **อยู่ร่วมกันได้** — Claude แยกตาม trigger:

| Signal | Skill |
|---|---|
| Jira URL/key | product-standard |
| PM brief / client mention | project-standard |
| Ambiguous (เช่น "design ตัวนี้") | ถามว่า "งานนี้มาจาก Jira หรือ PM brief?" |

**Cross-reference ที่ allowed:**
- Project skill อ้าง `references/ds-selection-guide.md` จาก product (DS เหมือนกัน) — แต่ในตัวอย่างนี้ duplicate เพื่อ self-contained
- Persona library: ต่างกัน — Project = client's user, Product = Sellsuki merchant

ถ้า refactor ในอนาคต: shared library อาจมาอยู่ใน `common/` แล้วทั้งสอง skill อ้างถึงได้

---

## 13. Success criteria ของ skill

1. **Trigger accuracy** — Claude เลือก project skill (ไม่ใช่ product) เมื่อเจอ PM brief > 90%
2. **PM Card completeness** — Stage 0 output ใช้ได้โดยไม่ต้องถาม PM กลับ > 80%
3. **Variant adoption rate** — Stage 2 ลูกค้าเลือกได้ใน 1 รอบ > 70%
4. **UAT budget respected** — projects ที่จบใน budget > 80%
5. **Handoff completeness** — ลูกค้า + future BE/QA pickup ได้โดยไม่ติดต่อกลับ > 90%
6. **Time to deploy** — จาก brief → staging URL < 1 week สำหรับ M-project

หลังใช้ 6 weeks: รัน retro กับทีม → iterate
