I have the following markdown <document> whose content I would like parsed and transformed per the <guidelines> below, plus any <specialized-guidelines> for this document's channel. The goal is prose that reads as natural human writing and loses the marks of machine generation. This is not to hide that a model was involved and not to defeat detectors. It is to remove the tells that distract a reader.

If I include a <voice_sample>, treat it as the target voice. Match its register, rhythm, and word habits. If the sample breaks the punctuation or formatting rules below, or carries its own slop, follow the rules and leave the slop out: reduce those patterns rather than copy them. If the slot is empty, ignore it. The deepest tell, prose that reads as nobody in particular, is the one editing cannot fix on its own, since the cure is genuine voice and specifics, not removal. A real sample is the strongest lever for that; without one, tighten what you can and do not invent a personality to fill the gap.

<voice_sample>

// optional: paste a page of your own writing here. This is the single biggest lever for sounding like you. Delete this slot if unused.

</voice_sample>

<document>

// paste the text to be transformed here

</document>

<guidelines>

# Your task

Edit the text in <document> so it reads as natural human writing. Three standing constraints sit above every rule below:

- Keep the author's meaning and every factual claim intact.
- Don't rewrite verbatim or technical content unless the edit specifically targets it: code, commands, quoted material, citations, link text and URLs, tables, filenames, API and product names, error strings, and UI labels. Leave the document's markdown structure in place unless the structure itself is a tell.
- Do not introduce facts, numbers, names, or citations the source didn't have. If you can't keep a specific without guessing, leave the source's version or flag it. Never invent one.
- If a change would introduce an error, flag it and propose a fix rather than silently rewriting a claim you can't verify.

Work in this order: structure first, then sentences, then words, then a final calibration check. The detailed steps are in "The pass" near the end; the sections between are reference for what to look for.

# Layering with <specialized-guidelines>

If a <specialized-guidelines> block is present, treat it as adjustments layered on top of everything here, not a replacement. It sets tone and channel conventions for this one document: formality, warmth, enthusiasm, length, and the shape a given channel expects. A README, a social post, and a launch announcement each have their own structure.

Resolve conflicts in this order:

1. The three standing constraints above (meaning and facts intact, no fabrication, flag don't guess) always hold.
2. Inclusion and accessibility, and intellectual honesty, are non-negotiable: truthful claims, stated limits, no hollow or fabricated puffery. The specialized layer cannot relax these. It can still set warmth and enthusiasm, and a grounded superlative is a tone choice rather than dishonesty. What stays banned is selling past the facts.
3. The de-slop tells hold: the specialized layer may not reintroduce slop. But where a channel genuinely needs a different structure or format than the general defaults (minimal formatting, lead with the main point), its conventions win at the format level. A README leads with a title and an install block, not a prose lede; a social post stays short and may open with a hook.
4. Within those bounds, the specialized layer sets tone. It may move the warmth, formality, and enthusiasm dials, which this core keeps restrained by default.
5. The em dash and semicolon bans stay absolute. The one punctuation the specialized layer may re-allow is the exclamation point, and only if it says so explicitly, used sparingly.

If a voice sample and the specialized layer pull in different directions, the voice sample governs voice and word habits while the specialized layer governs channel tone, structure, and length.

If the specialized layer is silent on a point, the general guideline applies. If the block is empty or absent, ignore it.

# Interactive mode (optional)

Default: one-shot. Make every edit and return the result, including depth-trimming, with each section you cut or heavily shorten named in the "Changes" section so it can be reversed. Do not stop to ask anything. This is the mode for one-shot and API runs where no one is waiting to reply.

If an <interactive> block is present and turned on, change only this: before you trim or cut any section for depth, stop and propose it instead of doing it. List each section you'd trim and the one-line reason, name the ones you judge load-bearing and would keep, and wait for the reply. Apply only what comes back approved. Every other edit (mirrors, hedges, word choice, structure that isn't deletion) still happens in one pass without asking. The trigger is the action, not your confidence: pause whenever you are about to remove content for depth, whether or not you feel unsure. Do not widen this to other edits or turn the whole job into a back-and-forth.

# The rule that governs all others: calibrate, do not sterilize

Fix tells where they cluster: a passage thick with them and thin on concrete detail. Leave a lone instance sitting in otherwise specific, varied prose. One "crucial," one good list, one long sentence is not a problem. Don't count words or hunt single instances; judge density. Lower the frequency of tells; do not drive them to zero. Banning every flagged word and every list flattens the prose into its own kind of artificial. When you finish, reread: if the voice is flatter or more uniform than the original, you overcorrected, so restore variation.

One worked example, since this balance is easier to show than describe:

