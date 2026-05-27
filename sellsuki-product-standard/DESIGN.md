# DESIGN.md — Sellsuki Product Standard

> เอกสารอธิบาย **ทำไม** skill นี้ออกแบบมาแบบนี้ — สำหรับทีมและ Lead ที่ต้อง maintain หรือ extend ต่อ

---

## 1. Problem we're solving

ทีม Designer/UXUI ของ Sellsuki รับงานเป็น **Card-based**: PO หรือ AI build card → ส่ง Epic/Story มาให้ → designer ต้องเริ่ม flow ตั้งแต่ research จนถึง vibe code

**ปัญหาที่ standard เดิมไม่ตอบโจทย์:**

| ปัญหาเดิม | ผลที่ตามมา |
|---|---|
| Workflow เป็น generic 5-phase (Discover → ... → Measure) | ไม่ตรงกับงานจริงที่เริ่มจาก card อยู่แล้ว — "Discover" ของจริงทำตอน PO ไม่ใช่ designer |
| ไม่มีตำแหน่งของ AI prototype / AI usability test | ทำกันอยู่แต่ไม่มี standard — แต่ละคน prompt ต่างกัน, output ต่างกัน |
| ไม่มี hook สำหรับ Vibe Code | ปลายทางจริงคือ code ที่ใช้ DS — แต่ workflow เดิมจบที่ Figma handoff |
| Designer ต้องวาง plan เองทุก card | เสียเวลา, plan ไม่ consistent ข้ามคน |
| ไม่มี machine-readable trigger | AI tools (Claude) ใช้ standard อัตโนมัติไม่ได้ |

---

## 2. Design goals

| Goal | Why |
|---|---|
| **AI-first orchestration** | Claude เป็น co-designer จริง ๆ ไม่ใช่แค่ assistant — skill ต้องให้ Claude run flow ได้เอง |
| **Card-as-entry** | Trigger คือ Jira card, ไม่ใช่ "ผู้ใช้บอก Claude ว่าจะทำอะไร" |
| **Auto-plan, ask only at gates** | ลด friction — ผู้ใช้ confirm ที่จุดสำคัญพอ |
| **Stage selection by size** | S/M/L card ไม่ควรใช้ effort เท่ากัน |
| **DS1/DS2 explicit** | Sellsuki มี 2 design system — flow ต้องบังคับเลือกชัด |
| **Loop ได้สำหรับ Product, hard-stop สำหรับ Project** | คงคุณลักษณะของ track เดิมไว้ |
| **Backward compatible mindset** | Designer ที่เคยใช้ standard เดิมไม่ต้องเรียนใหม่หมด — concept (gate, owner level, template) ยังเดิม |

---

## 3. Why 6 stages (not 5, not 7)

Workflow ของทีมจริง:
```
PO/AI Card → UXUI Research → User Journey → IA → Wireframe → Prototype → AI Usability Test → Improve → Vibe Code
```

มาย่อให้เป็น 6 stage ที่ Claude execute ได้ชัด:

| User's mental model | Maps to stage |
|---|---|
| PO/AI build card | **Stage 0 — Intake** (parse + classify) |
| Research + User Journey | **Stage 1 — Research** (รวม journey + persona signals) |
| IA + Wireframe + Prototype | **Stage 2 — Design** (3 sub-steps แต่ flow เดียว: IA → Wire → AI Proto) |
| Usability Test via Persona AI | **Stage 3 — AI Usability** (แยกออกเพราะเป็น insertion point ของ AI ที่ใหม่และต้อง standard) |
| Improve / Final | **Stage 4 — Refine** (apply findings) |
| Vibe Code DS1/DS2 | **Stage 5 — Vibe Code** (แยกเพราะ output คือ code ไม่ใช่ design) |

**ทำไมไม่รวม IA/Wire/Proto แยกเป็น 3 stage?**
เพราะใน practice มันเป็น iteration เดียวกัน — Claude สามารถ generate ทั้ง 3 จาก research output ได้ในรอบเดียว แยกเป็น 3 จะ slow flow ลงโดยไม่จำเป็น

**ทำไมแยก AI Usability ออกจาก Refine?**
เพราะมันเป็น input gate — ต้องมี persona result ก่อนถึงจะรู้ว่าจะ refine อะไร และเป็นจุดที่ user ต้อง confirm persona ก่อน run

---

## 4. Why "AI Usability Test" gets its own stage

User เลือกว่า "ยังไม่มีมาตรฐาน — ให้แนะนำ" สำหรับ persona AI

