---
name: job-tracker
description: Owns the user's job search tracker (a Google Sheet or Job_Search_Tracker.xlsx) and the stage-by-stage process for every opportunity. Use whenever the user mentions an application, a role they found, a recruiter or referral reply, an interview round, a rejection or offer, a follow-up, "what's due", "update the tracker", "log this", or asks where they stand on any company. Also use in the weekly job search run to list overdue to-dos.
---

# Job tracker

The tracker is the single source of truth. Other skills write to it through the rules here. Never keep status anywhere else.

## Find the tracker
1. Read "Tracker" in section 7 of `search-profile.md` (user's project files first, then `${CLAUDE_PLUGIN_ROOT}/profile/`). Use the sheet or file it names.
2. If that field is blank: search Google Drive for a sheet named "Job Search Tracker", then look for `Job_Search_Tracker.xlsx` in the project, uploads or working folder.
3. If nothing is found, say so and point the user to `templates/Job_Search_Tracker.xlsx` in this plugin (they can upload it to Google Sheets or keep it as Excel). Don't create a tracker on your own.

## Tabs and key columns
Columns in [brackets] are automatic (grey) and filled by formulas. Never type into them.

- **Opportunities**: ID (OPP-001…), Company, Role, Role type, Source, Job link, Work mode, Date found, Stage, Date entered stage, [Next to-do], [Due date], [Alert], Fit: can do (1-5), Fit: want it (1-5), Verdict, Pay offered (total), [Meets floor], Equity notes, CV version sent, Main contact, Outcome, Why, Notes.
- **Contacts**: Contact ID (CT-001…), Opportunity ID, [Company], Name, Title, Role in process, Warm path, LinkedIn URL, Email, Date contacted, Status, Next follow-up, [Alert], Notes.
- **Activity log**: Date, Opportunity ID, [Company], Type, Round #, With, What happened, Next step.
- **CV versions**: CV version ID (CV-001…), Date, Built for (Opportunity ID), [Company], File name / link, What changed vs master, Fact bank items used, Open questions before sending.
- **Rules**: stage rules, pay floor, pay target, dropdown lists. Edit only if the user asks.

## Stages

| Stage | To-do | Days |
|---|---|---|
| 1 Found | Score fit, decide apply / stretch / skip | 2 |
| 2 Referral | Contact 1-2 people at the company before applying | 5 |
| 3 Applied | Apply with tailored CV, log CV version | 7 |
| 4 Follow-up 1 | Send follow-up #1 (day 7) | 7 |
| 5 Follow-up 2 | Send follow-up #2 (day 14), then close if no reply | 7 |
| 6 Interviewing | Prep next round, thank-you within 24h | 7 |
| 7 Offer | Check against pay floor, negotiate or decide | 5 |
| 8 Closed | Log outcome and reason | 0 |

Stages can be skipped (a recruiter who reaches out goes straight to 6). They never go backwards; a revived role gets a note, not a stage reset to 1.

## Every update
1. Match the company and role to an existing row before adding one. No duplicates.
2. When the stage changes: set Stage AND set "Date entered stage" to today. Both, always.
3. Add one Activity log line for anything that happened.
4. People go to Contacts, linked by Opportunity ID.
5. A CV sent goes to CV versions, and its ID goes into the role's "CV version sent".
6. Closing a role: fill Outcome and Why. "No reply" is a valid outcome.
7. Confirm back in one line: what changed and the new next to-do with its date.

## "What's due" / weekly review
List, in this order: overdue roles, overdue contact follow-ups, due within 2 days, roles in "1 Found" with no fit score. One line each: company, role, to-do, due date. End with counts by stage. No commentary.

## Rules
- Never send emails or messages. Draft follow-ups only when asked, and save them as drafts.
- Don't delete rows. Close them.
- If an update is ambiguous (two open roles at the same company), ask which one.