> Original: "We leverage a robust, comprehensive pipeline to seamlessly delve into customer data and unlock actionable insights."
> Over-corrected: "We use a pipeline for customer data." (true, but stripped to nothing)
> Calibrated: "Our pipeline pulls every order, return, and support ticket into one table, so we can see which products drive repeat buyers. It's robust enough to keep running when a daily feed fails." (four flagged words gone; "robust" kept because it's now doing real work; a specific replaces the vague "actionable insights")

# Target voice and style

- Keep a high signal-to-noise ratio. Every sentence should carry concrete value. Cut fluff, hedging, and warm-up phrases.
- Be intellectually honest. The aim is to inform, not to impress or sell. State limits and trade-offs plainly. Avoid superlatives and opinion-loaded modifiers; let specifics carry the weight.
- Use plain, direct language without losing technical precision. Contractions are fine where they read naturally.
- Stay serious and human. No forced cheer, no cutesy metaphors, no conversational filler. Humor is not the default.
- Write clear sentences with a real subject and active voice; name the actor. "Plain" means clear, not uniform: vary length and opening (see Sentence construction). Avoid headline-style noun-phrase fragments as openers.
- Use direct address ("you," and "we" for a team or org) where the channel supports it, such as product copy, docs, emails, and posts. For reports, analysis, reference, academic, legal, or neutral briefs, keep the source's point of view unless a specialized layer says otherwise. Either way, avoid "one" and "the user" where a name or "you" reads better.
- Prefer the simpler word: "use" not "utilize," "process" not "regimen."
- Lead with the main point so a reader who stops early still gets the essentials.
- Frame gaps without apology or defensiveness. If the source says the gap is planned, say so. If it doesn't, state the limitation plainly and don't imply a roadmap.

# What to remove (de-slop), largest scope first

## Structure

- The five-paragraph shape stretched to any length: intro, three balanced chunks, recap.
- Empty intros and summary paragraphs that restate what was just said. Stop when the point is made.
- Listicle reflex: bullets for open-ended material, or prose disguised as a list.
- Forced symmetry that gives every point equal weight regardless of importance.
- Uniform depth, the subtler cousin: every section running the same length and the same exhaustive competence, so the piece reads as written from one flat altitude with no sign of where the author cared most. Let depth vary. Trim the obvious or low-stakes sections by cutting, not padding, and never by inventing detail. Reference and documentation channels built on parallel, complete sections are the exception: there, even structure is the point, so preserve it unless a specialized layer says otherwise. Depth-trimming is the one edit here that destroys content, so it follows the interactive rule (logged by default, proposed first if the flag is on).
- False balance: "critics say X, supporters say Y, the truth is somewhere between."
- The "despite its strengths it faces challenges, but the future is promising" formula.

## Tone

- Relentless positivity and promotional register on non-promotional subjects ("rich heritage," "vibrant community," "stands as a testament to"). State the fact; don't puff its importance.
- Sycophancy: "Great question," "You're absolutely right." Cut it.
- Cheap warmth and chatty filler: "Hope this helps," "Let's dive in," "that being said."
- Flat affect, one emotional temperature held for the whole piece. Let it drift the way a person's does.
- No genuine stance. Commit to a position where the piece is analysis or argument. Where it is reporting or reference and the author is deliberately neutral, preserve that; don't manufacture a stance.
- Stakes inflation, turning a small note into a meditation on the human condition.
- Strategic vagueness that sounds nice and says little.

## Substance and evidence

- The missing concrete particular. Swap generic nouns for specific ones: the support team, the March 2020 release, the iPhone X. This is the highest-impact single edit, and the one most likely to tempt invented detail, so use only specifics the source supports.
- Unanchored quantities: "about 70% of users," "studies suggest up to a third." Tie the number to a source the document already cites, or cut the number.
- False profundity: "change is the only constant," "at the end of the day we're all human."
- Invented concept labels dressed up as established terms ("the supervision paradox").
- Vague attribution: "experts argue," "studies show." If the source names who, use the name. If it doesn't, keep the claim and flag it rather than cutting it, or recast it as the author's own assertion if that's what it is. This is an editing pass, not a fact-check, so don't delete substance to tidy the attribution.
- Asserting instead of proving: "clearly," "the truth is simple" to skip the argument.

## Sentence construction

- The negated contrast: "it's not X, it's Y," "not just X but Y," "Not X. Not Y. Just Z." This is the most diagnostic move. Search for "just" and "not only" to find it. Rewrite as a direct claim.
- Mirrored contrast: two options set in matched, parallel clauses ("higher premium, stable costs" against "lower premium, variable costs"), often introduced by a reflexive "the trade-off:" or "the catch:". The symmetry reads as machine-balanced. Keep the comparison, break the mirror: vary the two sides in length or construction, or fold one into prose, and cut the "trade-off" framing where the contrast is already clear.
- The participial tail: "..., highlighting its importance," "..., reflecting broader trends." Rewrite as a direct assertion or split the sentence.
- Monotony, the deeper version of low burstiness: uniform sentence length, the same subject-verb-object shape sentence after sentence, repeated openings, and uniform paragraph length. Break these on purpose. A three-word sentence after a forty-word one. A one-line paragraph after a dense one.
- Rule-of-three stacking. Cut the third item when only two are real.
- "From X to Y" false ranges with nothing actually in between.
- Self-answered rhetorical questions: "The result? Devastating."
- Hedging, two forms. Stacked: "generally speaking," "to some extent," "in most cases" piled together. Reflexive: every assertion softened the moment it lands, so the piece runs claim, qualifier, claim, qualifier down the page ("X works this way. Generally, though..." / "...The trade-off:"). State things directly and qualify only where the caveat carries real information.
- Over-explanation. A sentence that only restates the previous sentence's implication adds nothing; cut it. Same for defensive completeness, the reflex to chase every caveat ("though some environments may differ depending on configuration, implementation, and platform"). Stop when the reader has enough.
- Thesis re-announcement: "as discussed above," "as we've seen," "this reinforces," "returning to our earlier point," or the same point resurfacing across sections with nothing new added. Consolidate or cut.
- Over-signposting that narrates the document instead of making the point: "First we'll look at... then we'll examine..."
- Orphaned demonstratives: "This highlights..." with no clear antecedent.

## Word choice

Watch for these families when they cluster on flat subjects: synthetic-erudition words (delve, intricate, meticulous, pivotal, garner, underscore, showcase); borrowed-grandeur nouns (tapestry, landscape, realm, ecosystem, cornerstone, testament, beacon); corporate inflation (robust, seamless, vibrant, comprehensive, multifaceted, holistic, cutting-edge, transformative, groundbreaking, plethora, myriad); inflated verbs (leverage, utilize, harness, streamline, facilitate, optimize, empower, foster, elevate, unlock, unleash).

Also recover buried verbs from noun phrases (nominalization): "conduct an evaluation of" becomes "evaluate," "perform an optimization of" becomes "optimize," "make a decision" becomes "decide."

The table below is a recognition list, not a find-and-replace map. Use it to notice flagged words, then decide case by case. Three rules. Prefer recasting the sentence so the word isn't needed over a one-for-one swap, since swapping every instance just trades one uniformity for another. Keep any word when it is the precise technical term ("robust error handling," "query optimization" are correct). Aim to lower frequency, not reach zero; one "leverage" is invisible, eight is the tell.

| Avoid by default | Prefer |
| --- | --- |
| leverage, utilize, harness | use, draw on |
| streamline | simplify, speed up |
| facilitate, foster, empower | help, let, enable |
| delve into, dive into, dig into | look at, examine, cover |
| unlock, unleash | enable, make possible |
| showcase, underscore | show, emphasize |
| robust | reliable, solid (keep for "robust to failure") |
| seamless | smooth, direct |
| comprehensive, holistic | full, complete, end-to-end |
| multifaceted, nuanced | complex, many-sided |
| cutting-edge, state-of-the-art | current, modern |
| transformative, groundbreaking, game-changing | major, useful |
| plethora, myriad | many, a range of |
| tapestry, mosaic, landscape, realm (figurative) | mix, field, area |
| testament to | proof of, shows |
| furthermore, moreover, additionally | also, plus, and |
| in conclusion, in summary, ultimately | (omit; just stop) |
| it's worth noting, it's important to note that | (omit; state the point) |
| when it comes to | for, with, in |
| at its core, at the heart of | (omit; say the thing) |

Also cut: opener cliches ("in today's fast-paced world," "imagine a scenario where"), closing rituals ("the journey doesn't end here"), and stray curly quotes or placeholder artifacts where a link was meant to go.

# Punctuation and formatting (hard rules for this task)

- No em dashes. Replace with a comma, colon, parentheses, or a sentence split. Never use a double hyphen. This is a deliberate hard rule for model output, not a frequency suggestion, so do not relax it even if the voice sample or a specialized layer asks for it; trim them instead.
- No semicolons either. This is a hard rule like the em dash, not relaxable by the voice sample or a specialized layer. Use a comma, a colon, or two sentences.
- No exclamation points, unless a <specialized-guidelines> block explicitly allows them. Even then, use them sparingly.
- Sentence-case headings that label their section, not taglines. Don't stack two headings with no text between them.
- Keep formatting minimal. Reserve bold and lists for cases that earn it, such as sequential steps or distinct requirements.
- No `**Term**: explanation` bullet chains repeated down a list; mix in plain bullets and full sentences. Use `- ` for bullets, not `* `.
- No decorative emoji, no ALL CAPS for emphasis, no bold combined with italic.

# Inclusion and accessibility

These are non-negotiable, with one scoped exception noted at the end.

- Gender-neutral language; singular "they" when pronouns are unknown. Person-first by default ("a person with diabetes"), but follow identity-first usage where a community prefers it ("autistic person," "Deaf community") or where the source already does.
- Avoid ableist terms and violent or aggressive idioms.
- No directional language ("above," "below," "the box on the right"); refer to things by name.
- Descriptive link text, not "click here."
- Meaning should survive without color or images.
- Scoped, not absolute: writing for a global or translated audience favors plain words over idioms, slang, and culture-specific references (holidays, sports, seasons). This is a localization choice, not a moral rule, so it yields to the voice sample and to channels where idiom is natural. Don't strip a casual or personal voice flat in its name.

# The pass (do these in order)

Before you start: the goal is calibration, not removal. Lower the density of tells and restore variation; don't strip the text to a uniform minimum. The mechanical rules below are easy to over-apply, so let the calibration gate at the end govern them.

1. Fix structure first. Cut empty intros and summary paragraphs, break the five-paragraph shape, turn prose-disguised-as-a-list back into prose (or a real list back into prose), and drop forced symmetry and false balance. Let section depth vary by trimming the obvious or low-stakes ones, unless the channel calls for even, complete sections, and handle those depth cuts per the interactive rule (log them by default, or propose them first if the flag is on).
2. Restore burstiness. Vary sentence length, opening, and shape, and vary paragraph length, but only where the content motivates it. Don't insert sentence fragments or clipped one-liners for rhythm; manufactured staccato ("Sad. Very sad.") is its own tell.
3. Hunt the negated contrast, the mirrored contrast, and the participial tail. Rewrite the contrasts as direct claims or break their symmetry; rewrite the tails as direct assertions.
4. Strip signposting filler, opener cliches, and stacked hedging. State the thing.
5. Rewrite for specificity. Swap generic nouns for concrete ones the source supports. Turn mood words into facts only where the source gives them ("robust" becomes a real number only if the document states one).
6. Replace inflated verbs, nominalizations, and ornate abstractions with plain words. Lower the frequency of the table words without zeroing them.
7. Fix punctuation and formatting. Remove em dashes and semicolons. Remove exclamation points too, unless the specialized layer allows them. De-bold and de-bullet connected prose, but keep genuine lists.

# Before you return

Run these as checks, not as edits woven into the pass:

- Stance: did you add one only where the piece argues or analyzes, and leave deliberate neutrality alone?
- Sources: does every claim that needs attribution either name its source or get flagged? Don't cut a claim just to remove a vague attribution.
- Facts: are all dates, figures, names, and citations preserved from the source or flagged, with nothing invented?
- Punctuation: scan the whole output for em dashes and semicolons that slipped in late, and remove them.
- Calibration gate, the last thing you do. Count nothing; compare. If the rewrite is more uniform than the original in sentence length, affect, or structure, the pass failed: restore variation before returning. Re-read against "calibrate, do not sterilize."

# Do not

- Don't insert typos, errors, slang, forced chattiness, or persona tics to "seem human." That trades away the goal, which is clear, correct prose. Calibrate register to the audience and fix the substance instead.
- Don't bulk-rewrite passages that are already clean. Touch what has tells.

# Output

Return the full rewritten document first. Then add a short section titled "Changes" naming the substantive edits and anything you flagged as unverified, and calling out any section you trimmed or cut for depth so it can be reversed. Use 4 to 8 bullets for a normal document; for a very short piece like a social post, a line or two is enough. If I write "skip the changelog," return only the rewritten text. In interactive mode, when you pause for approval on depth cuts, send the proposal on its own first and the rewritten document only after the reply.

</guidelines>

<specialized-guidelines>

// optional: context-specific guidelines that build on the general <guidelines> above. Use this for the channel and the one-off needs of this particular document: a GitHub README, a social post, a marketing campaign, release notes, and so on. State the channel, the tone you want (formality, warmth, enthusiasm), any length or structure the channel expects, and any must-haves (a call to action, install steps, a hook). These adjust tone and format within the general rules; they cannot relax the non-negotiables, reintroduce slop, or re-allow em dashes or semicolons. Delete this slot if unused.

</specialized-guidelines>

<interactive>

// optional, for live chat only. Write "on" to make me pause and ask before trimming or cutting any section for depth, so you approve those cuts first. Everything else still happens in one pass. Leave this empty, set it to "off", or delete the slot for one-shot behavior, which is the default and the right choice for API or batch runs where no one is available to reply.

</interactive>
