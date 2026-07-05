# Azure Learning Log — test-azure

A running record of my Azure deployment fundamentals. Newest session at top.

---

## Session 1 — 2026-07-04

### Goal
Set my Azure fundamentals: deploy this repo as an **Azure Static Web App** (code → GitHub → live site), before my Claude Code bootcamp.

### What this repo is
- The official Microsoft **"Vanilla JavaScript" Static Web Apps starter**.
- My website files live in **`src/`** (`index.html`, `styles.css`) — NOT the repo root.
- I personalized `index.html` into my own landing page.

### ✅ What I accomplished
1. **Edited & pushed my page** to GitHub (`numustafa/test-azure`, branch `main`).
2. Hit a push rejection caused by a **GitHub repository ruleset** (required PRs, signed commits, code scanning) — likely left behind by a Copilot agent. **Fixed by deleting the ruleset** in repo Settings → Rules. Push then succeeded.
3. Configured the **Create Static Web App** wizard correctly (see settings below).
4. **Ran my site locally** with `python -m http.server 8000 --directory src` → viewed at `http://localhost:8000`. Confirmed the page works.

### ⛔ Current blocker (NOT my fault — Azure capacity)
- My **Azure for Students** subscription has a region policy allowing **European regions only** (`RequestDisallowedByAzure` / "best available regions").
- Static Web Apps runs in only 5 regions worldwide; the only European one is **West Europe**.
- **West Europe is temporarily at capacity** → *"The selected region is currently not accepting new customers"* (https://aka.ms/locationineligible).
- Result: can't create the Static Web App until West Europe capacity reopens. Everything else is ready.

### 🧠 Key things I learned
- **Git 4 moves:** add → commit → push (+ pull/sync). I do these via **VS Code Source Control UI**, not the terminal.
- **CI/CD & GitHub Actions:** on every push to `main`, a workflow file (`.github/workflows/*.yml`) runs, grabs my code, and deploys it to Azure. That's the auto-deploy loop.
- **Resource Group** = a folder for related resources; delete the group to clean up everything at once (`rg-learning`).
- **Region policies & capacity** are real deployment constraints — a region can be *allowed by policy* yet *full*.
- **Serverless / Azure Functions** = small backend code that runs only when called; generous free tier; slots into Static Web Apps via the `api_location` setting.

### 📌 Correct Create-SWA settings (for when I retry)
| Field | Value |
|---|---|
| Subscription | Azure for Students |
| Resource Group | `rg-learning` (Create new) |
| Name | `test-azure-site` |
| Plan type | **Free** |
| Source | GitHub → `numustafa/test-azure` → branch `main` |
| App location | **`/src`** |
| Api location | *(empty)* |
| Output location | *(empty)* |
| Region (Advanced) | **West Europe** |

---

## ▶️ Next steps (start here next session)

1. **Retry the deploy.** Portal → Static Web Apps → **+ Create** → use the settings table above → **Review + create → Create**. Repeat until West Europe stops saying "not accepting new customers." (Try a few times/day.)
2. **When it deploys:**
   - In VS Code, click **Sync Changes** to pull the new `.github/workflows/*.yml` file Azure adds.
   - Watch the run go green in the repo's **Actions** tab (~2 min).
   - Find the live URL on the Static Web App's **Overview** page (`https://<something>.azurestaticapps.net`).
3. **Victory-lap lesson:** edit one line in `src/index.html`, commit + Sync in VS Code, watch it auto-redeploy live.
4. **Then, roadmap step 2 — Azure Functions:** add a small API in an `api/` folder, set `api_location: "api"`, and make the page *do* something.
5. Later: **Storage/DB** → **Azure OpenAI** (the agentic app goal).

### If West Europe stays full too long
Fallback that keeps everything on Azure: **Azure App Service (Free F1)** in West Europe — also deploys from GitHub, not capacity-blocked like SWA. (Ask Claude to walk through it.)

---

## 🎓 Certifications & free-voucher path

**The learning is free; the exams are paid — but Fundamentals exams can be free via Microsoft events.**

- **Training** (Microsoft Learn courses, study paths, practice assessments): **100% free**, always.
- **Exams** (the paid test that earns the badge):
  - Fundamentals (AZ-900, AI-900, DP-900): **~$99 / €-equivalent** each
  - Associate (AZ-204, AI-102): **~$165** each
  - Prices vary by country and change — confirm on the exam page before booking.

### Recommended cert order (hands-on first, cert second)
```
AZ-900 (Azure Fundamentals)  →  AI-900 (AI Fundamentals)  →  AZ-204 (Developer)  →  AI-102 (AI Engineer)
```
| Cert | Why it fits my path |
|---|---|
| **AZ-900** Azure Fundamentals | Formalizes what I learned today: regions, resource groups, free tiers |
| **AI-900** AI Fundamentals | Aligned with the Azure OpenAI / agentic-app goal |
| **AZ-204** Developer Associate | App Service, Functions, storage, APIs = basically my whole roadmap |
| **AI-102** AI Engineer Associate | Building AI solutions with Azure OpenAI (end goal) |

### 🎯 How to get Fundamentals exams FREE
1. Register for a free **Microsoft Virtual Training Day** — "Azure Fundamentals" or "Azure AI Fundamentals" (search *Microsoft Virtual Training Days* on the Microsoft Learn events page).
2. Attend → receive a **free exam voucher** for AZ-900 / AI-900.
3. Study on Microsoft Learn (free) → book with the voucher → **$0**.
4. Repeat for the other Fundamentals exam.

Associate exams (AZ-204, AI-102) are usually paid, but watch for **Cloud Skills Challenges** and **student offers** for discounts/vouchers.

---

## Local preview command (reusable)
```
python -m http.server 8000 --directory src
```
Then open http://localhost:8000 . Stop it by closing the terminal.
