# Stage 4 — Deploy

**Position:** `Vibe Code → DEPLOY → Test & Improve`

---

## Purpose

ทำให้ลูกค้า **เปิด URL ดูได้** — staging environment พร้อม access — เพื่อ start UAT cycle

---

## Trigger

- Stage 3 ผ่าน gate — code builds, QA passed, repo ready

---

## Input

- Repo (vibe code output)
- Build artifact
- Deploy target (Sellsuki cloud, Vercel, Netlify, client infra, ...)
- Access requirements (public / password-protected / auth)
- Domain plan (subdomain ของ Sellsuki, ของลูกค้า, หรือ generic staging URL)

---

## Activities

### 4.1 Choose deploy target

| Target | When | Pros | Cons |
|---|---|---|---|
| **Vercel/Netlify** (Sellsuki account) | Default, fast | Auto preview, CI hook | Sellsuki domain |
| **Sellsuki cloud** | When client wants under Sellsuki control | Brand consistency | Setup overhead |
| **Client infrastructure** | Client demands or pre-arranged | Final environment from start | Access setup ยาก |
| **Internal staging** | Sensitive content, internal review first | Privacy | ต้อง forward to client later |

`Vercel MCP` (`Vercel:deploy_to_vercel`) สำหรับ default path — Claude เรียกได้

### 4.2 Setup checklist (ดูเต็มใน `templates/deploy-checklist.md`)

- [ ] Build pipeline configured (env vars, build command)
- [ ] Domain attached / temp URL generated
- [ ] HTTPS / SSL ผ่าน
- [ ] Access control set (public / password / auth)
- [ ] Environment variables set (API URL, keys)
- [ ] CORS configured ถ้า cross-origin
- [ ] Analytics opt-in / opt-out per project
- [ ] robots.txt — disallow search index for staging
- [ ] Error monitoring (optional — Sentry/equiv)

### 4.3 Smoke test (internal — before client gets URL)

| Check | Pass criterion |
|---|---|
| URL loads | < 3 sec |
| All routes work | No 404 on intended routes |
| Forms submit | (with mock or real API) |
| No console error | clean console |
| Mobile viewport | renders correctly |
| Different browsers | Chrome + Safari minimum |

ถ้า smoke test fail → ห้ามส่ง URL ให้ลูกค้า → กลับ Stage 3

### 4.4 Prepare client-facing access

- URL
- Login credentials (ถ้ามี)
- Known limitations note (e.g., "API ใช้ mock", "ทดสอบเฉพาะ desktop ก่อน")
- How to give feedback (Notion comment? Inline annotation tool? Email?)

---

## Output

- Live staging URL
- Access credentials (sent to PM securely)
- Deploy notes / known limitations
- Smoke test result (filed)

---

## Gate to Stage 5

- [ ] URL accessible
- [ ] Smoke test passed
- [ ] Access shared with PM (PM forwards to client)
- [ ] Client confirmed receipt
- [ ] UAT round 1 scheduled

---

## Client checkpoint #2 — UAT round 1 invitation

Send via PM:

```
Project [name] พร้อม preview แล้ว

🔗 URL: [link]
🔐 Credentials: [if applicable]

📋 อยากให้ลูกค้าลองดูประเด็นนี้:
  1. Flow หลัก (happy path) — ทำตามที่ requirement ระบุได้ไหม
  2. Look & feel — match brand ตามที่คาดไว้ไหม
  3. Edge case — เจออะไรแปลก ๆ บ้าง

⏰ Deadline feedback: [date จาก milestone]

📝 ส่ง feedback มาที่: [channel]
```

---

## Deploy to client infrastructure

ถ้า target = client infra:

| Need | How |
|---|---|
| Access | PM coordinate กับ client IT |
| Credentials | Use Sellsuki secure tool (1Password, Bitwarden) |
| Runbook | Document setup steps in `deploy-checklist.md` extension |
| Rollback plan | Especially if production-adjacent |

อย่า assume — confirm everything กับ client IT ก่อน push

---

## Common Mistakes

- Skip smoke test → ลูกค้าเปิดแล้วเจอ error → trust damage
- Forward URL ก่อน HTTPS พร้อม → unprofessional
- ลืม env vars → app crash on load
- No known limitations note → ลูกค้าคิดว่า "mock data" คือ live → confusion
- Deploy โดยไม่บอก PM → client surprised, PM not in loop
- Hardcoded API URL → ลูกค้า test กับ dev API ของเรา (privacy concern)

---

## Owner

| Role | Responsibility |
|---|---|
| Claude | Run deploy via Vercel MCP, smoke test, generate access docs |
| Level 1 Designer | Verify URL, smoke test, prepare access info |
| Level 2 Lead | Approve client-infra deploys |
| PM | Forward access to client, set UAT expectation |
