---
name: referral-mapper
description: Finds the right people at a target company for the user to ask for a referral or intro — hiring manager, team lead, recruiter, and warm paths through shared past employers, schools or communities — and drafts short outreach messages. Use whenever the user asks who to contact at a company, how to get referred, who the hiring manager is, or when a tracked role reaches the "2 Referral" stage.
---

# Referral mapper

## Before you start
Read the profile files: `search-profile.md`, `career-fact-bank.md` and `best-practices.md`. Look first in the user's project files or working folder, then in `${CLAUDE_PLUGIN_ROOT}/profile/`. Warm paths come from section 5 of the search profile; if it's blank, run without warm paths and say so.

If a people-search connector is available (e.g. Apollo, Sales Navigator), use it for the searching. Otherwise use web search.

## 1. Who to find (3-5 people, in this order)
1. **Hiring manager**: the person the role reports to. Infer from the job ad and team structure; mark "likely" if not certain.
2. **Someone on the same team** at peer level.
3. **Warm paths**: anyone at the company who shares a past employer, school or community listed in the search profile, or a stated mutual contact.
4. **Recruiter** for that function or region.

People based in the user's target city or country first when the role is there.

## 2. How to search
- People-search connector (if connected): search people at the company by title and location.
- Web search: `site:linkedin.com/in "<company>" "<title>"`, the company's team or blog pages, press, podcasts.
- Never guess emails. Use only emails a connector returns as verified; otherwise LinkedIn only.

## 3. Output per person
Name, title, location, role in process, warm path, why this person, LinkedIn URL, confidence (confirmed / likely).

## 4. Draft messages (one per person, the user sends them)
- Under 90 words. LinkedIn connection notes under 300 characters.
- Start with the link (shared employer, school, or something specific they did). No flattery.
- One line on the user, tied to the role, using one proven result from the fact bank (✅ only).
- One clear, small ask: a 15-minute chat, or "would you be open to referring me".
- No CV attached in the first message.
- Match the contact's language (their local language unless their profile is English-only).

## 5. Then
Add the people to the tracker's Contacts tab via job-tracker, status "Not contacted", next follow-up = 5 days after the user sends.

## Rules
- If the company states referrals give no advantage (note it in the watchlist), say so and skip. Suggest applying directly.
- Never send anything. Drafts only.
- Public professional information only. No personal details, family, or home locations.
- Don't contact more than 2 people at the same company in the same week.
