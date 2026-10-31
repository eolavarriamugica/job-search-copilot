---
name: fit-scorer
description: Scores how well a job matches the user on two separate axes — "can I do it" (skills, years, industry, technology) and "do I want it" (target space, company stage, location, pay, growth) — and gives an apply / stretch / skip verdict with gaps named. Use whenever the user shares a job link or description, asks "should I apply", "am I a fit", "how do I match", or when opportunity-scout adds new roles.
---

# Fit scorer

## Before you start
Read the profile files: `career-fact-bank.md`, `search-profile.md` and `best-practices.md`. Look first in the user's project files or working folder, then in `${CLAUDE_PLUGIN_ROOT}/profile/`. If the fact bank is empty, or the target roles, location or pay floor are still `____`, stop and ask the user to fill them (or run `setup-profile`). Never guess a blank value.

## 1. Pull the job's requirements
From the posting, list: must-haves, nice-to-haves, years asked, industry, technology, languages, location, pay. Quote nothing longer than a short phrase.

## 2. Score "Can I do it" (1-5)
Match each must-have to fact bank IDs.

| Part | What to check |
|---|---|
| Skills | Each must-have: met (fact ID), partly met, or missing |
| Years | Compare with the user's years (fact bank F-01). Asked for more → gap. |
| Industry | Industries in the fact bank = strong. Other = transferable, say how. |
| Technology | Only technology the fact bank shows. Deep specialist skills asked and absent = gap. |

Score: 5 = all must-haves met; 4 = one partly met; 3 = one missing but learnable; 2 = two or more missing; 1 = core requirement missing.

Only facts marked ✅ count. A ⚠️ fact counts as missing until confirmed.

## 3. Score "Do I want it" (1-5)

| Part | Strong | Weak |
|---|---|---|
| Target space | Matches "Company type" / "Sector preference" in the search profile | Only loosely related |
| Role type | On the target role list | Near it |
| Location | Target city or remote from an allowed country | Hybrid with unclear rules |
| Pay | Clearly above the pay floor | Unknown or near the floor |
| Growth | Bigger scope, strategy or leadership path | Sideways move |

If the search profile names a longer-term goal (e.g. founding a company), note whether the role builds toward it. Mention, don't score.

## 4. Verdict
- **Apply**: can do ≥4 and want it ≥4
- **Stretch**: one score is 3, the other ≥4
- **Skip**: either score ≤2, or a hard filter fails (location, pay below floor, deal-breaker in the search profile)

## 5. Output (keep it short)
1. Verdict + both scores, one line.
2. Table: requirement → met / partly / missing → fact ID or gap.
3. Top 3 selling points for this role (fact IDs).
4. Gaps, stated plainly, and how to handle each (address in cover note, referral, or accept).
5. Open questions for the user, only if a ⚠️ fact would change the verdict.

Then write scores and verdict to the tracker via job-tracker.

## Rules
- Never inflate. A missing requirement is missing.
- Every item under "Known gaps" in the fact bank must be flagged whenever a role asks for it.
- Plain language. No acronyms without explaining them.
