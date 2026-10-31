---
name: setup-profile
description: First-run setup for the job search plugin — interviews the user and fills the four profile files (search profile, career fact bank, company watchlist, best practices) and points them to the tracker template. Use when the user installs the plugin, says "set up my job search", "fill my profile", or when another skill in this plugin stops because a profile field is blank.
---

# Setup profile

Goal: turn the blank templates in `${CLAUDE_PLUGIN_ROOT}/profile/` into the user's own filled copies. Nothing gets invented: every value comes from the user or from a document they share.

## 1. Where the filled files will live
Ask once where they want them, recommend the first option:
1. **Their Claude project files** (recommended: survives plugin updates and is private to them).
2. A local folder they choose.
3. Directly inside the plugin's `profile/` folder (simplest, but a plugin update can overwrite it, and they must never publish that copy).

## 2. Career fact bank (from their CV)
1. Ask them to paste or attach their current CV(s), LinkedIn export, or a performance review.
2. Draft the fact bank rows from those documents only. One result per row, exact numbers, IDs in the template's ranges.
3. Mark ✅ only what the document states clearly. Mark ⚠️ anything conflicting between two documents, vague, or unsourced, and add it to "Open questions".
4. Ask which clients or deal sizes are confidential and mark those rows 🔒 with an anonymised wording.
5. Ask for their known gaps (team management, quota, years, tools). Explain that the fit scorer uses them to stay honest.
6. Show the drafted table and the open questions. Save only after they confirm.

## 3. Search profile
Ask the questions in batches (max 4 at a time), section by section, using the template's fields. Must-haves before any other skill will run: target roles, target city, work mode, pay floor, tracker location. The rest can stay `____` for now. Remind them the pay floor and target stay private.

## 4. Company watchlist
Ask for 3-10 tier 1 companies and any notes (remote only, referrals don't help). Tiers 2 and 3 can stay empty; offer to run the opportunity-scout monthly refresh to suggest names.

## 5. Best practices
Show the 10 defaults. Ask if they want to change any. Keep the rest.

## 6. Tracker
Point them to `${CLAUDE_PLUGIN_ROOT}/templates/Job_Search_Tracker.xlsx`. Two options:
- Upload it to Google Drive and open it as a Google Sheet (recommended if they use the Drive connector).
- Keep it as an Excel file in their project or folder.
Then write the pay floor and target into its Rules tab, and the tracker's name or path into section 7 of the search profile.

## 7. Finish
Write the four files, then reply with: what's filled, what's still blank (and which skills that blocks), and the first thing to try ("score this job: <link>").

## Rules
- Never fill a field with a guess or an example value.
- Never write the user's personal data into this plugin's own files if they chose option 1 or 2.
- Plain language, no acronyms without explaining them.
