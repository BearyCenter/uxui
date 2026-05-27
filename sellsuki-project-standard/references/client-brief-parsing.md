# Client Brief Parsing

> วิธี Claude extract requirement จาก unstructured PM brief — Stage 0

---

## Brief formats ที่ Sellsuki Project team เจอจริง

| Format | Frequency | Parse approach |
|---|---|---|
| Slack message (paste) | High | Direct read |
| Email forward | High | Direct read |
| Meeting transcript (Otter/Fireflies) | Medium | Skim for decisions, ignore filler |
| Word/Google Doc | Medium | Use file-reading skill |
| PDF (RFP / proposal) | Low-Medium | Use pdf-reading skill |
| Voice note transcript | Low | Same as meeting transcript |
| In-person meeting → PM's notes | Variable | Treat as Slack message |

---

## Universal extraction checklist

ไม่ว่า format อะไร, แอบหา 8 ข้อนี้:

| # | What | Where it usually appears |
|---|---|---|
| 1 | **Client identity** | Top of email, signature, doc header |
| 2 | **Project name / working title** | Subject line, doc title, first paragraph |
| 3 | **Problem / objective** | "We need...", "Our challenge is...", body |
| 4 | **End users** | "Our customers...", "for [role]" |
| 5 | **Deliverable expectation** | Bulleted list, "We want to launch...", "Send us..." |
| 6 | **Timeline** | "by [date]", "before [event]", "urgent" |
| 7 | **Budget hint** | Often vague — "small project", "comprehensive", or explicit range |
| 8 | **Existing assets/constraints** | Brand kit, "we use [stack]", "tied to [system]" |

ถ้าไม่ครบ → **explicit list as open question** ใน PM Card Section 7

---

## Reading between the lines

PM brief มักมี implicit info ที่ designer ต้องดึงออกมา:

### Signal: "Just a simple landing page"
**Likely reality:** ลูกค้ามี image ในหัว, ขนาดอาจไม่ "simple" จริง → ขอ reference

### Signal: "Like Stripe but for us"
**Likely reality:** ลูกค้าชอบ aesthetic / clarity ของ Stripe → ไม่ได้แปลว่า payment product → ขอ specifics

### Signal: "We have a design but need it built"
**Likely reality:** "Design" อาจเป็น Figma มี/ไม่มี components, อาจเป็น screenshot → ตรวจสอบ

### Signal: "Mobile-first"
**Likely reality:** ลูกค้าให้ความสำคัญ mobile, ไม่ได้แปลว่า desktop ไม่ต้อง → confirm scope

### Signal: "AI-powered" (in brief)
**Likely reality:** Buzzword หรือจริง — ถ้าจริงต้องรู้ว่า AI ทำอะไร, ใช้ provider ไหน → ขอ specifics

### Signal: timeline "ASAP" without date
**Likely reality:** ไม่มี real deadline แต่ client expectation = "next week" → confirm date, มิฉะนั้นจะ misalign

---

## Red flags to surface to PM

ถ้าเจอ signal เหล่านี้ใน brief, raise ต่อ PM ก่อน start Stage 1:

| Red flag | Why | Action |
|---|---|---|
| ไม่มี end user identified | Design ไปทาง wrong direction risk | ถาม "ใครใช้" |
| Deliverable list ขัดกับ tier (เช่น L scope, S deadline) | Set up failure | scope conversation |
| Multiple decision makers ฝั่งลูกค้า | Variant pick จะวุ่น | identify primary decision maker |
| Brand assets "later" promised | Stage 2 delayed | get workaround agreement |
| Stack ของลูกค้าที่ Sellsuki ไม่เคยใช้ | Stage 3 risk | feasibility check ก่อน |
| Hard deploy target client infra ไม่ document | Stage 4 risk | runbook plan |
| Reference is competitor of Sellsuki | Conflict-of-interest check | flag to Lead |

---

## Anti-patterns ตอน extract

