# Frontier Model Roles and Tool Routing (May 2026)

Curated from cross-comparison of Claude, ChatGPT, Gemini, and Perplexity. Free tier assumed except Claude Pro.

| Use case | Tool |
|---|---|
| Architecture, code review, test design, brainstorming, meta planning | Claude Opus 4.7 + Extended Thinking |
| Writing/modifying code, generating test code | Claude Code in VSCode (Sonnet 4.6 default; Opus for hard refactors) |
| Documentation, READMEs, JSDoc, commit messages | Claude Sonnet 4.6 (Haiku 4.5 for routine) |
| Evaluating design mockups (PNG/JPG) | Claude Opus 4.7 or Gemini 2.5 Pro — try both (Claude leads on dense UI; Gemini on Figma-native workflows). For Figma sources specifically, the Figma MCP server is model-agnostic and works with Claude Code, Cursor, Copilot, Windsurf, and Gemini. For matching mockup sections to existing components, use Claude in a Project seeded with the component library |
| Whole-codebase ingestion (large repos) | Gemini 2.5 Pro via AI Studio (1M context) |
| Q&A grounded in uploaded docs/ADRs | NotebookLM (Google) — separate product from Gemini but built on the same models |
| Cited research, fact-checking | Perplexity free (3 Pro Searches/day, 5 Deep Research queries/day); Gemini Deep Research for higher volume |
| Accuracy/hallucination verification | Run output through a different model than the one that wrote it (ChatGPT and Gemini are both fine free-tier cross-checks for Claude output). Perplexity Model Council exists for parallel multi-model synthesis but is Max-tier only ($200/month) |
| Image generation | ChatGPT Images 2.0 (thinking mode + 8-frame coherence for sequential consistency) or Gemini Nano Banana |
| Marketing copywriting | Claude Opus 4.7; ChatGPT for short-form punchy alternatives if Claude feels too measured |
| Legal copy drafts (Terms, Privacy Policy) | Claude Opus 4.7 for first drafts and plain-language summaries — always review with an actual lawyer before shipping |
| Alt text from image input | Claude Opus 4.7 (writes function-and-intent alt text, not pixel description) |
| Accessibility audits | Standard automated auditing tools first for deterministic WCAG checks, then Claude Opus 4.7 for contextual issues automation misses |

**Defaults:** Claude as spine. Extended Thinking on for hard tasks. Use Projects for context that persists across sessions. Cross-check important outputs with a second model.

---

# AI Tool Behavior Notes (May 2026)

Companion to the AI Tool Routing Cheat Sheet. This doc captures behavior-of-tools knowledge — quirks, defaults, and mental models — that affect *how* to use each tool, separate from *what* to use it for.

## Memory and context isolation

- **Claude Projects** isolate context to a single project deliberately. Prevents cross-project bleed but requires manually re-establishing context when switching projects.
- **Gemini with memory** is more fluid across projects but can silently bleed context from one to another without flagging it.
- **Mitigation:** When using any AI with persistent memory across sessions, periodically ask "what do you remember about me and my projects?" early in a session to surface cross-context assumptions before they affect advice.

## Brand bias in peer review

Every model tested defended its own ecosystem when asked to peer-review recommendations:
- Perplexity defended its own row, pushed against Claude-leaning defaults elsewhere
- ChatGPT pushed to upgrade Gemini versions to paid tiers and to add itself to coding
- Gemini framed Gemini-heavy recommendations as "industry consensus" and presented Figma MCP as a Gemini-specific advantage (it's not — it's model-agnostic)
- Claude over-weighted Claude as the spine

**Implication:** Single-model peer reviews are biased. Cross-checking across models is genuinely informative, but consensus signal is stronger than any individual review.

## Verifying unfamiliar product claims

Models with static training cutoffs make two opposite errors with comparable confidence:

**Direction 1: Fabricating products that don't exist.** Example: ChatGPT's "OpenAI Factify" was a hybrid hallucination (attaching OpenAI's brand to a real independent startup called Factify).

**Direction 2: Dismissing real products as hallucinations.** Three products initially flagged as hallucinations in this exercise are real:
- **Claude Mythos Preview** — Anthropic frontier model announced April 7, 2026. Restricted to Project Glasswing (a defensive cybersecurity consortium with ~40 partners including AWS, Apple, Google, Microsoft, NVIDIA). Not publicly available — does not appear in standard Claude product lineups for this reason.
- **Grok Build 0.1** — xAI terminal coding CLI launched May 2026 for SuperGrok / X Premium Plus subscribers. Real, but subscriber-only and outside the free-tier scope of this workflow.
- **Factify** — Tel Aviv-based startup, $73M seed round in January 2026, building a post-PDF intelligent document standard. Real company, not part of this workflow's routing decisions.

**Implication:** When a model confidently asserts a product exists with specific details (dates, benchmarks, links), web-search before dismissing as hallucination. Conversely, when a model confidently asserts a product exists with specific details but those details are *easy to confabulate* (vague benchmarks, no canonical sources), web-search before accepting. The verification step is the same in both directions; only the prior assumption differs.

## Doubling down under social pressure

When told there was peer consensus, models did not always self-correct previous claims — sometimes they generated more confident content, including additional unverified details. **Implication:** "Telling a model there's consensus" is not a reliable error-correction technique. Direct contradiction with specific verifiable facts works better.

## Free tier reality (verify before assuming)

Free tiers tighten frequently in 2026. Recent examples:
- Gemini 2.5 Pro free tier reduced from 100 to 50 RPD on May 7, 2026
- Perplexity Model Council is Max-only ($200/month), not in free or Pro tier
- Gemini 3.x Pro is paid/preview-only, not on free tier
- Perplexity free tier offers ~5 Deep Research and ~3 Pro Search queries per day (sources vary slightly on exact numbers)

**Implication:** Re-verify free tier limits quarterly. Don't rely on training data for current quotas.

## Vision model nuance

Claude Opus 4.7's April 2026 vision upgrade (3.75MP, dense UI focus) and Gemini's Figma-native integration are different strengths:
- Claude reads small typography and dense layouts at higher resolution
- Gemini integrates with Figma product flows more cleanly

Neither is universally better for design mockup evaluation. Try both on real work.

**Note on Figma MCP:** The Figma MCP server is a model-agnostic protocol that lets any compatible AI coding tool (Claude Code, Cursor, Copilot, Windsurf, Gemini) read Figma design metadata. It is not a Gemini advantage despite occasional marketing framings suggesting otherwise.

## When research mode pays off

Research mode (Claude) or Deep Research (Gemini, ChatGPT, Perplexity) earns its compute on:
- Comprehensive multi-source synthesis
- Landscape overviews with citations
- Comparisons across many options on several dimensions

Not worth it for:
- Single fact verification (use web search)
- Quick iterations on existing work
- Document editing
- Anything where waiting 5-15 minutes would feel excessive
