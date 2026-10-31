---
name: cv-tailor
description: Tailors the user's CV to a specific job using only verified facts from their career fact bank — selecting, ordering and rewording, never inventing. Asks before using anything unclear. Use whenever the user asks to adapt, tailor, rewrite or prepare their CV or résumé for a role or company, or when a tracked role reaches the "3 Applied" stage.
---

# CV tailor

## Before you start
Read the profile files: `career-fact-bank.md`, `search-profile.md` and `best-practices.md`. Look first in the user's project files or working folder, then in `${CLAUDE_PLUGIN_ROOT}/profile/`. If the fact bank is empty or a CV-rules field in the search profile is still `____`, stop and ask the user to fill it (or run `setup-profile`). Never guess a blank value.

Also read the docx skill (or your Word-file tool) before producing the file.

## Hard rules (no exceptions)
1. Use only facts marked ✅, plus the "Confirmed additions" section of the fact bank. Never add a skill, number, title, date or result that isn't in either.
2. Numbers stay exactly as in the fact bank. No rounding up, no adding totals, no merging two facts into one.
3. Facts marked 🔒: no client names or deal figures. Use the anonymised form.
4. Rewording is allowed only if the meaning stays the same. "Coordinated" does not become "led".
5. If the job needs something the fact bank doesn't cover, or a ⚠️ fact would help: stop and ask the user. List the questions. Don't write around the gap.
6. Job title: use "Current job title to use" from the search profile.
7. Never include anything listed under "Never include on a CV" in the search profile.

## Steps
1. Get the job ad. Pull the 5-8 things it cares about most, in its own words.
2. Map each to fact IDs. Show the user the map and any questions before writing if a ⚠️ fact or a gap matters.
3. Build the CV:
   - Summary: 3 lines, written for this role. Lead with the angle from "Your angle" in the search profile that fits this role.
   - Experience: most relevant results first within each job. Few bullets per role.
   - Use the job ad's words where they are true for the user.
   - Skills and languages: only what the fact bank supports.
4. Check before delivering: every bullet traces to a fact ID or confirmed addition. List any bullet you couldn't trace, then remove it.
5. Save using the "Tailored CV file name pattern" from the search profile. Log it in the tracker's CV versions tab via job-tracker: changes vs master and fact IDs used.

## Format
Follow the CV rules in the search profile (length, font, sections, master file). These defaults apply unless the profile says otherwise:
- Single column. No tables, so screening software can read it.
- Fill the page top to bottom without spilling onto an extra page. Render to PDF and check page count and fill before delivering.
- Dates right-aligned on the same line as the employer/title/school. Use a right tab stop set slightly inside the right margin (text width minus ~15 twips), never spaces, positional tabs or tables, so it survives conversion to Google Docs. Keep left-hand text short enough that the date never wraps (e.g. Education: school + date on one line, degree on the next).
- Contact line on one line (shrink it 1 pt if needed).

## Output to the user
The file, then 3 lines max: what was emphasised, what was left out, open questions.

## Writing style
Plain, direct verbs. One result per bullet. No filler words ("dynamic", "passionate", "results-driven"). No acronyms without spelling them out once.
