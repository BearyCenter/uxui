# Deploy Checklist

> Stage 4 — เรียงตามลำดับ, tick ทีละข้อ

---

## Meta

**Project:** `[name]`
**Deploy target:** `Vercel / Netlify / Sellsuki cloud / Client infra / Other`
**Deploy date:** `YYYY-MM-DD HH:MM`
**Deployed by:** `[name]`

---

## Pre-deploy

- [ ] Code built successfully locally (`npm run build` etc.)
- [ ] All tests pass (ถ้ามี)
- [ ] No console error in production build
- [ ] Environment variables prepared (separate dev / staging / prod)
- [ ] `.env.example` updated in repo
- [ ] Build artifact size check (no unexpectedly large bundle)
- [ ] `package.json` engines / runtime correct
- [ ] `.gitignore` ครบ — no secret committed
- [ ] README updated with deploy instructions

---

## Deploy

### If Vercel/Netlify:

- [ ] Connect repo to Vercel/Netlify account
- [ ] Build command set
- [ ] Output directory set
- [ ] Env vars added in dashboard
- [ ] Custom domain configured (or use generated *.vercel.app / *.netlify.app)
- [ ] Initial deploy triggered
- [ ] Build log clean — no warning that needs attention

### If Sellsuki cloud / Client infra:

- [ ] Server access confirmed
- [ ] Runtime installed (Node version etc.)
- [ ] Reverse proxy / web server configured
- [ ] PM2 / systemd / Docker container set up
- [ ] HTTPS / SSL cert installed
- [ ] DNS record pointed correctly
- [ ] First deploy via SCP / git pull / docker push
- [ ] Service started and verified running

---

## Access setup

- [ ] URL works in incognito (no cache)
- [ ] Access type set:
  - [ ] Public
  - [ ] Password protect (Vercel password / basic auth)
  - [ ] SSO / auth
  - [ ] IP allowlist
- [ ] Credentials stored in secure tool (1Password / Bitwarden)
- [ ] Credentials NOT in repo / Slack / email plain text

---

## Configuration

- [ ] API endpoint env var → staging API (not prod)
- [ ] Analytics → off OR staging account (not prod)
- [ ] Error monitoring (Sentry/equiv) → staging project
- [ ] CORS configured correctly
- [ ] `robots.txt` → disallow crawl on staging
- [ ] `noindex` meta tag (extra safety)

---

## Smoke test (internal — before client gets URL)

| Check | Status | Notes |
|---|---|---|
| URL loads (cold) < 3 sec | ☐ | |
| Homepage renders | ☐ | |
| All routes work (no 404) | ☐ | |
| Forms submit (mock or real) | ☐ | |
| No console error | ☐ | |
| Mobile viewport renders | ☐ | |
| Chrome works | ☐ | |
| Safari works | ☐ | |
| Firefox works | ☐ | |
| Mobile Safari works | ☐ | |
| Mobile Chrome works | ☐ | |

**Smoke test result:** `PASS / FAIL`

ถ้า FAIL → ไม่ส่ง URL ให้ client → กลับ Stage 3

---

## Client-facing access prep

- [ ] URL ready
- [ ] Credentials packaged (secure channel)
- [ ] Known limitations list ready (e.g., "API uses mock — orders are sample data")
- [ ] Feedback channel agreed (Notion comment / inline tool / email / Slack)
- [ ] UAT round 1 date scheduled

---

## Hand to PM for client

- [ ] Sent message to PM:
  - URL
  - Credentials (via secure channel)
  - Test scenarios suggested
  - Deadline for round 1 feedback
- [ ] PM confirmed receipt
- [ ] PM scheduled with client

---

## Post-deploy verification

หลัง client received URL:

- [ ] Client can access (PM confirms)
- [ ] No "can't open" report within first hour
- [ ] Error monitoring shows no spike (if enabled)

---

## Deploy notes / known limitations

> Document anything client should know

- `[e.g., "Order list uses mock data, real API ใน Week 3"]`
- `[e.g., "Authentication ยังไม่มี — staging is open access"]`
- `[e.g., "Mobile responsive optimized for iPhone, Android Galaxy ก่อน"]`

---

## Status

- [ ] Deployed ✓
- [ ] Client has access
- [ ] UAT round 1 scheduled
- [ ] Stage 5 ready to start
