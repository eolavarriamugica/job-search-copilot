---
name: opportunity-scout
description: Finds open roles across company careers pages, startup job boards, LinkedIn and Indeed, keeps a watchlist of target companies and the local startup scene, filters roles against the user's search profile, removes ones already tracked, and adds new ones to the job tracker. Use whenever the user asks to find jobs, scan for openings, check what a target company is hiring for, asks which startups are hot in their area, or in the weekly job search run.
---

# Opportunity scout

## Before you start
Read the profile files: `search-profile.md`, `company-watchlist.md` and `best-practices.md`. Look first in the user's project files or working folder, then in `${CLAUDE_PLUGIN_ROOT}/profile/`. If target roles, target city, work mode or tier 1 of the watchlist are still `____`, stop and ask the user to fill them (or run `setup-profile`). Never guess a blank value.

## 1. Sources, in this order
1. **Careers pages of every company in the watchlist** (most reliable), tier 1 first. Find each company's jobs page with web search ("<company> careers", or its Ashby / Greenhouse / Lever job board) and fetch it.
2. **Startup job boards** — for example Y Combinator's Work at a Startup, Wellfound, or boards local to the user's region. Search for the target role types.
3. **LinkedIn and Indeed** — public job pages via web search, e.g. `"<target role>" <target city>`, `site:linkedin.com/jobs "<target role>" <country>`. Logged-in LinkedIn is not used here; say so if a lead needs it (the `role-scan` skill covers logged-in LinkedIn).
4. **Monthly refresh (first run of each month).** Refresh tiers 2 and 3 of the watchlist as that file describes. Report new names in a short table (name, city, what it does, latest funding, hires locally or remote). Add them to the watchlist only after the user approves. Don't add their roles unless they pass the filters.

## 2. Hard filters (drop, don't score)
- Location: not the target city and not remote → drop. Remote limited to a country the user can't work from → drop, note it.
- Company-specific exceptions in the search profile (e.g. "only if remote") → apply them.
- Pay: if listed and below the pay floor → drop. If not listed → keep, mark "Pay unknown".
- Role clearly outside the target list (e.g. engineering, design, junior roles, unless targeted) → drop.
- Posting older than 60 days or closed → drop.

## 3. Deduplicate
Check the tracker's Opportunities tab (via job-tracker) for the same company + role. Skip matches.

## 4. Output
For each new role: company, role, role type, source, link, work mode, pay if listed, posting date. Then:
- Run fit-scorer on each one if the user asks, or in the weekly run.
- Add to the tracker as stage "1 Found", today's date, via job-tracker rules.

Report back as a short table: company, role, work mode, pay, link. Then one line: how many found, dropped, and already tracked.

## Rules
- Only real postings with a working link. Never describe a role that you didn't see.
- Say which sources failed or were blocked. Don't fetch blocked sites through other means.
- Weekly run: only report roles that are new since the last run. If none, say "no new roles" and stop.
