# Client Communication Templates

> Templates สำหรับ message ที่ designer ส่งผ่าน PM ไปยังลูกค้า — ที่ checkpoint สำคัญ
> ปรับ tone ตาม client relationship (formal new client / casual returning)

---

## Principles

1. **PM ในวงเสมอ** — ห้าม designer คุย client โดยตรง โดยไม่ระบุ PM
2. **One ask per message** — ไม่ stack 3 คำถามทับกัน
3. **Deadline ชัด** — ทุก ask มี date
4. **Action clear** — ลูกค้าทำอะไร, อย่างไร, ที่ไหน
5. **Defaults provided** — เสนอ default ที่ client OK ได้ง่าย ๆ
6. **Thai/English** — match brief's language. Most Thai project = Thai default

---

## Checkpoint 1 — Variant Pick (After Stage 2)

### Thai version

```
สวัสดีครับ/ค่ะ คุณ [client name]

นำเสนอ design สำหรับ project [name] — 2 variants ครับ/ค่ะ

🅰 **Variant A — [Direction name]**
🔗 [link to A]
   จุดเด่น: [1-line]
   Trade-off: [1-line]

🅱 **Variant B — [Direction name]**
🔗 [link to B]
   จุดเด่น: [1-line]
   Trade-off: [1-line]

📋 รบกวนตอบ 3 ข้อนี้ครับ/ค่ะ:
   1. เลือก variant ไหน (A / B / hybrid)
   2. ถ้า hybrid: ชอบ section ไหนจาก variant อื่น
   3. มีจุดที่อยากปรับเพิ่มเติมไหม

⏰ Deadline ตอบ: [date — ปกติ 2-3 working days]

หากต้องการ call เพื่อ discuss สะดวกแจ้ง slot ได้เลยครับ/ค่ะ

ขอบคุณครับ/ค่ะ
```

### English version

```
Hi [client name],

Presenting design for [project name] — 2 variants:

🅰 **Variant A — [Direction]**
🔗 [link]
   Strength: [1-line]
   Trade-off: [1-line]

🅱 **Variant B — [Direction]**
🔗 [link]
   Strength: [1-line]
   Trade-off: [1-line]

📋 Could you reply to these 3 questions:
   1. Which variant (A / B / hybrid)?
   2. If hybrid: which parts from which variant?
   3. Any specific tweaks you'd like?

⏰ Reply by: [date — typically 2-3 working days]

Happy to jump on a call if helpful — just send a few time slots.

Thanks!
```

---

## Checkpoint 2 — UAT Round 1 Invitation (After Stage 4 Deploy)

### Thai version

```
สวัสดีครับ/ค่ะ คุณ [client name]

Project [name] พร้อม preview รอบแรกแล้ว 🚀

🔗 URL: [link]
🔐 Login: [if needed — credentials ส่งแยกผ่าน secure channel]

📋 อยากให้ลูกค้าทดสอบประเด็นนี้:
   1. **Happy path** — ทำตาม flow หลักที่ตรง requirement
   2. **Look & feel** — อารมณ์รวม brand match ไหม
   3. **Edge case** — เจออะไรแปลก ๆ บ้าง (data เยอะ, network ช้า, ฯลฯ)

🔍 จุดที่ยังเป็น mock / ยังไม่ final:
   - [item 1 — e.g., "ข้อมูล order เป็น sample"]
   - [item 2]

⏰ Deadline feedback: [date — ปกติ 2-3 working days]
📝 ส่ง feedback มาที่: [channel — Notion comment / email / Slack]

💡 Tip การทดสอบ:
   - แนะนำเปิดในหลาย browser (Chrome / Safari) อย่างน้อย
   - ทดสอบมือถือถ้า scope ของ project ครอบคลุม
   - บันทึก screenshot ของจุดที่ติดขัด

UAT round นี้คือ round [1/2/3] จาก [budget] ที่วางไว้

ขอบคุณครับ/ค่ะ
```

### English version

```
Hi [client name],

Preview ready for [project name] 🚀

🔗 URL: [link]
🔐 Login: [if needed — credentials sent via secure channel separately]

📋 Could you focus on these areas:
   1. **Happy path** — main flow per requirements
   2. **Look & feel** — does it match brand expectation?
   3. **Edge cases** — anything unexpected (heavy data, slow network, etc.)?

🔍 Still mock / not finalized:
   - [item 1]
   - [item 2]

⏰ Feedback by: [date]
📝 Send feedback to: [channel]

💡 Testing tips:
   - Test in Chrome + Safari minimum
   - Try mobile if in scope
   - Screenshots of issues help a lot

This is UAT round [1/2/3] of [budget] planned.

Thanks!
```

---

## Checkpoint 3 — Sign-off Request (End of Stage 5)

### Thai version

