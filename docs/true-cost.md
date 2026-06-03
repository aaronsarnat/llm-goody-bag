# True Cost of Using LLMs

---

[back to Table of Contents](../README.md)

---

# True Cost of Using LLMs

*An open-source reference for estimating the energy, water, carbon, and social footprint of using frontier chat models — and for cross-checking AI-generated research so the numbers can be trusted.*

**Models in scope:** Claude (Anthropic), Gemini (Google), ChatGPT (OpenAI), Perplexity, and Le Chat (Mistral) — text, reasoning, research, and coding workloads, with image/video broken out separately.
**Last verified:** June 2, 2026. Figures change fast; treat every number as a dated estimate, not a meter reading.
**License:** Free to copy, adapt, and redistribute. Verify before you rely on it.

---

## TL;DR

1. **A single text prompt is tiny.** A median text prompt costs roughly **0.3 watt-hours, a fraction of a gram of CO₂, and well under a milliliter of water.** Independent estimates converge: Google measured 0.24 Wh / 0.03 gCO₂e / 0.26 mL for a median Gemini prompt; OpenAI's Sam Altman cited ~0.34 Wh; Epoch AI estimates ~0.3 Wh for a standard GPT-4o query.
2. **What you do with the model is the whole story.** A reasoning ("thinking") prompt costs **10–100× a standard one**; a long-context prompt **8–130×**; one 5-second AI video costs **~700× a single image and thousands of times a text prompt.** Your footprint is set by *task choice and volume*, not by which subscription you hold.
3. **A heavy text-only month is still a rounding error for an individual.** Realistic heavy use (hundreds of prompts a day, frequent reasoning and long context, no media) lands around **15–70 kWh, 6–28 kg CO₂e, and 30–130 L of water per month** — a few hours of flying, or one to a few beef burgers' worth of carbon, and a fraction of a percent of an average person's annual footprint.
4. **The real cost is collective, not personal.** Aggregate data-center demand is doubling to ~945 TWh by 2030, raising electricity bills (data centers drove 63% of one PJM capacity-price spike — $9.3 billion), straining water (two-thirds of new U.S. data centers sit in high-water-stress areas), and concentrating air pollution in frontline communities. None of this is meaningfully offsettable by one user.
5. **Offset honestly with durable removal, not cheap forestry.** Over 90% of the largest provider's rainforest credits were found to be "phantom," and fewer than 16% of credits across 2,346 projects represented real reductions. Budget for **biochar (~$164/tonne) or direct air capture**, not $5–15/tonne avoidance credits.
6. **Cross-check AI research before trusting it.** Running the same question through several models and verifying against primary sources catches confident errors that any single model will produce — including total topic derailment, fabricated citations, and false precision. Methodology for doing this is in Part 8.

---

## Part 1 — Rule-of-thumb per-task metrics

These are the building blocks. Multiply them by how often you do each kind of task. Express results as **ranges**, because the underlying sources disagree by 10–100× depending on model, prompt length, hardware, data-center location, and accounting method.

| Task | Energy (per task) | Notes |
|---|---|---|
| Standard short text prompt | **~0.3 Wh** (0.24–0.34) | The well-established anchor. Google, OpenAI, and Epoch AI converge here. |
| Long-context prompt (~10k tokens / a paper attached) | **~2.5 Wh** | ~8× a standard prompt (Epoch AI). |
| Very long context (~100k tokens / ~200 pages) | **~40 Wh** | Over 100× a standard prompt. |
| Reasoning / "thinking" prompt (long) | **~15–40 Wh** | Claude 3.7 Sonnet extended ≈ 17 Wh; o3 ≈ 39 Wh; DeepSeek-R1 ≈ 30–34 Wh (Jegham et al.). Roughly **10–100× a standard prompt**; up to ~700× in extremes. |
| Deep-research / multi-step agentic run | **~0.3–2+ kWh** | Bundles tens to hundreds of reasoning/tool steps. The single most expensive routine text workflow. |
| AI image (1024×1024) | **~0.6 Wh** (up to ~1.2 Wh) | MIT Technology Review, from Hugging Face data. |
| 5-second AI video | **~900 Wh** | ≈ running a microwave for an hour; ~700× an image; thousands of times a text prompt. The dominant line item if you generate media. |

