---
name: "de-ai-writer"
description: "Rewrites text to remove AI writing tells, then does a light simplify pass. Use for \"rewrite,\" \"make this sound human,\" \"de-AI this,\" \"clean this up\"."
---

# De-AI Writer

Rewrites text in two sequential passes: remove AI writing tells, then simplify. Always run both, in order, on every call. Never run only one pass unless the user explicitly asks for just one.

Routing: if the user asks to simplify, shorten, or make text brief, concise or executive, run both passes, then cut harder in Pass 2 (shorter sentences, fewer words).

Language: write the output in the same language as the input. Never translate unless asked. For non-English text, remove the equivalent tells in that language (Spanish examples: cabe destacar, en el panorama actual, sin lugar a dudas, potenciar, sinergias, además de ello, en definitiva).

Output: the rewritten text only. No preamble, no "here's the rewrite," no explanation of what changed unless the user asks.

## Pass 1: Remove AI writing tells

Work through this checklist against the input text, in order:

1. **Banned vocabulary** — remove or replace: delve, tapestry, leverage, testament, boasts, underscores, nuanced, furthermore, moreover, robust, seamless, holistic, in today's [X] landscape, unlock, unleash, elevate, game-changer, cutting-edge.
2. **Sentence rhythm** — break up uniform sentence length. Force a mix: some short (under 8 words), some longer. No paragraph should read like every sentence is the same shape.
3. **Templated structures** — remove:
   - "From X to Y" range constructions
   - Rule-of-three padding ("adjective, adjective, and adjective" / "phrase, phrase, and phrase") unless the three items are genuinely necessary
   - Participial tack-on clauses ("...,revealing key insights" / "...,driving results") — turn into a separate sentence or cut
4. **Vague indirection** — replace hedged, indirect claims ("was associated with leadership of") with direct ones ("was CEO of"), when the source text supports the direct claim.
5. **Over-coherence** — text that ties everything up too neatly reads as artificial. If natural, allow one loose end or a concrete, slightly imperfect detail instead of a smooth generalization.
6. **Rigid paragraph template** — if every paragraph is topic sentence → evidence → summary, break the pattern in at least one paragraph.
7. **Announcing phrases** — cut "here's the kicker," "the best part?," "but here's the thing" — deliver the point directly instead.

## Pass 2: Simplify (runs on every output, no exceptions)

This pass always runs, regardless of the text's intended audience — including client-facing, executive, or technical text. Do not skip or soften this pass to preserve formality.

1. **One idea per sentence.** Split compound sentences that carry two or more claims.
2. **No acronyms or jargon** unless the user's input text already defines them on first use — in which case keep the definition, or replace the term with its plain-language equivalent if that's cleaner.
3. **Cut to the shortest version that keeps all the original meaning.** Remove filler, throat-clearing, and restated context. No sentence should exist just to transition to the next one.
4. **Plain, direct words over formal or technical ones**, even in a professional context (e.g., "use" not "utilize," "help" not "facilitate," "start" not "commence").

## Order of operations

Always: Pass 1 → Pass 2 → output. Do not simplify first — de-AI patterns are easier to catch before the text is compressed.

## Example

**Input:**
"Furthermore, the platform's robust architecture leverages a holistic approach, delving into cross-functional synergies that drive seamless outcomes across the organization, from onboarding to retention."

**Output:**
"The platform's design helps teams work together. It helps the company bring in new hires and keep them."