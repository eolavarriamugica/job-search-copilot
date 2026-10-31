---
name: job-interview-prep
description: Prepares the user for an interview round (recruiter screen, hiring manager, case, final) at a tracked company — reviews the CV sent, the job description, the company and the pay for the role, then builds a prep doc and updates the job tracker. Use when the user says they have an interview, a screen, a referral that led to a call, or asks to prepare for a round at a company.
---

# Job interview prep

One prep doc per company and round.

## Before you start
Read the profile files: `search-profile.md`, `career-fact-bank.md` and `best-practices.md`. Look first in the user's project files or working folder, then in `${CLAUDE_PLUGIN_ROOT}/profile/`.

## Pay rules
- Pay floor and pay target come from section 2 of the search profile (or the tracker's Rules tab if it's newer). If both are blank, skip the comparison and say so.
- The floor is the user's private walk-away line; never suggest they say it to a company.

## Inputs (find, don't ask)
1. Job tracker (via job-tracker rules). Find the Opportunities row for the company and role. If two open rows match, ask which one.
2. CV sent: read "CV version sent" on that row, then the matching CV versions row and its file link. Read the file itself. If no CV was logged, say so and use the closest CV version.
3. Job description: the row's Job link. If the site blocks fetching, search the exact role title plus company and read a copy on another job board. Note if the listing looks closed.
4. Contacts and Activity log rows for that opportunity (referrer, recruiter, past rounds).
5. Career fact bank, to check every story is a real, confirmed fact.

## Research the company (open the pages, never cite search snippets)
- History and founders, with their backgrounds.
- Funding: every round with date, amount, valuation, lead investors. Prefer primary sources (company blog, major news outlets); mark secondary sources as such.
- Product or platform: main products, launch dates, pricing model, the last 3 months of news.
- Customers: named ones, especially in the user's sectors and country.
- Presence in the user's region: offices, opening dates, who leads, local customers, open roles in the target city.
- Competitors.
- List open points (conflicting figures, missing facts) instead of guessing.

## Research the pay for the role
Goal: an estimated range in the user's target city for this exact role, base, variable and equity separate, compared with the floor and target.
1. Job sites: the posting itself and its copies on other boards. Copies in other countries often publish a range even when the local one does not.
2. Same company, same role, other regions (major tech hubs). Public salary filing data where it exists (for example US visa salary databases) for real base salaries by title.
3. Similar companies, same role: closest competitors and peers hiring the same job, in the user's country first, then the region, then the US.
4. Glassdoor and Levels.fyi. If salary data is missing or blocked, record the rating and pay-and-benefits score and say salary data was not available.
5. Extrapolate to the target city: state the ratio used versus each hub, show the arithmetic, and label the result an estimate. Convert currencies at the current rate and say which.
6. Output in the doc's pay section: one lead sentence with the estimated range against the floor and target; a table (comparable, where, pay, source, date); how the estimate was built; Glassdoor findings; what to say if asked for a number (ask for the band first; if pressed, anchor at the target; never quote the floor); equity questions for later rounds.
7. Note whether each figure is base, total or unclear, and whether it is employer-published or a third-party estimate. Never present an estimate as a published figure.

## Build the prep doc
Use the user's document tool (a shared doc, Google Doc, or .docx). Write one section at a time. Sections, in this order:
1. At a glance: role, tracker ID, date applied, CV version, referrer, next round and date, main gap, estimated pay against floor and target.
2. The role: what the job does (sourced), then a table "They ask for / Your evidence / Fit (Strong, Medium, Gap)".
3. The CV you sent: bullets most likely to come up with a one-minute story each; what to fix or be ready for.
4. The company: founders, funding table, product, customers, regional presence, competitors, open points.
5. Your pitch and stories: two-minute pitch (who, what you do, proof, why this company); stories table (question, story, result to quote); two or three reasons "why this company".
6. The call itself: likely questions with short answers for this round type; 5 questions to ask; pay (from the pay research); a before-the-call checklist.
7. Sources: every page opened, with dates.

Adjust section 6 to the round: recruiter screen = motivation, logistics, pay; hiring manager = stories and role depth; case or build exercise = structure and a practice prompt; final = founders' priorities and closing questions.

## Rules
- Never invent experience, numbers or results. Every story traces to the fact bank. Label gaps as gaps and give an honest way to answer them.
- Never use anything listed under "Never include on a CV" in the search profile.
- Respect the re-application rule in the search profile when suggesting other roles at the same company.
- Plain language, no acronyms without spelling them out.

## Tracker updates (follow job-tracker rules)
- Move the role to "6 Interviewing" and set "Date entered stage" to today.
- Fill "Pay offered (total)" only with a number the company gave; put the estimated range in the activity line instead.
- Add or update the referrer and recruiter in Contacts.
- Add one Activity log line with the round, the prep doc link and the next step.
- Never send messages or emails; draft only if asked.

## Reply to the user
1) Needs your input (date to confirm, gaps to decide on, facts to confirm), 2) Done (doc link, tracker changes, estimated pay range), 3) Optional recommendations. Keep it short.