**ที่ตัดสินใจให้เป็น Claude-based (prompt-based personas):**

| เหตุผล | รายละเอียด |
|---|---|
| **เข้ากับ tool stack ที่ใช้อยู่** | ทีมใช้ Claude อยู่แล้วทุกขั้น — persona AI เป็น natural extension |
| **Zero new vendor cost** | ไม่ต้อง subscribe Maze/UserTesting/Figma Make เพิ่ม |
| **Iterate ได้เร็ว** | ปรับ persona prompt = แก้ markdown ไฟล์, ไม่ต้อง re-record |
| **Versionable** | persona library อยู่ใน repo เดียวกัน, diff ได้ |
| **Composable** | run หลาย persona แบบ parallel ก็ได้, hybrid (Claude + real user) ก็ได้ |
| **Honest about limits** | ของ Sellsuki ในตอนนี้ — เริ่มแบบนี้ก่อน, ถ้าโตค่อย integrate Maze ทีหลัง |

**สิ่งที่ standardize ใน `references/ai-persona-library.md`:**
- Persona prompt template (background, goal, frustrations, tech-savviness)
- การ run: paste prototype description → ask persona to walk through → log friction
- Output format: standardized `persona-test-result.md`

---

## 5. Why Stage 0 (Intake) parses Jira specifically

User บอกว่า Card มาจาก **Jira/Atlassian** เป็นหลัก

ผมเลย:
- ตั้ง Stage 0 ให้รู้จัก Jira URL pattern + Jira key pattern
- ใช้ Atlassian MCP tool ที่ Claude มีอยู่แล้ว (`getJiraIssue`, `searchJiraIssuesUsingJql`) — auto-fetch ไม่ต้อง paste
- เตรียมโครงสำหรับ Confluence (research artifacts มักอยู่ที่นั่น)
- ใน `references/jira-parsing.md` อธิบายการ extract: summary, description, AC, attachments, linked issues, parent epic

ถ้าทีม migrate ไป Linear/Notion ภายหลัง: เพิ่มไฟล์ใหม่ `references/linear-parsing.md` แล้วอัปเดต SKILL.md trigger pattern — ไม่ต้อง rewrite ทั้ง skill

---

## 6. Track distinction — Product vs Project

คงไว้จาก standard เดิมเพราะยังเป็น distinction ที่ใช้ได้:

| | Product track | Project track |
|---|---|---|
| Examples | Sellsuki core platform, internal tools | Client work, one-off integrations |
| Stage 5 → next | Loop ไป Stage 0 (เปิด card ใหม่จาก learning) | Hard stop + post-launch report |
| Usability test | Lighter, faster iteration | Heavier, sign-off |
| Gate strictness | Flexible | Strict |

ที่เปลี่ยน: **Measure phase หายไปเป็น stage แยก** — เอา measure logic ไปฝังใน Stage 5 (vibe code → release → log) และใน `design-retro.md` (post-launch) เพราะใน flow AI-first การ measure เป็น check-in มากกว่า phase

---

## 7. Stage selection matrix — เหตุผล

ทำไมต้องมี S/M/L matrix?

**ปัญหาเดิม:** designer รัน full flow ทุก card → S-card (เช่น "เปลี่ยน copy ของปุ่ม") ก็ทำ user journey เต็ม → เสียเวลามาก

**Matrix ตัดสินใจให้:**
- S = skip research, skip usability test (ถ้า flow ไม่เปลี่ยน), direct vibe code
- M = full flow, แต่ usability test 1-2 personas พอ
- L = full flow + competitive research + 3+ personas + multiple refine cycles

**ใครเป็นคนตัดสิน S/M/L?**
Claude เดาก่อนจาก signals (story points ถ้ามี, จำนวน AC, ความซับซ้อนของ description) — แสดงให้ user ดูใน plan summary — ถ้า user disagree ค่อยเปลี่ยน

ตรรกะอยู่ใน `references/card-classification.md`

---

## 8. DS1 vs DS2 — เหตุผลที่ทำเป็น explicit gate

Sellsuki มี 2 design systems:
- **DS 1.0** — legacy, React-only, ใช้ใน product เดิม
- **DS 2.0 (ssk-* Lit components)** — current, multi-framework, support brand variants (patona, ccs3, oc2plus)

**ปัญหาเดิม:** designer/vibe-coder ใช้สลับกันโดยไม่มี rationale → component mix, design debt

**ใน Stage 5 บังคับให้ระบุ:**
- DS1 หรือ DS2?
- ถ้า DS2: brand variant ไหน?
- เหตุผล (อ้าง `references/ds-selection-guide.md`)

