---
name: role-scan
description: Scans LinkedIn in the user's own logged-in browser for business roles in their target city — hiring posts (who's hiring, past week or month) and job listings (last 14-30 days) — shortlists by fit with the user's fact bank and drafts the first referral message. Use when the user asks for a LinkedIn scan, "who's hiring", "run the job scan", or wants roles beyond what opportunity-scout finds on public pages.
---

# Role scan (LinkedIn, logged in)

> **Terms-of-use warning.** This skill reads LinkedIn pages in the user's own logged-in browser session. LinkedIn's User Agreement restricts automated access. Keep runs small and occasional, never run it on a schedule, and the user accepts the risk to their own account. If the user hasn't confirmed this once, say so before the first run.

## Before you start
Read the profile files: `search-profile.md`, `career-fact-bank.md`, `company-watchlist.md` and `best-practices.md`. Look first in the user's project files or working folder, then in `${CLAUDE_PLUGIN_ROOT}/profile/`. If target roles or target city are still `____`, stop and ask. Use:
- `<city>` = target city, `<country>` = its country
- `<roles>` = target role list
- `<space>` = company type / sector preference (e.g. "AI")
- floor = pay floor

Needs a browser tool connected to the user's own browser where they are logged in to LinkedIn. If none is available, say so and suggest opportunity-scout instead.

## Pick a mode

| Mode | When | What it searches | Company filter | Date window |
|---|---|---|---|---|
| **A. Posts, focused** (default) | "who's hiring", no other detail | Hiring posts | Companies matching `<space>` | Past month |
| **B. Posts, broad** | "any company", "this week" | Hiring posts | Any company, but the **role itself** must match `<space>` | Past week |
| **C. Job listings** | "look for jobs", "run the job scan" | LinkedIn Jobs | Companies matching `<space>` | Last 14 days (30 for company-name searches) |

## 1A/1B. Hiring posts
If the user's current tab holds something they may be typing (messaging, a draft), open a new tab and tell them. Close any tab you opened when done.

URL per query:
`https://www.linkedin.com/search/results/content/?keywords=<query>&datePosted="past-month"` (Mode A) or `"past-week"` (Mode B). Add `&sortBy="date_posted"` as a second pass when results look thin.

Build 8-12 short queries from the profile. Patterns that work:
- `hiring "<role>" <city>` for each main role
- `"we're hiring" <city> <space>`
- `hiring <city> <space> strategy` / `partnerships` / `business development`
- the same in the local language (e.g. `"estamos contratando" <city>`)
- `hiring "<role>" (<tier-1 company> OR <tier-1 company>)`

Keep queries short. Long OR chains return mostly noise in post search.

**How to read results (tested):**
- Wait about 6 seconds after loading (3 seconds often returns 0 posts), scroll to the bottom twice, then pull `main` innerText and split it on "Feed post".
- Tool output may get cut at about 1,000 characters. Store posts in `window._p` and print them in slices of 4–5 posts, about 200 characters each.
- Strip URLs before printing (`replace(/https?:\S+/g,'')`), or the output may get blocked.
- To read a full post, click the "more" buttons first, then find the post by author name.
- Job links: collect `a[href*="jobs/view"]` from the page. lnkd.in links open an interstitial page that shows the real target URL; navigate there.

## 1C. Job listings
Base URL: `https://www.linkedin.com/jobs/search/?keywords=<kw>&location=<city, region, country URL-encoded>&f_WT=3&f_TPR=r1209600`
(`f_WT=3` = hybrid, `f_WT=2` = remote, `f_TPR=r1209600` = last 14 days. For company-name searches drop `f_WT` and use `f_TPR=r2592000` = last 30 days.)

Keyword sets: one per target role, plus `<space> strategy OR growth OR operations`, plus one search of tier 1 company names joined with OR.

**How to read results (tested):** cards load lazily. Navigate, wait 5 s, then run JS that finds the list's scrollable parent of `li[data-occludable-job-id]`, scrolls it 300 px every 350 ms about 14 times, and collects `title | company | location` plus the job ID from each card.

To read a job: open `https://www.linkedin.com/jobs/search/?currentJobId=<id>&keywords=<company>`, wait 9-10 s, then read `document.body.innerText` from "About the job". On a job page, title, location, post date, work mode and closed status sit near the top of the body text. If it's still empty, wait 5 s more, or find the role on the company's job board (Greenhouse, Ashby, Lever).

**Do not** use the `/jobs-guest/` API with fetch: it rate-limits (429) after a few calls.

## 2. Filter
Keep a result only if all of these are true:
- **Posts only:** the author works at the hiring company (check the headline). A company page post counts. An outside recruiter working only for that company can count, but flag it and find an employee for the referral.
- **Company / role** matches the mode's filter.
- **Business role** from `<roles>`, not engineering or junior.
- **Location:** `<city>` hybrid, office or remote from an allowed country. On-site in `<city>`: allowed but flag it. On-site elsewhere: drop.
- **Inside the date window** and still accepting applications.

Skip and note in one line: recruiting agencies, staffing firms, job-list or repost accounts, investor round-ups, newsletters, people looking for jobs, roles outside the filters.

## 3. For each match
- Company: what it does, funding or size, HQ (one quick web search).
- Role: location, office days, pay against the floor, travel, languages, years required. **Flag "No longer accepting applications."** If it asks for a background the fact bank lacks, mark it Stretch.
- People: author or "Meet the hiring team" names, their type (technical / sales / leader / recruiter), connection degree.
- Fit (✅ facts only, cite fact IDs): Strong or Stretch, gaps.

## 4. Output
- One table: company, role, person, date, location and work mode, pay, fit, blocker.
- One table (or line) of the closest skipped results, with the reason.
- One recommendation: which to apply to now and who to contact first.
- A draft message for the top pick: under 300 characters; tone by person (technical = very to the point, sales = friendly, leader = executive); interest + one match with the company's mission; local language if the posting is in it.
- Sources.

## 5. If nothing matches
Say so plainly. Post search has low yield for business roles in most cities. Suggest Mode C, or opportunity-scout on the watchlist careers pages.

## 6. Stop
Never send messages or apply. Wait for the user's OK. After they send, log the role and contact in the tracker via job-tracker.

## Rules
- Public professional information only.
- Max 2 people at the same company in the same week.
- Don't fetch blocked sites through other means.
- Keep a short "Notes from earlier runs" list in the user's project files (not in this skill) if the user wants runs to remember who was contacted.
