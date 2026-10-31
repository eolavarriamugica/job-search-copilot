# Job Search Copilot

A plugin for Claude that runs a job search end to end: find roles, score fit honestly, tailor your CV from verified facts only, find people for referrals, prepare interviews, and keep one tracker up to date.

It never sends anything. Every message, email and application is a draft you send yourself.

## What's inside

| Skill | What it does |
|---|---|
| `setup-profile` | First-run interview. Fills your profile files from your CV and your answers. **Start here.** |
| `opportunity-scout` | Finds open roles on your watchlist's careers pages, job boards and public listings. Filters, removes duplicates, adds new roles to the tracker. |
| `role-scan` | Scans LinkedIn hiring posts and job listings in your own logged-in browser. See the warning below. |
| `fit-scorer` | Scores a job on "can I do it" and "do I want it", gives Apply / Stretch / Skip, names the gaps. |
| `referral-mapper` | Finds the hiring manager, teammates, recruiter and warm contacts. Drafts short outreach messages. |
| `cv-tailor` | Builds a one-job CV using only facts from your fact bank. Asks before using anything unclear. |
| `job-interview-prep` | Researches the company and the pay for the role, then builds a prep doc for the round. |
| `job-tracker` | Owns the tracker: stages, due dates, follow-ups, "what's due". |
| `de-ai-writer` | Rewrites any text to remove AI writing tells and simplify it. |

```
job-search-copilot/
├── .claude-plugin/plugin.json
├── profile/                  ← blank templates you fill in (see below)
│   ├── search-profile.md
│   ├── career-fact-bank.md
│   ├── company-watchlist.md
│   └── best-practices.md
├── templates/
│   └── Job_Search_Tracker.xlsx   ← blank tracker with formulas
└── skills/  (one folder per skill above)
```

## Before it works: what you must fill in

The skills ship with **no personal data**. Your target companies, pay floor, career facts and everything else are left blank (`____`) on purpose. A skill that hits a blank field it needs stops and asks you; it never guesses.

The fastest route: install the plugin, then tell Claude **"set up my job search"**. The `setup-profile` skill asks the questions, reads your CV and writes the files for you. Or fill them by hand:

### 1. `profile/search-profile.md` — required

| Section | Fields | Needed by |
|---|---|---|
| 1. What you are looking for | **Target roles, target city, work mode**, countries you can work from, company type, sector preference, travel, languages | All skills |
| 2. Pay | **Pay floor**, pay target, currency, equity rule | opportunity-scout, fit-scorer, interview prep |
| 3. Hard no's | Deal-breakers, company exceptions, re-application rule | opportunity-scout, fit-scorer |
| 4. Your angle | Years of experience, your edge, pitch angle | cv-tailor, fit-scorer |
| 5. Warm paths | Past employers, schools, communities | referral-mapper |
| 6. CV rules | Master CV file, file-name pattern, length, font, sections, current title, contact line, "never include" list | cv-tailor |
| 7. Tracker | **Tracker name or path**, where CVs and prep docs are saved | job-tracker and everything that logs to it |

Bold fields are the minimum before any skill runs.

### 2. `profile/career-fact-bank.md` — required

Every result you're allowed to claim, one per row, with the exact number. Mark each row:
- ✅ confirmed — the only status the skills will use
- ⚠️ open question — blocked until you answer
- 🔒 confidential — used without the client name or deal size

Also fill **Known gaps** honestly (e.g. "never managed a team"). The fit scorer flags them instead of hiding them, which is what makes the scores worth trusting.

### 3. `profile/company-watchlist.md` — required for opportunity-scout

Your tier 1 target companies, left blank for you to fill. Tiers 2 and 3 can start empty; the monthly refresh suggests names and adds them only after you approve.

### 4. `profile/best-practices.md` — optional

Ten sensible defaults (referral before applying, follow up at day 7 and 14, drafts only). Edit any you disagree with.

### 5. The tracker — required

`templates/Job_Search_Tracker.xlsx` has five tabs: Opportunities, Contacts, Activity log, CV versions, Rules.
1. Either upload it to Google Drive and open it as a Google Sheet (best if you use the Google Drive connector), or keep it as Excel in your project or folder.
2. In the **Rules** tab, fill **Pay floor**, **Pay target** and **Currency** (cells F2:F4, left blank).
3. Put the sheet's name or the file's path in section 7 of `search-profile.md`.

Grey columns are formulas (next to-do, due date, overdue alert, meets floor). Don't type in them. Stages, days and dropdowns are editable in the Rules tab.

### Where to keep your filled files

Skills look for the profile files in this order:
1. Your Claude project files or working folder (**recommended**: private to you, survives plugin updates).
2. The plugin's own `profile/` folder.

If you fill the copies inside the plugin folder, **never push them to a public repo**. If you fork this repo, keep your filled files in a folder named `my-profile/` (already in `.gitignore`) or outside the repo.

## Install

**Claude Code / Cowork (plugin):**
```
/plugin marketplace add eolavarriamugica/job-search-copilot
/plugin install job-search-copilot@job-search-copilot
```
Or clone the repo and point Claude at the folder as a local plugin.

**Claude.ai (skills only):** zip each folder in `skills/` and upload it under Settings → Capabilities → Skills. Upload your filled profile files and the tracker to a Claude project, and chat inside that project.

## Connectors and tools

| Tool | Used by | Required? |
|---|---|---|
| Web search and web fetch | opportunity-scout, interview prep, referral-mapper | Yes |
| Word file creation (docx skill) | cv-tailor | Yes, for CV files |
| Google Drive / Sheets | job-tracker (if your tracker is a Google Sheet), interview prep | Optional |
| A document tool (Docs, Google Docs or .docx) | interview prep | Yes, one of them |
| Browser connected to your own logged-in Chrome | role-scan | Only for role-scan |
| People-search connector (e.g. Apollo) | referral-mapper | Optional |
| Email drafts (e.g. Gmail) | follow-ups | Optional, drafts only |

## ⚠️ LinkedIn terms of use

`role-scan` reads LinkedIn pages in **your own logged-in browser**. LinkedIn's User Agreement restricts automated access and scraping, and accounts can be limited or banned for it. If you use this skill:
- run it by hand, occasionally, on small searches;
- never put it on a schedule;
- you accept the risk to your own account.

`opportunity-scout` only uses public pages and web search, and is the safer default.

## Suggested weekly run

Paste this into a chat once a week (or set it as a scheduled task, **without** role-scan):

> Run my weekly job search: 1) opportunity-scout for new roles since last week (monthly watchlist refresh if it's the first run of the month), 2) fit-scorer on each new role, 3) job-tracker "what's due". Drafts only, send nothing.

## Rules the skills follow

- Facts only from your fact bank. No invented skills, numbers, titles or results. No rounding up.
- A missing requirement is shown as missing.
- Drafts only. Nothing is sent, posted or submitted.
- Public professional information only when researching people.
- Max 2 contacts per company per week.
- Plain language, no unexplained acronyms.

## License

MIT. See `LICENSE`.