Claude จะ suggest ให้ก่อนแล้ว user confirm — เป็น gate ที่ user ต้องผ่านก่อน vibe code

---

## 9. Trade-offs ที่รับไว้

| Trade-off | สิ่งที่เสียไป | สิ่งที่ได้ |
|---|---|---|
| AI-first persona | Real user signal | Speed, iteration cost ต่ำ, standardize ได้ |
| 6 stages (ไม่ใช่ 3 แบบ minimal) | Slight overhead สำหรับ S-card | Discipline + traceability |
| Auto-plan + confirm-at-gate (ไม่ confirm ทุก step) | User อาจ "ตามไม่ทัน" บางจุด | Speed, ลด friction |
| Templates เยอะ (7+ files) | Maintenance load | ความ consistent ของ output ข้ามคน/ข้าม card |
| ผูกกับ Jira | ทีมที่ใช้ tool อื่นต้อง adapt | Auto-fetch ได้, deep integration |

---

## 10. Migration จาก standard เดิม

| ไฟล์เดิม | ไฟล์ใหม่ที่แทน | หมายเหตุ |
|---|---|---|
| `workflow/overview.md` | `SKILL.md` (Flow section) | รวม overview เข้า SKILL.md เพื่อ progressive disclosure |
| `workflow/phase-discover.md` | `workflow/stage-0-intake.md` + `stage-1-research.md` | Split: PO ทำ discover, designer ทำ research |
| `workflow/phase-define.md` | รวมใน `stage-0-intake.md` (parse AC) และ `stage-1-research.md` | Define ไม่ใช่ phase แยก — มันคือผลลัพธ์ของ intake parsing |
| `workflow/phase-design.md` | `workflow/stage-2-design.md` | เพิ่ม IA + AI prototype |
| `workflow/phase-deliver.md` | `workflow/stage-5-vibe-code.md` | "Deliver" คือ vibe code ในยุค AI |
| `workflow/phase-measure.md` | ฝังใน `stage-5-vibe-code.md` (post-release) + `templates/design-retro.md` | ไม่เป็น phase แยก |
| `templates/problem-brief.md` | `templates/intake-brief.md` | Rename, adapt fields |
| `templates/design-spec.md` | `templates/design-spec.md` | คงไว้ — ยัง relevant |
| `templates/design-critique.md` | (removed) | Critique กลายเป็น activity ใน Stage 4 ไม่ใช่ document แยก |
| `templates/design-retro.md` | `templates/design-retro.md` | คงไว้สำหรับ Product track |
| `templates/design-backlog-item.md` | (removed) | Backlog อยู่ใน Jira อยู่แล้ว — ไม่ duplicate |
| `rules/standard-team.md` | `rules/standard-team.md` | คงเดิม + เพิ่ม rule เกี่ยวกับ AI usability + DS selection |
| `rules/standard-master.md` | `rules/standard-master.md` | คงเดิม + เพิ่ม governance ของ persona library |

---

## 11. Open questions (ต้อง iterate)

- [ ] Persona library จะมีกี่ persona ตอนเริ่ม? — ตอนนี้ propose 4: power user, new user, mobile-first, edge-case user
- [ ] Stage 3 ต้องการ approval ของใครเป็น minimum? — ตอนนี้ให้ designer self-run, Lead review สำหรับ L-card
- [ ] Vibe code ใช้ Claude in repo (Claude Code) หรือ Claude.ai? — ตอนนี้ skill agnostic, prompt ใน `vibe-code-prompt.md` ใช้ได้ทั้งสอง
- [ ] DS2 brand selection (patona/ccs3/oc2plus) จะ auto-detect จาก parent epic ได้ไหม? — ยังต้อง user confirm

---

## 12. Success criteria ของ skill นี้

วัดจาก:

1. **Trigger accuracy** — Claude ใช้ skill ตอนเจอ Jira card > 90% ของกรณี
2. **Plan-to-execution match** — สิ่งที่ Claude plan ตรง flow จริงที่ designer ทำ > 80%
3. **Time to first wireframe** — จาก card → wireframe < 1 ชั่วโมงสำหรับ M-card
4. **DS consistency** — vibe-coded UI ใช้ token จาก DS เท่านั้น, no hardcode
5. **Retro feedback** — designer บอกว่า skill ช่วยลด cognitive load ของการ "เริ่มงาน"

หลังใช้ 4-6 สัปดาห์: รัน retro, iterate skill — ดู rules/standard-master.md ข้อ Y4 (measure adoption)