**Converting energy to carbon** — multiply kWh by grid intensity:

| Grid | Intensity | Use when |
|---|---|---|
| France (e.g., Le Chat / Mistral, nuclear-heavy) | **~0.02 kg CO₂e/kWh** | Model is served from France or a comparably clean grid. RTE: 21.7 g (2024), below 20 g (2025). |
| Hyperscaler clean-procurement blend | **~0.05 kg CO₂e/kWh** | Provider reports high 24/7 carbon-free energy. Optimistic; market-based. |
| U.S. delivered average | **~0.39 kg CO₂e/kWh** | Default for U.S.-served workloads. EPA/eGRID 2022: 823 lb CO₂/MWh. |

**Converting energy to water** — multiply kWh by a water-use factor:

| Scope | Factor | Notes |
|---|---|---|
| On-site, best-in-class | **~0.15 L/kWh** | AWS 2024 water-use effectiveness (PUE 1.15). On-site cooling only. |
| On-site, typical-to-hot climate | **~0.5–1.5 L/kWh** | Varies enormously by site and season. |
| On-site + off-site (power generation) | **~1.8–1.9 L/kWh** | The fuller picture; off-site thermoelectric water is often omitted from headline figures. |

**Embodied (one-time) cost of the hardware** — usually excluded from per-query figures but real: an NVIDIA HGX H100 8-GPU baseboard carries **~1,312 kg CO₂e** of cradle-to-gate manufacturing emissions (~164 kg per GPU). Generative-AI e-waste is projected at **1.2–5.0 million tonnes cumulatively over 2020–2030** (Wang et al., *Nature Computational Science*, 2024), reducible 16–86% with circular-economy practices.

---

## Part 2 — Three-tier monthly framework

Pick the tier that matches the usage pattern. Ranges, not point estimates.

| Tier | Pattern | Energy/mo | Water/mo | Carbon/mo (US grid) |
|---|---|---|---|---|
| **1 — Light** | A few hundred standard prompts; little reasoning; no media | ~0.5–6 kWh | ~10–20 L | ~0.5–2.5 kg CO₂e |
| **2 — Heavy text** | Hundreds of prompts/day across tools; frequent reasoning + long context; periodic deep research; no media | ~15–70 kWh | ~30–130 L | ~6–28 kg CO₂e |
| **3 — Worst-case agentic** | Sustained 24/7 agent/coding loops; some image/video | ~150–700 kWh | ~300–1,300 L | ~60–280 kg CO₂e |