❌ **Quote brief verbatim ใน PM Card** — designer ต้องสรุป + translate
❌ **Skip ambiguous parts** — surface as open question แทน
❌ **Assume happy path** — ถาม edge case ตั้งแต่ต้น
❌ **Trust client's tech estimate** — ลูกค้ามักประเมินผิด ทั้งทาง over/under
❌ **Ignore brand voice signal** — voice ใน brief = brand voice ลูกค้าอยากได้

---

## Example: parsing a messy brief

**Raw brief from PM:**
> "Hey, Acme Corp wants a portal for their partners to track orders. They said they want it 'like a typical B2B tool but cleaner'. Need it in about 6 weeks. They have a logo and color and that's it. Their dev team is busy so they want us to build front-end and they'll connect backend later. Budget ~M-size."

**Extracted to PM Card:**

```
Section 1:
  Client: Acme Corp
  Project: B2B Partner Order Portal (working title)
  Brief source: Slack from PM

Section 2:
  Tier: M (matches budget + timeline signal)
  Urgency: 6 weeks deadline (soft, no specific event tied)

Section 3:
  Objective: Self-service portal for Acme's partners to track orders
  End users: Acme's B2B partners (need to confirm: roles, count, frequency)
  Deliverable list:
    - Multi-screen portal (TBD which screens — derived in Stage 1)
    - Frontend only (no BE)
    - Connect to client's BE later (handoff Section F1 important)
    - Brand application from logo + color
  Out of scope:
    - Backend / API (their team)
    - Hosting (TBD — needs Stage 4)

Section 4 (to be locked at Stage 1):
  Stack: Modern default likely (Next.js + TS + Tailwind + shadcn/ui) — confirm at Stage 1
         (Acme team busy on BE, no client stack to match → greenfield modern choice)
  Deploy target: TBD (likely Vercel staging, client infra later)

Section 7 (Open questions for PM):
  - End user role + count + frequency?
  - "Cleaner than typical B2B" — any reference sites?
  - Brand kit beyond logo + color (font, voice, spacing) — when?
  - Hosting target staging vs prod
  - BE team's API contract — will design lead to API spec, or wait?
  - Maintenance after handoff: Acme dev team or Sellsuki?

Section 8 (Risks):
  - "BE connects later" = handoff Section F1 must be solid
  - Limited brand assets = Stage 2 may need to propose direction
  - 6 weeks for M = comfortable, but no buffer if Acme decision slow
```

---

## When brief is too thin

ถ้า brief สั้นจริง ๆ (e.g., "ทำเว็บให้บริษัทผม"):
- **ไม่ใช่** generate full plan แล้ว overload
- **ใช่** post a short response:

```
รับ brief มาแล้ว ผมต้องการ context เพิ่มก่อน start plan
- รบกวน PM ช่วยส่ง info ต่อไปนี้ก่อน (เก็บเป็น batch จาก client):
  1. End user คือใคร
  2. หลักการ "เว็บ" หมายถึง landing page, web app, e-commerce, หรืออื่น
  3. Timeline expectation
  4. มี brand asset อะไรบ้าง
  5. ใครจะ maintain หลัง launch

ส่งกลับมาแล้วเราจะวาง plan ได้แม่นและตรงงาน
```

---

## Tool: Atlassian / Notion / Google Drive

ถ้า PM brief อยู่ในเครื่องมือเหล่านี้, ใช้ tool ที่เกี่ยวข้อง:

- **Atlassian Confluence** → `Atlassian:getConfluencePage` (load via tool_search)
- **Notion** → ถ้า Notion MCP connected, ใช้ตามนั้น
- **Google Drive** → ถ้า Drive MCP connected, ใช้ตามนั้น
- **Email** → user paste content
- **PDF/Word** → user attaches, ใช้ file-reading skill

อย่าถาม "paste ให้หน่อย" ถ้า MCP มีให้ใช้