```
สวัสดีครับ/ค่ะ คุณ [client name]

Project [name] — final version พร้อมแล้วครับ/ค่ะ

🔗 URL: [latest staging] (build [date])

📊 สรุปสิ่งที่ทำใน round ล่าสุด:
   ✓ [N] bugs fixed
   ✓ [N] improvements applied
   ⏸ [N] รายการเลื่อนไป v2 (ตกลงร่วมกัน — list ใน improvement log)

🎯 ขอ formal sign-off:
   - กรุณา reply กลับมาว่า **"approved"** หรือ **"sign-off"** หรือ **"ผ่าน"**
   - หรือถ้ายังมีประเด็น pending รบกวนแจ้งให้ทราบ

หลังได้รับ sign-off ผมจะส่ง **handoff package** ภายใน [N days]:
   📦 Design doc + final spec
   📦 Code repo + access
   📦 Staging URL + production deploy guide
   📦 Section สำหรับ BE/QA pickup ในอนาคต

⏰ ขอ sign-off ภายใน: [date]

ขอบคุณที่ work ด้วยกันครับ/ค่ะ 🙏
```

### English version

```
Hi [client name],

[Project name] — final version ready for your sign-off.

🔗 URL: [latest staging] (build [date])

📊 Latest round summary:
   ✓ [N] bugs fixed
   ✓ [N] improvements applied
   ⏸ [N] deferred to v2 (agreed — listed in improvement log)

🎯 Requesting formal sign-off:
   - Please reply with **"approved"** / **"sign-off"**
   - Or let us know if anything still pending

After sign-off, we'll deliver the **handoff package** within [N days]:
   📦 Design doc + final spec
   📦 Code repo + access
   📦 Staging URL + production deploy guide
   📦 Future BE/QA pickup hooks

⏰ Sign-off requested by: [date]

Thanks for working with us! 🙏
```

---

## Scope Conversation Trigger (Stage 5, mid-round)

ส่งให้ PM ทันทีเมื่อ "Change request" หรือ "Out of scope" finding ปรากฏ:

### Thai version (PM → Client via PM)

```
สวัสดีครับ/ค่ะ คุณ [client name]

จาก feedback round ล่าสุด มี [N] รายการที่อยู่นอก scope ตามที่เราตกลงกันใน brief เริ่มต้น:

📋 รายการ:
   1. **[item 1]**
      - อยู่ใน original scope: ❌ ไม่อยู่
      - Effort estimate: [hours / days]
      - Impact ต่อ timeline: + [N days]
      - Impact ต่อ budget: [if applicable]

   2. **[item 2]**
      ...

💡 Option ที่เสนอ:
   A) **เพิ่ม scope** — เซ็น change order, ขยาย timeline + budget
   B) **เลื่อน v2** — ไม่ทำตอนนี้, เปิด project ต่อในอนาคต
   C) **ผมรับเอง (ถ้าเป็น minor)** — ไม่ขยาย scope แต่ทำให้

รบกวนตัดสินใจภายใน: [date]

หากต้อง call เพื่อ align รบกวนแจ้งสะดวกครับ/ค่ะ

ขอบคุณครับ/ค่ะ
```

---

## Handoff Delivery (After Stage 6)

ใช้ format ใน `workflow/stage-6-handoff.md` Section 6.3 (Final delivery message) — copied here for reference:

```
🎉 Project [name] — handoff package พร้อม

📦 Deliverable:
  • Design: [link to handoff doc / Figma]
  • Code: [repo URL]
  • Live: [staging URL]
  • Docs: [link to handoff-doc.md]
  
🔑 Access:
  • ส่งผ่าน [1Password / Bitwarden / secure email]
  • Receiver: [name + email]
  
🔄 Post-handoff:
  • Bug ที่เกิดจากเหตุที่ Sellsuki รับผิดชอบ: support N วัน (per contract)
  • Future iteration: เปิด project ใหม่
  
🚀 Future BE / QA phase:
  • Hook สำหรับ pickup documented ใน Section F ของ handoff doc
  • เมื่อ Sellsuki พร้อม BE/QA team, plug-in ได้ทันที
  
ขอบคุณที่ work ด้วยกันครับ!
```

---

## Quick reference — when to use what

| Situation | Template |
|---|---|
| Present design variants | Checkpoint 1 |
| Invite client to UAT | Checkpoint 2 |
| Request sign-off | Checkpoint 3 |
| Surface scope issue mid-UAT | Scope conversation |
| Deliver final package | Handoff Delivery |

---

## Tone modifiers

ปรับ tone ตาม relationship:

| Relationship | Adjustment |
|---|---|
| First-time client | Slightly more formal, full intros |
| Returning client (2nd/3rd project) | Skip pleasantries, get to point |
| Long-term retainer | Casual, assume context, minimal preamble |
| Enterprise / multiple stakeholders | More formal, CC stakeholders, written record-style |

---

## Anti-patterns

- ❌ "Just checking in" with no clear ask — wastes client's time
- ❌ ทุกข้อความมี "if you have time" — soft, no deadline = ignored
- ❌ Three asks bundled — client picks one, ignores others
- ❌ "We need..." (Sellsuki's need) — flip to client's benefit
- ❌ Wall-of-text deliver — use bullets, links, headers
- ❌ Skip PM in CC — chain of accountability broken
- ❌ "ผ่านได้ไหม" — vague — ใช้ "approved" หรือ "sign-off" explicit