**Putting it in perspective.** Even Tier 2 (~6–28 kg CO₂e/month, ~70–340 kg/year) is **a small fraction of a person's footprint** — a U.S. resident emits roughly 13.6 t CO₂ (17.3 t CO₂e) per year. As Hannah Ritchie (*Our World in Data*) puts it, unless you're an extreme power user, daily AI questions are "a rounding error on your total electricity footprint" — she estimates ~2–3 g CO₂ per query, so 10 queries a day for a year adds ~11 kg CO₂ (~0.07% of an American's annual emissions). Comparison anchors: a round-trip transatlantic flight ≈ ~1.6 t CO₂e per passenger (with high-altitude radiative forcing); an average U.S. household uses ~865 kWh/month of electricity; a kilogram of beef ≈ ~22 kg CO₂e.

**The caution that matters:** a low *personal* number is not a clean bill of health for the *system*. See Part 5.

---

## Part 3 — What actually drives the footprint (the levers)

In rough order of impact:

1. **Media generation.** One 5-second video (~900 Wh) outweighs thousands of text prompts. If you generate images or video, that becomes your single largest line item by far. Generating no media keeps a heavy text month an order of magnitude lower.
2. **Reasoning / "thinking" mode.** 10–100× a standard prompt. Reserve it for tasks that genuinely need multi-step reasoning; don't default to it for lookups.
3. **Context length.** Stuffing a 100k-token context costs ~100× a short prompt. Trim context to what the task needs.
4. **Deep research / agentic loops.** Each run bundles many reasoning and tool steps (~0.3–2+ kWh). High value, high cost — use deliberately.
5. **Redundant cross-checking.** Asking the same question of three models triples the compute. Worth it for high-stakes outputs (see Part 8); wasteful for routine ones.
6. **Grid and provider choice.** A query on the French grid emits ~15–20× less carbon than one on the U.S. average. Providers procuring 24/7 carbon-free energy and reporting low water-use effectiveness lower the per-token footprint without changing your behavior.
7. **Model size / tier.** A small model (Haiku/Sonnet/4o-mini class) can cost ~10–70× less than a frontier reasoning model for an adequate answer. Right-size the model to the task.

---

## Part 4 — Where the models run (and how transparent they are)

Per-query footprint depends on the data center, its grid, and its cooling — so *which provider and region* often matters more than *which model*.

| Provider / model | Infrastructure | Transparency | Notes |
|---|---|---|---|
| **Google / Gemini** | Google's own TPU fleet | **Highest** | Published a per-prompt methodology (median 0.24 Wh); reports 66% carbon-free energy (2024) and water-replenishment goals. Caveat: median only; market-based carbon and on-site-only water are criticized (UC Riverside) as undercounting. |
| **Mistral / Le Chat** | European cloud, France | **Strong** | Full peer-reviewed lifecycle assessment (with Carbone 4 / ADEME). Cleanest grid (French nuclear). |
| **OpenAI / ChatGPT** | Microsoft Azure (+ Oracle / Stargate buildout) | **Minimal** | One unaudited datapoint (~0.34 Wh), no methodology, no Scope 1/2/3 disclosure. |
| **Anthropic / Claude** | AWS (Trainium / "Project Rainier," ~500k→~1M chips) + Google Cloud + Azure; additional capacity via an Anthropic–SpaceX deal (May 2026) and an Anthropic–Fluidstack $50B build (TX/NY) | **Lowest** | No per-query figures, no Scope 1/2/3. Footprint must be inferred from AWS efficiency metrics (WUE ~0.15 L/kWh) and third-party benchmarks. |
| **Perplexity** | Routes across providers: its own Sonar models plus OpenAI/Anthropic/Google/xAI, on AWS and Azure | **Not directly attributable** | A single query may run on any of several models and clouds; footprint is genuinely indeterminate per request. |

**Lifecycle note:** inference now dominates lifecycle emissions for a deployed model. Mistral's assessment of Mistral Large 2 (123B parameters) found training + inference accounted for **85.5% of greenhouse-gas emissions and 91% of water use** over 18 months; training alone emitted ~20,400 tonnes CO₂e and used ~281,000 m³ of water, and a single ~400-token response cost ~1.14 g CO₂e and ~45 mL of water.

---

## Part 5 — The systemic cost (where the real footprint is)

Individual inference is small; the aggregate is not, and its harms fall on specific communities.

- **Total demand.** The IEA projects global data-center electricity roughly **doubling to ~945 TWh by 2030** (from ~415 TWh in 2024). A single 100-MW data center can require **over 2 million liters of water per day**. U.S. data centers directly consumed **17.4 billion gallons of water in 2023**, projected to **38–73 billion by 2028**, plus ~211 billion gallons of indirect (power-generation) water (Lawrence Berkeley National Laboratory).
- **Electricity bills.** In the PJM grid, data centers drove **63% of the 2025/26 capacity-auction price increase — $9.3 billion** passed to customers; prices jumped 833%. The December 2025 auction cleared at the cap ($333.44/MW-day, $16.4 billion total), with the market monitor attributing **40% (~$6.5 billion) to data-center load.** NRDC estimates **$100–163 billion** in cumulative capacity costs through 2033 and roughly **$70/month** more per household by 2028.
- **Water stress.** A Bloomberg analysis (using World Resources Institute and DC Byte data) found about **two-thirds of new U.S. data centers built or in development since 2022 sit in high-water-stress areas**, with five states (Virginia, Arizona, Texas, Illinois, California) accounting for 72% of new builds.
- **Air quality and environmental justice.** xAI's "Colossus" operation ran dozens of **unpermitted gas turbines** (27, growing to 33) in majority-Black South Memphis and Southaven, Mississippi. The NAACP, Southern Environmental Law Center, and Earthjustice filed a Clean Air Act lawsuit (April 2026) and a preliminary-injunction request (May 2026); the turbines are estimated to emit **>1,700 tons/year of NOₓ, ~236 tons/year of fine particulates**, plus carbon monoxide and formaldehyde, in counties already graded "F" for ozone.
- **Embodied and mineral costs.** Manufacturing GPUs is carbon- and mineral-intensive (~1,312 kg CO₂e per 8-GPU baseboard), and the e-waste stream is projected in the millions of tonnes this decade.

**Takeaway:** the highest-leverage response is not personal abstinence but engagement — supporting standardized disclosure (an "Energy Star for AI," location-based carbon and full-lifecycle water reporting), dedicated large-load rate classes, and clean-power requirements for new data centers.

---

## Part 6 — Offsets done honestly

**Start by distrusting cheap credits.** A 2023 Guardian/Die Zeit/SourceMaterial investigation found **over 90% of the largest provider's rainforest (REDD+) offset credits were likely "phantom credits."** A 2024 meta-study in *Nature Communications* (Probst et al.) reviewing 2,346 projects and ~1 billion credits found **fewer than 16% represented genuine emissions reductions.** The voluntary market's 2024 average transacted price was just ~$6.34/tonne — cheap precisely because much of it is low-integrity avoidance crediting.

**Prefer durable removal:**

| Option | Indicative price | Notes |
|---|---|---|
| **Biochar** | **~$150–165/tonne** (Sylvera 2025 avg ~$164) | Best cost/integrity balance for an individual. |
| **Direct air capture** | **~$1,000–1,300/tonne** | Highest durability, highest cost. One flagship (Climeworks) faced a 2025 investigation finding delivered tonnage well below claims — verify delivery, don't assume it. |
| **Advance-market portfolios** (e.g., Frontier/Stripe Climate) | **~$400–1,000/tonne** | Weighted across vetted removal projects. |

**Consumer-facing providers** (directional; verify at purchase): Tradewater (refrigerant destruction; strong additionality), Wren (~$20/tonne diversified), Terrapass (~$6–17/tonne), Climeworks subscriptions (~$8–50/month, subject to the delivery caveat above). Screen any provider against the **ICVCM Core Carbon Principles** and independent ratings (Sylvera, BeZero, Calyx).

**What it costs to offset typical use.** A Tier-2 footprint (~70–340 kg CO₂e/year) costs roughly **$11–56/year via biochar** — affordable and credible. **Water is much harder to "offset"**; the better move is supporting watershed-replenishment in stressed basins and preferring low-WUE, clean-energy providers.

**Reality check:** offsetting your *personal* AI use is cheap and easy; the systemic grid/water/community costs are not individually offsettable and argue for model choice and civic engagement over guilt.

---

## Part 7 — A practical checklist for any user

1. **Right-size the model.** If a smaller/non-reasoning model suffices, the footprint is ~10–70× lower. Reserve reasoning, long context, and deep research for tasks that need them.
2. **Skip media unless necessary.** One video can outweigh a month of text prompts.
3. **Trim context.** Don't attach 200 pages when 2 will do.
4. **Cross-check only high-stakes outputs.** Triplicating compute is worth it for important answers, wasteful for routine ones.
5. **Prefer clean grids / transparent providers** where you have a choice.
6. **Offset the residual with durable removal** (biochar first), and budget realistically — single-digit dollars per year for typical use.
7. **Engage with the systemic issue.** Disclosure standards and siting/rate policy do more than any personal offset.

---

## Part 8 — Methodology: cross-checking AI research for accuracy

This document exists because **no single LLM's research output can be trusted on its own.** The reliable method is to run the same question through several models, then verify against primary sources — and to know the failure modes you're hunting for. The reports synthesized here (seven model runs across five products) produced a clean taxonomy of how AI research goes wrong, including two especially instructive failures.

### Two illustrative failures

**Failure A — circular sourcing and misattribution.** One report cited sources for nearly every claim, but **every citation resolved to the single uploaded input file**, not to any independent source. A report whose citations point only at its own input is verifying nothing. The same report **misattributed claims to the wrong models** — assigning one model's worst-case energy figure and its local-impact narrative to a different model — and falsely claimed that two of the input reports were "too incomplete to trust" when they were complete. Its *abstract* guidance (favor disclosed figures, label estimates, use ranges) was sound, which is the trap: **a degraded report can still sound reasonable while being useless on specifics.** Separate a model's reasoning quality from its factual reliability.

**Failure B — total topic derailment.** Another report, asked to analyze AI environmental footprints, instead produced a polished, citation-dense document about **an entirely different subject** (battery-industry commercialization), complete with data tables and a summary that falsely described the user's request. It was fluent, confident, and completely off-topic. **Fluency and formatting are not correlated with correctness**, and the single most important check is the simplest: *did the model answer the question I actually asked?*

### Taxonomy of failure modes to check for

1. **Topic derailment / instruction loss** — answering a different question than asked. Check first.
2. **Fabricated or circular citations** — sources that don't exist, or that point only back to the input or the model's own prior output.
3. **Cross-source misattribution** — assigning claim X to the wrong source or model.
4. **False precision** — over-precise numbers (e.g., "7,103.40 kWh/month") implying accuracy that the underlying evidence cannot support.
5. **Boundary / definition conflation** — comparing figures with different scopes as if equivalent (e.g., a short-prompt energy number against a long-prompt one; on-site water against full-lifecycle water).
6. **Entity conflation** — merging similarly named things, sometimes pulled from the prompt's own context (e.g., attributing a data center to the user's local utility rather than the correct one).
7. **Stale-vs-current confusion** — mixing an outdated figure with current ones, or citing the wrong version of an evolving paper.
8. **Plausible-but-wrong confidence — in both directions** — a confident claim that's false, *and* its inverse: a surprising claim that sounds fabricated but is actually true. (In this exercise, a deal that looked invented turned out to be real.) Don't accept *or* dismiss surprising claims without checking.

