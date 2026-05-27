# Card Classification Reference

> วิธีตัดสินใจว่า card เป็น track + size อะไร — สำหรับ Stage 0

---

## Track: Product vs Project

### Product track
- ใช้กับ: Sellsuki core platform, internal tools, ของที่เราเป็นเจ้าของและ iterate ต่อเนื่อง
- Signal:
  - Project key ของ Sellsuki product (เช่น SUKI, OC, MNG)
  - Epic ใน roadmap ของ Sellsuki
  - Label: `product`, `internal`, `core`
- Stage 5 จบที่: loop ไป Stage 0 อีกรอบหลัง measure

### Project track
- ใช้กับ: Client work, one-off, integration จบสายงานคนเดียว
- Signal:
  - Project key ของ client (เช่น CLIENT-XXX)
  - Epic มี client name
  - Label: `client`, `project`, `delivery`
- Stage 5 จบที่: hard stop, post-launch report

**ถ้าไม่แน่ใจ:** default = Product (เพราะ Sellsuki เป็น product company), แต่ confirm กับ user ก่อน Stage 1

---

## Size: S / M / L

ใช้ scoring system — รวมคะแนนแล้วจัด bucket

### Signals ที่ใช้ (รวมคะแนน)

| Signal | S signal | M signal | L signal |
|---|---|---|---|
| Story points (ถ้ามี) | 1-2 | 3-8 | 13+ |
| Number of ACs | 1-2 | 3-6 | 7+ |
| Affected screens | 0-1 | 2-4 | 5+ |
| New screens (vs edit) | 0 | 1-3 | 4+ |
| New nav item | no | maybe | yes |
| Backend/DB change | no | maybe | yes |
| Cross-team dependency | no | 1 team | 2+ teams |
| Estimated hours (PM estimate) | < 4 | 4-40 | 40+ |
| Description length | < 200 words | 200-800 words | 800+ words |

### Bucket rule

**Count how many signals fall in each column:**
- 7+ signals in S column → **S**
- 7+ signals in L column → **L**
- Mixed → **M** (default for ambiguous)
- ถ้าคะแนน borderline → ขึ้นไป size ที่สูงกว่า (เพื่อ avoid under-scoping)

### Examples

**Example 1 — S card:**
- "เปลี่ยน text ของปุ่ม 'Submit' เป็น 'บันทึก' ใน Order Detail page"
- Story points: 1, ACs: 1, Screens: 1 (edit), no new nav, no BE
- → **S**

**Example 2 — M card:**
- "เพิ่ม bulk export feature ใน Order List"
- Story points: 5, ACs: 4, Screens: 2 (1 edit + 1 new dialog), no new nav, BE: yes
- → **M**

**Example 3 — L card:**
- "Redesign Order Management module — new list, new detail, new filter, new bulk actions"
- Story points: 21, ACs: 12, Screens: 6 new + 3 edit, new nav, BE: yes, 2 teams
- → **L**

---

## Size → Stage selection (cheat sheet)

| Stage | S | M | L |
|---|---|---|---|
| 0 Intake | Quick parse, 5-line brief | Full parse | Full parse + Epic split |
| 1 Research | Skip — reuse existing | Light journey + IA | Full + competitive |
| 2 Design | Wireframe only | Wire + Hi-fi proto | IA sitemap + Wire + Hi-fi proto |
| 3 AI Usability | Skip (ถ้า flow ไม่เปลี่ยน) | 1-2 personas | 3+ personas |
| 4 Refine | Inline | 1 iteration | 2+ iterations |
| 5 Vibe Code | Direct DS swap | Full vibe code | Per-screen vibe code |

---

## Edge cases

### "Bug fix" cards
- Most bug fixes = S
- But: bug ที่เผยให้เห็น design flaw → escalate to M (เพราะต้อง redesign ส่วนเล็ก ๆ)

### "Spike" / research cards
- ไม่ใช่ design card จริง → run แค่ Stage 1 (research) แล้วจบ
- Output = research findings, ไม่ใช่ spec

### "Tech debt" cards ที่กระทบ UI
- Treat as M ขั้นต่ำ
- Stage 5 หนัก, Stage 1-4 ปานกลาง

### Card ที่ "เร่ง" (rush from PO)
- ห้าม skip Stage 0 และ Stage 3 — ทั้งสองเป็น safety net ที่สำคัญที่สุด
- สามารถ compress Stage 1-2 ได้ถ้า reuse จาก card ก่อนหน้า
- Document การ rush ใน intake brief Section 7

---

## When Claude can't decide

- ถ้า card ขาดข้อมูลพื้นฐาน (no description, no AC) → Stage 0 fail → ถาม PO ก่อน
- ถ้า signals ขัดแย้งกันอย่างหนัก → present 2 options ให้ user เลือก
- ถ้าเป็น L แต่ user บอกว่า "ทำเร็ว ๆ" → escalate to Lead — L-card ไม่ควร rush