### The verification workflow

1. **Did it answer the actual question?** (Derailment check — do this before reading the content.)
2. **Do citations resolve to real, independent, authoritative sources?** Open them. Discount anything pointing to the input file, a content farm, or the model's own earlier output. Prefer primary sources (company reports, peer-reviewed papers, government data, named investigations).
3. **Is precision honest?** Numbers should be ranges where the evidence is uncertain. Be suspicious of decimal-point precision on inherently fuzzy quantities.
4. **Are system boundaries stated?** For energy/water/carbon, what's counted — chip only, or with cooling/overhead/off-site generation; market-based or location-based carbon?
5. **Triangulate contested claims** across at least two independent primary sources before believing them.
6. **Check surprising claims both ways** — verify the shocking-but-maybe-true, and don't rubber-stamp the confident-but-maybe-false.
7. **Mind version and date hygiene** — note which version of a paper and which year's figure you're citing.
8. **Run a fresh-thread red-team pass.** Hand the draft to a *different* model in a clean context and ask it to find errors. Iterate until a fresh set of eyes finds nothing — but apply steps 1–7 to the red-teamer's output too, because it will make its own mistakes.

### Why this works

Different models fail differently. One will derail, another will fabricate citations, a third will inflate a worst case by an order of magnitude, a fourth will conflate short- and long-prompt figures. Errors that are invisible inside one model's confident prose become obvious when two outputs disagree — disagreement is the signal that tells you where to dig. The cost is real (cross-checking multiplies compute; see Part 3), so reserve the full treatment for outputs that matter.

---

## Caveats and open uncertainties

- **Provider opacity persists.** Only Google and Mistral publish methodologies; Google's is for a *median* prompt, not heavy/reasoning use. OpenAI's single figure is unaudited. Anthropic publishes no per-query or Scope 1/2/3 data.
- **Benchmarks are estimates, not meters.** Inference benchmarks infer hardware and overhead and have been revised significantly across versions; real footprint depends on prompt length, batching, routing, location, and season.
- **Sources disagree by 10–100×.** Standard-query energy spans from a legacy ~3 Wh figure down to ~0.24 Wh; reasoning multipliers are reported as anywhere from ~10× to ~700×. Ranges in this document reflect genuine disagreement, not hedging for its own sake.
- **The worst-case tier is deliberately bounded.** Some model outputs produced multi-thousand-kWh monthly worst cases for a single user; those imply implausible throughput and are not decision-useful.
- **Water is the hardest number.** On-site, off-site, and lifecycle water differ by large factors, and "water-positive" replenishment pledges are less verifiable than carbon claims.
- **Offset pricing and provider integrity move.** Verify current prices, certifications, and — for engineered removal — actual delivered tonnage before purchasing.

---

## Detailed source list

**Per-query / per-token energy, water, and carbon (inference)**
- Google Cloud, "Measuring the environmental impact of AI inference." https://cloud.google.com/blog/products/infrastructure/measuring-the-environmental-impact-of-ai-inference/
- "Measuring the environmental impact of delivering AI at Google Scale," arXiv:2508.15734. https://arxiv.org/abs/2508.15734
- Sam Altman, "The Gentle Singularity." https://blog.samaltman.com/the-gentle-singularity
- Data Center Dynamics, "Sam Altman: ChatGPT queries consume 0.34 watt-hours of electricity and 0.000085 gallons of water." https://www.datacenterdynamics.com/en/news/sam-altman-chatgpt-queries-consume-034-watt-hours-of-electricity-and-0000085-gallons-of-water/
- Epoch AI, "How much energy does ChatGPT use?" https://epoch.ai/gradient-updates/how-much-energy-does-chatgpt-use
- Jegham et al., "How Hungry is AI? Benchmarking Energy, Water, and Carbon Footprint of LLM Inference," arXiv:2505.09598. https://arxiv.org/abs/2505.09598
- MIT Technology Review, "We did the math on AI's energy footprint. Here's the story you haven't heard." https://www.technologyreview.com/2025/05/20/1116327/ai-energy-usage-climate-footprint-big-tech/
- The Verge, on criticism of Google's per-prompt accounting. https://www.theverge.com/report/763080/google-ai-gemini-water-energy-emissions-study

**Reasoning-model energy multipliers**
- Hugging Face AI Energy Score (Sasha Luccioni et al.), leaderboard and discussion. https://huggingface.co/spaces/AIEnergyScore/Leaderboard
- SingularityHub, "Hugging Face Says AI Models With Reasoning Use [30×/100×] More Energy on Average." https://singularityhub.com/2025/12/15/hugging-face-says-ai-models-with-reasoning-use-100x-more-energy-than-those-without/

**Lifecycle assessment**
- Mistral AI, "Our contribution to a global environmental standard for AI" (Mistral Large 2 LCA, with Carbone 4 / ADEME). https://mistral.ai/news/our-contribution-to-a-global-environmental-standard-for-ai

**Macro energy demand, grid mix, geography**
- IEA, "Energy and AI." https://www.iea.org/reports/energy-and-ai
- IEA, "Key Questions on Energy and AI." https://www.iea.org/reports/key-questions-on-energy-and-ai
- Lawrence Berkeley National Laboratory, Shehabi et al., "2024 United States Data Center Energy Usage Report" (LBNL-2001637). https://eta.lbl.gov/publications/2024-lbnl-data-center-energy-usage-report
- RTE (Réseau de Transport d'Électricité), French Annual Electricity Review (carbon intensity). https://analysesetdonnees.rte-france.com/en/annual-review-2024/keyfindings
- EPA, Greenhouse Gas Equivalencies Calculator (eGRID, U.S. grid intensity). https://www.epa.gov/energy/greenhouse-gas-equivalencies-calculator

**Water use and community impacts**
- Bloomberg, "The AI Boom Is Draining Water From the Areas That Need It Most." https://www.bloomberg.com/graphics/2025-ai-impacts-data-centers-water-data/
- Amazon Sustainability, AWS Cloud (WUE 0.15 L/kWh, PUE 1.15, 2024). https://sustainability.aboutamazon.com/products-services/aws-cloud
- IEEFA, "Projected data center growth spurs PJM capacity prices by factor of 10." https://ieefa.org/resources/projected-data-center-growth-spurs-pjm-capacity-prices-factor-10
- Monitoring Analytics (PJM Independent Market Monitor), RPM auction analyses. https://www.monitoringanalytics.com
- NRDC, "Building Data Centers Without Breaking PJM." https://www.nrdc.org/bio/tom-rutigliano/building-data-centers-without-breaking-pjm
- Utility Dive, "Data centers were 40% of PJM capacity costs in last auction." https://www.utilitydive.com/news/data-centers-pjm-capacity-auction/808951/
- Southern Environmental Law Center; Earthjustice; NAACP — xAI Memphis data-center air-pollution litigation. https://www.selc.org / https://earthjustice.org / https://naacp.org

**Embodied carbon and e-waste**
- NVIDIA, "Product Carbon Footprint Summary for HGX H100." https://images.nvidia.com/aem-dam/Solutions/documents/HGX-H100-PCF-Summary.pdf
- Wang et al., "E-waste challenges of generative artificial intelligence," *Nature Computational Science* (2024). https://www.nature.com/articles/s43588-024-00712-6

**Carbon offsets — integrity and pricing**
- The Guardian / SourceMaterial / Die Zeit investigation of Verra rainforest credits (summary via Carbon Brief). https://www.carbonbrief.org
- Probst et al., "Systematic assessment of the achieved emission reductions of carbon crediting projects," *Nature Communications* (2024). https://www.nature.com/articles/s41467-024-53645-z
- Sylvera, carbon-offset price and biochar reliability analyses. https://www.sylvera.com/blog/carbon-offset-price / https://www.sylvera.com/blog/biochar-carbon-credits
- ETH Zurich, on the cost of direct air capture. https://ethz.ch/en/news-and-events/eth-news/news/2024/03/cost-of-direct-air-carbon-capture-to-remain-higher-than-hoped.html
- Senken / Ecosystem Marketplace, voluntary carbon credit prices. https://www.senken.io/academy/carbon-credit-price

**Provider infrastructure**
- Anthropic, "Anthropic invests $50 billion in American AI infrastructure" (Fluidstack, TX/NY). https://www.anthropic.com/news/anthropic-invests-50-billion-in-american-ai-infrastructure
- Semafor, "AWS' mega multistate AI data center is powering Anthropic's Claude" (Project Rainier). https://www.semafor.com/article/10/29/2025/aws-massive-multi-state-ai-data-center-is-powering-anthropics-claude
- Microsoft, "Inside the world's most powerful AI datacenter" (Mt. Pleasant, WI / Fairwater). https://blogs.microsoft.com/blog/2025/09/18/inside-the-worlds-most-powerful-ai-datacenter/
- Google, Sustainability (TPU fleet, carbon-free energy, water replenishment). https://ai.google/sustainability/

**Perspective and equivalents**
- Hannah Ritchie, *Sustainability by Numbers* (Our World in Data), on the per-query footprint in context. https://www.sustainabilitybynumbers.com
- U.S. Energy Information Administration, average residential electricity use. https://www.eia.gov

*All URLs were checked on June 2, 2026. Several secondary claims (e.g., specific reasoning-energy estimates from individual labs, certain provider water figures, and an IEA April-2026 update) are plausible but were not independently re-verified to a single primary source in this pass and should be confirmed before high-stakes use.*

---

## About this document

This reference was produced by comparing **seven independent AI-generated research reports** (across Claude, Gemini, ChatGPT, Perplexity, and Le Chat) that were each asked the same question about the end-to-end environmental cost of using frontier LLMs. The reports were cross-checked against one another and against primary sources to identify agreements, resolve contradictions, and flag inaccuracies — including fabricated citations, misattributed claims, false precision, an order-of-magnitude-inflated worst case, an entity conflation, and one report that derailed onto an entirely unrelated topic. The surviving, verified takeaways were then generalized — decoupled from any individual's specific subscriptions — into this open-source reference. The cross-checking method itself is documented in Part 8 so the process can be reused and audited. Treat every figure as a dated estimate, verify before you rely on it, and contribute corrections.
