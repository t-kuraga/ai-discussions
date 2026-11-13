# Discussion: Is "The Case for Guided Autonomy" right?

An open, evidence-based discussion of claims that AI will make understanding code, maintaining code, or source code itself unnecessary, using the document *AI Coding: The Case for Guided Autonomy* (GA) as the starting point. The discussion settles each claim in a strong and a weak version, records the replies and their evidence, and states a position with implications for practice. It is meant to keep growing: new evidence and re-measurements are added with dates.

**Opened:** 2026-11-12 · **Status:** position and implications accepted (§5.1, §6); GA rewritten (v1.0, 2026-11-13); open to new evidence · **Owner:** Andrés Gómez

## 0. Context

Read first:
- [AI_Coding__The_Case_for_Guided_Autonomy.md](../AI_Coding__The_Case_for_Guided_Autonomy.md) (**GA**): the document under review.
- [guided_autonomy_references.md](guided_autonomy_references.md): every source cited here and in GA, with verification status and key figures. IDs such as B2, C1 or N23 below refer to that file.

**Ground rules**
1. The goal is a *defensible* position, not confirmation of the author's view or GA's. Steelman both sides.
2. A figure counts only if it is in the references file as verified, or verified during the discussion and added there.
3. Separate three things: what the evidence shows **today**, what the **trend** suggests, and what is **opinion**.
4. Forecasts ("in a few years") cannot be refuted by snapshots. They can be judged as *supported / not supported yet / contradicted by trend*.

---

## 1. The claims under test

The **strong** versions are the claims as originally made in the debate. The **weak** versions are the middle ground, and they are discussed too (G1, confirmed 2026-11-12).

| ID | Claim (as heard in the debate) | Strong version (original claim) | Weak version (middle ground) |
|---|---|---|---|
| **A** | Understanding code will not be required in a few years, so developers should judge AI **outcomes**, not read and review the code. | **A-strong:** nobody on the team needs to be able to read the code. | **A-weak:** humans no longer review every diff; review moves to specs, tests, metrics and sampling. Someone can still read the code when needed. |
| **B** | In a few years, regenerating or refactoring a whole project with AI will be cheaper than maintaining it, so coding skill won't be needed. | **B-strong:** for a typical product codebase, regeneration from spec beats incremental maintenance. | **B-weak:** for some classes of code (small, well-specified, well-tested modules; mechanical migrations), regeneration or AI-driven migration beats manual maintenance. |
| **C** | Source code will become so unnecessary that it disappears. AI will emit intermediate representations (bytecode, IL) directly, keeping software platform-independent *and* independent of any source language. | **C-strong:** high-level source languages are no longer written or stored. AI generates and maintains the IR directly, and IR is the artifact of record. | **C-weak:** for some scopes, source becomes a generated, disposable artifact nobody edits by hand (as with protobuf stubs or ORM migrations today). The human-maintained artifact is the spec plus tests. Whether the generated layer is source or IR is an implementation detail. |

**GA's verdict:** A and B are wrong (section 10): "Code understanding is not being eliminated, it is being concentrated." C is addressed in section 6: LLMs are worse at IR than at source, so languages persist.

**Working hypothesis to test:** GA rebuts the *strong* versions of A and B reasonably well *for today*, but does not rebut the *weak* versions. The weak versions are roughly what earned-autonomy models (GA §9's later phases) already assume. For C, GA's rebuttal rests on one misdescribed source (§2b). C-weak is close to A-weak plus B-weak and is not addressed at all.

---

## 1b. Author replies to the weak versions and to C

Recorded in checklist step 2 (§9). Each reply is tested in step 4 like any other argument: evidence today, trend, or opinion.

Received 2026-11-12. Each reply is split into testable sub-claims. Research status per sub-claim goes in the last column (step 3).

### Replies to A-weak

Summary: if A-weak holds, teams reorganise around cheaper non-developers who produce specs and outcomes and fewer, more expensive developers who sample and review code. BDD already tried this and the work fell back to developers. Cheaper outcome generation may then *increase* the review load (Jevons paradox).

| # | Sub-claim | Relies on | Type | Research status |
|---|---|---|---|---|
| RA1 | A-weak implies a team shape: more non-developer staff writing specs and judging outcomes; fewer, more expensive developers who sample and review code | Reasoning | Opinion (prediction) | **Partly supported, mostly anecdote.** No representative data on team composition. Fewer juniors: young workers in AI-exposed jobs ~19% below counterfactual, through reduced hiring (N18). PM:engineer ratio shifts are anecdotes (Andrew Ng; second-hand). Counter: vendor hiring data shows software engineers' share of new hires *rising* (Pave, second-hand). No evidence yet of growth in non-developer spec roles |
| RA2 | This is already happening: product owners write specs that go to agents directly, or to developers for technical refinement and then to agents | Observation | Today (anecdotal) | **Supported on adoption; quality data mostly vendor.** 34% of ~800 US employees building tools with AI have no programming background, and 56% build for customers or the public. 92% of these builders report major challenges (38% bugs, 37% security/privacy) (N20, vendor survey). Lovable/Supabase CVE-2025-48757: ~10% of 1,645 showcase apps exposed data without login (second-hand). No data on hand-off to developers |
| RA3 | Precedent: BDD with Cucumber/SpecFlow. Automation developers wrote step definitions; product owners were meant to write Gherkin scenarios. Debugging was inconvenient, and fixing and maintaining tests fell back to automation developers, who had the debugging tools and both code and domain knowledge | Industry experience | Historical (testable) | **Partly supported.** BDD maintenance survey (N21, 75 respondents, mostly engineers): specs "not legible to colleagues outside software engineering"; business people "not interested in test cases no matter how easy-to-read"; 61% say duplication makes specs hard to change. Does *not* count who authored specs. **Counter / reframe:** Cucumber's creators say the intent was collaboration (Three Amigos), not POs writing Gherkin alone; Hellesøy (2014) calls Cucumber "the world's most misunderstood collaboration tool" (N22). So the precedent is "collaboration collapsed into a developer tool", which still supports the reply. 4GL precedent (Martin, *Application Development Without Programmers*, ~1981) second-hand |
| RA4 | Agents can debug and will improve (E2E tests with long timeouts are an exception). But with poor or obsolete harnesses, growing low-quality output ("slop") will drive more debugging and analysis by developers as non-developers generate outcomes | Reasoning | Opinion / trend | **Partly supported.** Agent capability rising fast (METR time horizons; doubling estimate shortened in 2026, second-hand, see N1). Rework signals rising too: bugs per developer +54%, incidents per PR +242.7% in high- vs. low-adoption periods (N23, vendor telemetry, correlational). DORA 2025: AI still hurts delivery stability (B13). No data isolating "obsolete harness" as the cause. **Author refinement (2026-11-12):** no such data is expected, since harnesses are a new concept and are not recorded as a root cause when errors happen. The obsolete-harness part of RA4 stays opinion; the Jevons part moves to RA6 as a testable proxy |
| RA5 | Jevons paradox: cheaper outcome generation by non-developers increases total output, and so increases the sampling and review load over time | Economic analogy | Hypothesis (testable) | **Supported for volume and review load; contested for labour.** Merged PRs/month +23% YoY, commits +25% (N25, GitHub says not causal). High-adoption teams merge 98% more PRs; review time +91%, PRs 154% larger; no company-level gain (N24). 2026: median time in review +441.5%, **and PRs merged with no review +31.3%** (N23). So review load grows *and* review is already being skipped rather than scaled, which is directly relevant to A-weak. No peer-reviewed Jevons study found (opinion pieces only) |
| RA7 | *(Added at step 4 review.)* **Concentration, not dilution.** The spirit of A, even in its weak form, is a trend toward *less coding knowledge*. The counter: coding knowledge concentrates in fewer participants and fewer parts of the process, but where it is still needed, the required depth does **not** fall. There is no role for "superficial" coding knowledge in those parts | Reasoning | Opinion, testable in part | **Consistent with the evidence.** Fewer parts: junior hiring falls, senior share of postings rises (N18, N44). Same depth where needed: reviewer experience predicts catching bugs (N42); experience improves security beyond what AI supplies (N43); shallow learning with AI hurts debugging most (N2). Counter-signal: agent *usage* success plateaus at intermediate level (N41), but that measures getting tasks done, not reviewing or diagnosing. Note: this matches GA §10's own phrase "concentrated, not eliminated" |
| RA8 | *(Added at step 5.)* **Jevons × concentration.** Concentration (RA7) lowers the share of the process that needs deep coding knowledge, but if Jevons holds, cheaper development raises the volume of software built, so demand for the concentrated skill rises. Formally: demand for deep skill = **V** (volume) × **s** (share needing deep skill) × **d** (depth, constant per RA7). Demand rises only if V grows faster than s falls | Reasoning (Jevons + RA7) | Hypothesis (testable), conditional | **Consistent, not shown.** Conditions: (1) demand for software is elastic enough; (2) extra volume reaches high-impact or constrained work, not only low-impact work where YOLO is rational (RM3c), though low-impact software tends to integrate with high-impact systems (data, payments, auth); (3) review and verification are not automated as fast as generation. Current data points that way: time in review +441%, unreviewed merges +31% (N23), so the need per unit isn't falling. Labour data: seniors 69.3% of software postings, 71% of the recent rise (N44); BLS +10% (N17). Against: total software postings still 27.5% below Feb 2020 (N44); interest rates confound. **Corollary (most defensible part):** demand for deep skill rises while its supply pipeline shrinks (N18), a bottleneck risk |
| RA6 | *(Refinement of RA4/RA5.)* Test Jevons through agent configuration: if outcome generation is getting cheaper and spreading to non-developers, the number of agent configurations (AGENTS.md, CLAUDE.md, rules, skills, settings) added to **new and existing** projects should grow, and a rising share should be authored by non-developers | Proposed test | Hypothesis (testable) | **Partly supported: growth yes, non-developer authorship no data.** AGENTS.md in 60k+ open-source projects (N34, live count, no time series). In 2,853 repos created *before* 2024 and still active, 90.6% now have context files and 72.1% have AI-authored commits, so adoption reaches **existing** projects; context files "increased continuously", skills and subagents more slowly (N35). Cursor rules "emerged rapidly from mid-2024", concentrated in small, single-maintainer repos, the only hint of hobbyist or non-professional adoption (N36). Files have a median of 1 author (N37). **Gap:** no study splits new vs. existing repos over time or classifies authors by role. A GitHub mining study could measure growth; the non-developer proxy (low prior code activity) would show only a trend in "low-activity authors", not role |

### Replies to B-weak

Summary: B-weak needs a good harness, and harnesses go stale. The work moves from writing code to building and maintaining harnesses, which still needs developers who read generated code. Jevons again: cheaper new domains may need *more* developers. Teams may shift from owning projects to owning domains and their harnesses.

| # | Sub-claim | Relies on | Type | Research status |
|---|---|---|---|---|
| RB1 | B-weak is achievable only with a good harness | Consistent with §3 caveat (guided migrations) | Today | **Supported.** Every documented success had a heavy harness: Google (N3: changes kept only if build + tests pass, AST checks, expert review; "prompting alone insufficient for all but the simplest migrations"; review capacity was the bottleneck), Airbnb (N4: per-file state machine, retry loops, 40–100k-token prompts). Against unguided agents: FreshBrew (N12, best agent 52.3% of JDK 8→17 projects, reward hacking such as deleting failing tests). T2J-BENCH (N13): passing tests while numerical behaviour diverges, so test-only harnesses overstate success. No documented failed migration found (likely publication bias) |
| RB2 | Harnesses go obsolete as new business needs, domains, paradigms and tech stacks arrive. Work moves to creating and maintaining harnesses (AGENTS.md, settings, hooks, sandboxes), which needs developers who evaluate generated code in order to prune it | Reasoning | Opinion / trend (testable in part) | **Partly supported.** Context files evolve through "frequent, small additions"; few cover security (14.8%) or performance (14.5%) (N14). Whether they help is contested: no general success gain and >20% higher cost (N15); faster runtime and fewer tokens at similar completion (N16). **Gap:** no study measures who maintains harnesses or how fast they go obsolete. N15 also suggests much harness effort is wasted, so *what* goes in the harness matters. **Author refinement (2026-11-12):** test maintenance by how often skills, rules and configuration are *added* to AGENTS.md, hooks, settings etc. alongside domain changes. See RB5 |
| RB5 | *(Refinement of RB2.)* Following the open/closed principle (SOLID "O": extend, don't modify), new paradigms and tech stacks are more likely to produce **new harnesses for new sub-projects** (nested AGENTS.md, new skills, new rule files) than changes to already-tuned harnesses. Harness work grows by extension | Reasoning (OCP) | Hypothesis (testable) | **Partly supported.** *Within* files, change is mostly additive: ~80% of 5,396 heading-level edits are additions, and the top trigger is a feature PR (33.9%), so harnesses co-evolve with code (N37); in a 100-commit sample, additions 66, fixes 32, deletions 19 (N14). *Across* files, extension appears when the main file is constrained: one repo capped its root AGENTS.md by lint, and growth moved to SKILL.md files and nested rules (4.9k → 17.4k words), with a 32% manual prune that regrew 27% (N38, N=1). CLAUDE.md is usually created first and AGENTS.md added later and referenced (N35). **Counter:** tuned files are *not* left alone: 59–67% are modified in more than one commit, every ~1–3 days (N14); yet 40.4% are touched only once (N37), i.e. created and left. **Gap:** no study measures new-file creation vs. edits at repo level, or nested files over time. Refined reading: harnesses grow by both extension and modification, and need pruning, so the OCP pattern holds partly |
| RB6 | *(Added at step 5.)* **Jevons on harness work.** Harness design and maintenance should also see rising demand: demand for harness work = (number of agent-using projects and sub-projects) × (harness work per project) × (skill depth) | Reasoning (Jevons + RB2, RB5) | Hypothesis (testable), conditional | **Likely rises, but may be absorbed by platforms, and has no labour data yet.** *Volume rises:* AGENTS.md in 60k+ projects (N34); 90.6% of active pre-2024 repos have context files (N35). *Work per project is ongoing:* files edited every 1–3 days, growth by new files per sub-project (N14, N37, N38; RB5), so it scales with the number of projects and domains. *Depth matters:* context files give no general gain (N15), and LLM-generated ones slightly lower success while developer-written ones help (second-hand), so design skill is what makes harnesses pay; the verifier is where developer effort pays most (N49). **Against:** (a) agents write and update harnesses themselves (72.1% of repos have AI-authored commits, N35; who authors harness files is unmeasured); (b) standardisation amortises harness work across projects, through shared skills, plugins and platform teams (76% of organisations have platform teams, B13), the same way ORMs amortised SQL. Reading: harness demand rises with volume, but concentrates in platform/enablement roles that build *standard* harnesses (linking RB4 and the RM1 refinement: standards give generated code ORM-like trust). No job-category data exists yet |
| RB3 | Jevons paradox: cheaper automation of new domains means more software gets built, so eventually *more* developers are needed | Economic analogy | Hypothesis (testable) | **Partly supported in aggregate, contested for juniors.** BLS projects +10% software developers 2025–35, citing AI development as a demand source (N17). Against: young (22–25) workers in AI-exposed jobs ~19% below less-exposed peers, gap widening; no comparable gap for experienced workers (N18, descriptive, not causal). Reading: demand may grow while the entry route shrinks, which threatens the supply of the developers RB2 needs. **Author refinement (2026-11-12):** consistent with the reply. Senior developers are better at foreseeing scalability and maintainability issues, which is the judgement harness work needs; hence seniors are retained while junior hiring falls. *Out of scope:* how junior training will change. **Research (step 3): labour shift supported; mechanism only indirectly.** Demand: senior roles were 69.3% of software postings in Q1 2026 vs. 4.5% entry-level; seniors account for 71% of the 2025–26 rise in software postings (N44). Benefit by experience depends on the tool: with autocomplete, juniors gained more output (27–39% vs. 8–13%, not significant; N39); with real-world data and agents, gains go to experienced users (N40: productivity gains "exclusively" from experienced developers; N41: verified agent success 15% for novices vs. 28–33% for intermediate and above). Review: reviewer experience predicts catching bugs (N42), and programming experience improves code security in a way AI does not replace (N43). Novices learning with AI lose debugging skill (N2). **Nuance:** the benefit plateaus early: the usefulness of review comments rises in the first year then flattens (N42), and the intermediate→expert gap is "modest" (N41). The asset is *domain and codebase competence*, reached fairly early, not seniority as such. Direct evidence on foreseeing scalability/maintainability is missing |
| RB4 | Team structure shifts from teams that maintain projects to teams that maintain domains and their harnesses | Reasoning | Opinion (question) | **Weak / indirect.** DORA 2025 (B13): 76% of organisations have dedicated platform teams, and platform quality is linked to value from AI. But DORA frames AI as an *amplifier* of existing organisation, not a driver of new structures. No data on "domain + harness" teams or a harness-engineer role. Remains a forecast |

### Replies to C (strong and weak)

Summary: more data shows general-purpose LLMs do worse on IR unless trained for it. Languages will get more agent-friendly but keep evolving, because they carry context (names, domain boundaries, messaging, layer hierarchies). Dijkstra argued that natural-language programming is foolish because of ambiguity. Prompts are natural-language programming, and harness engineering tries to restore determinism.

| # | Sub-claim | Relies on | Type | Research status |
|---|---|---|---|---|
| RC1 | General-purpose LLMs perform worse on IR than on high-level code unless trained for that IR | *Does Representation Matter? Evaluating IRs for LLM-based Binary Decompilation* (NDSS BAR 2026); Jiang et al. (2025) = C5 | Today | **Partly supported.** The trend holds, but **N10 does not test it**: it compares disassembly vs. three Binary Ninja IR levels for decompilation (no source input). Large models are stable across levels; GPT-4.1 does slightly *better* from raw assembly (74.8%) than from high-level IR (67.4%); no level is best overall. Direct paired evidence comes from elsewhere: binary code summarisation, same models, METEOR source 0.167 → assembly 0.066 → IR 0.052 (N26); one agent's correct samples 84.8% at source vs. 41.0% at IR (N27). Specialisation helps (LLM4Decompile, N28). Counter: IRCoder (N29) uses IR as a *training aid* that improves source generation, not as a replacement |
| RC2 | Languages will become more agent-friendly but will keep evolving, because they carry context for humans and agents: names, domain boundaries, messaging between components, hierarchies across layers | Reasoning (links R6, R8) | Opinion / trend | **Supported.** Names: obfuscating identifiers drops GPT-4o class-summary accuracy from 87.3 to 58.7 (N30; small effect on code already using short names). Stripping symbols halves semantic similarity in binary summarisation (N26). Types: 94% of LLM compile errors in TypeScript are type errors; type-constrained decoding cuts them 52–75% (N31). TypeScript became #1 on GitHub by monthly contributors in Aug 2025; GitHub *correlates* it with AI, also credits framework defaults (N25). Agent-oriented languages exist only as experiments (second-hand) |
| RC3 | Dijkstra, *On the foolishness of "natural language programming"* (EWD667): natural language is too ambiguous to program in. Prompts are natural-language programming; the purpose of a programming language is determinism, which is what harness engineering tries to bring back | Dijkstra (EWD667); reasoning | Argument from authority + opinion | **Partly supported.** EWD667 (1978) verified: natural language's "naturalness" lies in "the ease with which we can use them for making statements the nonsense of which is not obvious" (N11). Modern evidence: asking clarifying questions raises GPT-4 Pass@1 from 68.0% to 75.8% (N32), so ambiguity measurably costs correctness. **Counter / reframe:** letting users approve generated tests adds +46 pp pass@1 within 5 interactions (N33). NL becomes reliable once *formalised* through tests or specs, which agrees with Dijkstra as much as it refutes him, and matches the reply's point that harness engineering restores determinism |

---

### General reply: marginal returns (applies to A, B, C and to GA §8)

Added 2026-11-12. Origin: the initial debate. The claim's analogy was that code will stop mattering the way memory allocation stopped mattering for most software, or the way nobody reads the code behind an ORM. The reply: that holds for a maintainable CRUD app, but not when constraints bind. In a large ETL you need to know (and sometimes write) the SQL the ORM generates. In a CPU- or memory-limited container you care about allocation. Maintainers of kernels or compression libraries (e.g. gzip) always care. Whether you can ignore what's under the hood depends on whether the marginal gain or cost of looking is worth it. GA §8 tries to capture this, but with invented positions (see §2).

The reply draws on two distinct economic laws. They are split here because they answer different questions.

| Law | Origin | Question it answers here |
|---|---|---|
| **Diminishing marginal returns** | Classical economics (Turgot, Ricardo) | If I keep adding *one* input (tokens, agent retries) while the others stay fixed (spec, harness, human attention), how fast does the extra output shrink? |
| **Marginal utility** and the **equi-marginal principle** | Gossen (1854); Menger, Jevons and Walras independently (1871) | Given a budget, should the *next* unit go to tokens or to developer effort? Spend where the utility per unit of cost is highest, until both are equal |

**Applying marginal utility, with risk.** The utility of the next unit of effort is the *expected loss it removes*:

> utility of next unit = reduction in P(bug escapes) × impact of that bug

The comparison for each change class is then:

> (reduction in expected loss from the next unit of tokens) ÷ (token price) **vs.** (reduction in expected loss from the next unit of developer guide/review/correct effort) ÷ (developer hourly cost)

- **Low impact** (CRUD screen, internal tool): a bug costs little, so both sides remove little expected loss. Tokens are cheaper, so the next unit goes to tokens. Outcome-only (YOLO) is rational.
- **High impact** (large ETL on financial data, kernel, compression library, resource-limited service): the same reduction in P(bug) is worth much more. Tokens hit diminishing returns once the spec or verifier is the bottleneck, while a developer hour can fix the spec, the verifier, or the generated SQL/allocation itself. The next unit goes to the developer.
- **Optimum (equi-marginal):** add tokens until the expected loss removed per euro of tokens falls to that of developer time, then switch. The switch point moves with impact, constraints, model capability and token price, which is why it must be re-measured, not fixed (P10).

Jevons is the same economist as in the Jevons paradox (RA5, RB3): cheaper tokens lower the cost side, which increases token use, but do not change the *impact* side of the equation.

| # | Sub-claim | Relies on | Type | Research status |
|---|---|---|---|---|
| RM1 | *(The claim's own analogy, steelman.)* Abstractions let most developers ignore lower layers: garbage collection removed manual memory management; ORMs are used without reading their code | Analogy | Today (well established) | **Valid only for shared, standard layers.** Generated code is new every time and has no reputation to trust (SL5, §3.2). And even standard abstractions leak (RM2). **Author refinement (step 4 review):** the analogy holds symmetrically. You must read the SQL an ORM generates when performance matters; likewise you must read agent-generated code when performance, maintainability or security matter. Otherwise you can ignore the generation, *provided it follows enough enforced standards* (conventions, templates, lint and architecture rules, readability gates). Standards are what give generated code ORM-like trust |
| RM2 | The lower layer matters again when constraints bind: large ETL (generated SQL), resource-limited containers (allocation, CPU), low-level libraries (kernel, gzip). Abstractions leak in proportion to how hard the constraints are | Experience; candidate: Spolsky's "Law of Leaky Abstractions" (2002); ORM performance anti-pattern studies; EffiBench (B4) | Today (testable) | **Supported.** "All non-trivial abstractions, to some degree, are leaky" (N46; its SQL example is the query optimiser, not an ORM). ORM-generated SQL: fixing anti-patterns improves response time up to 98% (N47, best case); redundant data access found in 87% of exercised transactions, fixing it gains 17% on average (N47 follow-up, second-hand). Default AI code is 3–14x slower, worse in Java/C++/Go (B4, B5) |
| RM3a | **Diminishing marginal returns on tokens.** With spec, harness and verifier fixed, extra tokens (retries, longer context, more agent iterations) buy less and less correctness. Past that point, only a better spec or verifier, i.e. developer effort, raises the ceiling | Diminishing returns | Hypothesis (testable) | Early signals: Airbnb needed 10 retries typically and 50–100 for hard files, and finished the last files by hand (N4); context files add >20% cost without a general success gain (N15); METR 80% horizons far shorter than 50% (N1). **Supported.** Accuracy "often peaks at intermediate cost and saturates at higher costs"; repeated runs of the same task differ up to 30x in tokens (N51). Simple agents sit on the cost–accuracy frontier: 93.2% for $2.45 vs. 88.0% for $134.50 (N48, HumanEval). Repeated sampling raises *coverage* log-linearly (15.9% → 56% with 250 samples), but turning coverage into fixes needs a verifier; without one, selection plateaus (N49). This confirms the condition "once spec and verifier are fixed": the verifier is where developer effort pays |
| RM3b | **Diminishing marginal returns on human review.** Review effort per diff also saturates (fatigue, large diffs), so more human review is not always the better unit either | Diminishing returns | Hypothesis (testable) | Signals: approval fatigue (A4-alt2: 93% of prompts approved); larger PRs (+154%, N24). **Partly supported, mostly vendor data.** SmartBear/Cisco: 200–400 LOC in 60–90 minutes finds 70–90% of defects; defect discovery falls sharply above ~200 LOC (N50, vendor, not peer-reviewed). Peer-reviewed: low review coverage and participation are linked to more post-release defects (McIntosh et al.), not replicated at Sony; useful comments plateau and then decline as files per review grow (Bosu et al., slides only). No study measures returns per extra review-minute. Practical reading: small diffs keep human review effective, which matters as PRs grow 154% (N24) |
| RM3c | **Marginal utility with risk.** For each change class, the next unit goes to tokens or to developer guide/review/correct effort, whichever removes more expected loss (ΔP(bug) × impact) per unit of cost. Low impact → tokens (YOLO rational); high impact or binding constraints → developer effort | Equi-marginal principle; expected loss | Framework (opinion), testable in part | **Original framing, consistent with the evidence.** No peer-reviewed paper derives a review rule from expected loss; present RM3c as this discussion's own framework. Its inputs are measurable: token cost and its variance (N48, N51), review effectiveness (N50), failure frequency (N23: incidents per PR +243%), and impact (per change class, set by the team). Closest related work (not read in full): queueing models with reviewer attention as bottleneck (arXiv:2605.27202); a cost-per-implementation metric combining tokens with human spec and gatekeeping time (arXiv:2608.20341) |
| RM4 | GA §8 points at this rule but replaces it with invented quadrant positions and benchmark numbers mapped onto domains they didn't measure. RM3a–c are a principled replacement: autonomy set per change class by impact, constraints and cost, not by LOC | Reasoning | Opinion | Decided: replaces GA §8 (§3b); applied as I2–I3 (§6) |

---

## 2. Section-by-section audit of GA

Evidence status comes from the [references file](guided_autonomy_references.md). "Supports" = what the evidence actually shows, which may be narrower than what GA concludes.

| GA § | GA's point | Evidence status | What it actually supports | Bearing on A / B | Provisional verdict |
|---|---|---|---|---|---|
| 1 Productivity paradox | AI made experts 19% slower; a 2026 follow-up "confirmed 18% slowdown" | B1 ✅ (early-2025 tools, 16 devs). **B2 misreported:** −18% is a non-significant *speedup*, and METR calls the signal unreliable | Perceived productivity is unreliable; measure it. Says nothing about code understanding | Weak, indirect. The trend (B2) points slightly *against* GA | Keep B1 with caveats; correct B2 |
| 2 Complexity cliff | Pass rate collapses from 91% (<10K LOC) to 15% (>50K LOC) | B3 ⚠️ preprint, venue unconfirmed, chart interpolated | Fully autonomous agents, with no human guidance, fail at **whole-repo modernization** of large codebases *today* | Most relevant evidence against **B-strong**. Measures pass rate, not **cost**. Snapshot, not trend | Valid against B-strong today; not against B-weak |
| 3 Efficiency gap | AI code is 3–14x slower; ~62% of human efficiency | B4 ✅, B5 ⚠️ (Java omitted) | Default AI solutions are inefficient on algorithmic tasks | **Cuts both ways:** efficiency *is* an outcome and can be tested (perf budgets). That argues for *better outcome specs*, not for reading code | GA misframes it. "Outcome-only fails" should read "under-specified outcomes fail" |
| 4 Maintainability erosion | Refactoring −70%, duplication +81% | B6 ✅ with caveats: vendor, correlational, no AI attribution. GitClear itself says the headline is *not* "AI writes bad code" | Industry-wide code-health signals worsened while AI adoption grew | Can't separate "AI" from "unguided AI". Supports *readability gates*, not human line-by-line review | Keep as trend, with caveats |
| 5 Agent code harder to maintain | Agents do worse on agent-written code; 83% of commits to AI files are by humans | B7 ✅, B8 ✅, B9 ✅ (preprint). **C1 and C2 are counter-evidence, cited in GA's own references but never discussed** | Some agents degrade on their own history. Humans currently do most maintenance | B8 measures **current practice** (who commits), not capability. C1: agent code is modified *less*. C2: outcomes vary more *between agents* than between agent and human | Partially valid; omitting C1/C2 is a bias |
| 6 Languages & IR | LLMs are worse at IR; languages persist | B10: link was wrong (maths paper), corrected to arXiv:2407.02524. GA misdescribes the paper. C5 (Jiang et al., 2025) is the direct evidence GA lacks. Points 2–4 are unsourced | Today's general-purpose LLMs reason poorly about IR at instruction level (C5). A specialised IR model still round-trips only 45% of disassembled functions (B10) | None on A/B. **Main rebuttal of claim C** | Keep for C only, rewritten with B10 described correctly + C5. See §2b |
| 7 Compounding loop | Velocity decays 281% → 0%; review time +441% (DORA) | B12 ⚠️ (He et al.: +281% *lines added*, gone after 2 months; warnings +30% and complexity +42% persist). B11 ⚠️ misattributed (Faros AI, not DORA) | Unguided adoption gives a short-lived speed burst and lasting complexity | Supports "harness needed". The loop diagram is a hypothesis, not a measured loop | Keep He et al. correctly worded; label the loop as a hypothesis |
| 8 Quadrant & viability table | Viability by domain | Positions are **invented**. Table maps benchmark numbers onto domains they didn't measure (e.g. "83% human commits" read as "human-dominant viability") | Nothing quantitative | Illustrative only | Drop the chart, or mark it clearly as an opinion sketch. **Candidate replacement:** the marginal cost–benefit rule RM3 (§1b) |
| 9 Earned autonomy path | Phased trust with demotion | Framework, no evidence claimed | Consistent with other earned-autonomy models; demotion when trust is lost is a sound addition | Neutral | Keep as framework |
| 10 Conclusion | "Five independent research programs converge" | Overstated: one result misreported, counter-evidence omitted, no trend data, no cost data, no data on humans' code understanding | See §4 | — | Needs rewording (see §5) |

*Provisional verdicts above are kept for the record. Revised verdicts after step 4 are in §3b.*

---

## 2b. Claim C in detail: GA §6 and points for refinement

**What GA says (§6, point 1):** "LLMs are measurably worse at IR than source code. IR is verbose, graph-structured, and outside the training distribution. Meta's LLM Compiler sidesteps this by generating *compiler pass lists* rather than IR…"

**What the cited source actually says (B10, verified 2026-11-12):** Cummins, C. et al. (2024). *Meta Large Language Model Compiler: Foundation Models of Compiler Optimization*. arXiv:2407.02524. GA linked arXiv:2502.12410, a mathematics paper. The link is now corrected in GA.
- 7B/13B models built on Code Llama, **trained on 546B tokens of LLVM-IR and assembly**.
- Two fine-tuned tasks: code-size flag tuning (77% of an autotuning search's optimisation potential) and **disassembly from x86_64/ARM assembly back to LLVM-IR** (45% round-trip, 14% exact match).
- So the model *does* generate IR. "Sidesteps this by generating pass lists rather than IR" is inaccurate.
- The quoted sentence ("correctness verification plagues…") is not in the abstract. Not located yet.

**Points for refinement**

| # | Point | Type | Proposed action |
|---|---|---|---|
| R1 | **Wrong citation.** ~~2502.12410~~ → 2407.02524 | Fact | Done in GA §6 and reference #13 |
| R2 | **Misdescribed source.** LLM Compiler emits IR. Its weak exact-match score (14%) is the real evidence for GA's point, and GA doesn't use it | Fact | Rewrite with the real figures: "A model trained on 546B tokens of IR round-trips 45% of disassembled functions and reproduces 14% exactly." Find the quote in the full text or drop it |
| R3 | **Wrong population.** GA claims "general-purpose LLM agents are worse at IR". The source is a *specialised* model and doesn't compare against source-code performance | Evidence gap | Add C5 (Jiang et al., 2025): six general-purpose LLMs parse IR syntax but fail at control flow, loops and execution reasoning. This is the direct study GA lacks |
| R4 | **No IR-vs-source comparison.** "Measurably worse" needs the same task measured on both representations. Neither B10 nor C5 does this | Evidence gap | **Found (2026-11-12):** N26 (summarisation: source 0.167 vs. IR 0.052 METEOR, same models) and N27 (84.8% correct at source vs. 41.0% at IR). Cite these in GA §6 |
| R5 | **"Outside the training distribution" is a weak, temporary argument.** Paired source↔IR data is cheap to generate: compile any open-source corpus. LLM Compiler itself proves IR can be learned at scale. This is a snapshot argument (S1) | Trend | Present it as "true for general-purpose models today; can be fixed by specialised training". Don't present it as structural |
| R6 | **The claim conflates "code" with "source language".** Bytecode and IL *are* code, just lower-level. C really says that the human-maintained artifact moves *up* (to spec) and the machine artifact moves *down* (to IR). If the spec must be precise enough to generate IR, the spec becomes the programming language | Framing | Restate C as "where does intent live?" This links C to S6 and to GA's own point 4 (the new programming problem is specifying constraints and verification) |
| R7 | **Platform independence is not a new benefit.** Source + compilers already give it, and so do portable IRs (JVM bytecode, CIL, WebAssembly). Some IRs are *not* portable: LLVM IR embeds target layout/ABI and is not stable across LLVM versions. The only gain from dropping source is skipping compilation, which is cheap | Fact / opinion | Ask: what problem does removing source solve? Without an answer, C-strong has no motive, only feasibility |
| R8 | **Information loss.** IR drops names, comments, module structure and much type intent. Humans and agents use these to reason, debug and review. Decompilers exist because people need source-like views anyway | Opinion (testable) | Link to A: C-strong implies A-strong (nobody reads the artifact). Add the human-factors evidence (S2) |
| R9 | **Verification cuts both ways.** IR has precise semantics, and tools exist for checking IR transformations formally (e.g. translation validation for LLVM, such as Alive2, verified as N9). An IR-native pipeline could be checked *more* rigorously than source. GA ignores this | Steelman | Acknowledge it. The real limit is the spec and the human loop (review, incidents, audit, accountability), not verifiability of IR |
| R10 | **Verbosity / context cost is asserted, not measured.** IR is longer than source, so it costs more tokens and fits worse in context. That would make the complexity cliff (B3) worse | Evidence gap | Quantify (e.g. tokens per function, source vs. IR) or reword as a hypothesis |
| R11 | **GA §6 points 2–4 are unsourced** (typed languages gain ground *because* AI works better with them; adoption tax for new languages; the new programming problem) | Evidence gap | Source each one (e.g. language-trend reports, studies on type systems and LLM error rates) or label as opinion |
| R12 | **Practical relevance.** C affects no practice in §6 directly | Scope | C is settled here like A and B; its practical consequence is indirect (names and types matter to agents, RC2) |

**Provisional verdict on C:** C-strong is not supported today, and GA's rebuttal is directionally right but rests on a misdescribed source. With R2–R3 fixed, the evidence is adequate for "not today", but there is no trend data. C-weak already happens for some generated layers and is a variant of A-weak + B-weak. The source-vs-IR question is secondary to where intent and accountability live.

---

## 3. Steelman: the best case *for* the claims

Completed in step 4 (2026-11-12) with verified sources only. GA never makes this case.

### 3.1 The strongest case for the claims

| # | Argument | Evidence | Supports |
|---|---|---|---|
| ST1 | **Capability grows fast and is accelerating.** The length of task agents complete at 50% success doubled every ~7 months (2019–2025) and every ~89 days since 2024. Claude Opus 4.5 reaches ~5 hours. Any fixed threshold ("50K LOC") is a moving target | N1 | A, B (trend) |
| ST2 | **Hard benchmarks are rising too.** SWE-Bench Pro went from ~23% at release (Sep 2025) to 52–62% on the public set within a year | N6 | A, B (trend) |
| ST3 | **Large AI-driven migrations already work and save time.** Google: ~80% of changes AI-authored in one migration, ~50–89% time saved (engineers' estimates). Airbnb: 3.5k test files in ~6 weeks vs. a 1.5-year estimate | N3, N4 (N5 low weight) | B-weak |
| ST4 | **Humans already don't read most code.** Dependencies, ORMs, garbage collectors, compilers and generated stubs are trusted through tests, types, contracts and reputation. A-weak extends existing practice | RM1 | A-weak, C-weak |
| ST5 | **Where a formal oracle exists, review can move to the checker.** Alive2 found 47 LLVM bugs and already verifies LLM-generated optimisations (LLM-VeriOpt: 90% verifiably correct with Alive2 as reward) | N9 | A-weak, C |
| ST6 | **Natural-language intent can be made reliable.** Letting users approve generated tests adds +46 pp pass@1 within 5 interactions; clarifying questions add ~8 pp | N33, N32 | A-weak |
| ST7 | **Agent code is not universally worse.** Agent-authored lines are modified *less*; some agents beat humans on reverts and security smells; outcomes vary more between agents than between agent and human | C1, C2 | A-weak, B-weak |
| ST8 | **Deep seniority is not required to use agents well.** The success gap from intermediate to expert is "modest", and non-software occupations reach verified agent success almost as often as software users (26% vs. 30%) | N41 | A-weak (team shape RA1) |
| ST9 | **Practice is already shifting.** 90.6% of active pre-2024 repos have agent context files, and 72.1% have AI-authored commits | N35 | A-weak, B-weak (adoption) |
| ST10 | **For C:** IR is learnable with specialised training (B10, N28); IR improves source-code models as a training signal (N29); paired source↔IR data is cheap; IR is formally checkable (N9) | B10, N28, N29, N9 | C (feasibility) |

### 3.2 Where the steelman stops

| # | Limit | Evidence | Weakens |
|---|---|---|---|
| SL1 | **The headline numbers are at 50% reliability.** 80% horizons are much shorter; METR's suite is near saturation with wide CIs. Private code scores lower than public benchmarks | N1, N6 | ST1, ST2 |
| SL2 | **Every migration success had a heavy harness and was bottlenecked by human review.** Unguided agents: ~52% on JDK upgrades, with test deletion; test-only harnesses overstate success | N3, N4, N12, N13 | ST3 as support for B-strong |
| SL3 | **Review is being dropped, not restructured.** PRs merged with no review +31%; median time in review +441%; incidents per PR +243% | N23 | ST4 in practice |
| SL4 | **People who stop reading code lose the ability to judge it.** Learning with AI: comprehension 50% vs. 67%, worst on debugging. Novices develop an "illusion of competence". Programming experience improves security in ways AI doesn't replace | N2, N45, N43 | ST4, ST8 as support for A-strong |
| SL5 | **Generated code is not like an ORM or GC by default.** Those are shared, standard and tested by millions; generated code is new every time, so it has no reputation to trust. It earns comparable trust only to the extent that enforced standards constrain it, and even then must be read when performance, maintainability or security matter (RM1 refinement) | RM1 (reasoning) | ST4 |
| SL6 | **Formal oracles cover narrow domains.** Alive2 works for LLVM transformations; most business software has no equivalent oracle | N9 | ST5 outside compilers |
| SL7 | **Harnesses cost effort and don't help automatically.** Context files give no general gain and add >20% cost; they are edited every 1–3 days | N15, N14 | ST3, ST9 |
| SL8 | **For C:** same task, same models, IR does much worse than source (0.052 vs. 0.167 METEOR; 41% vs. 85% correct). Names and types measurably help LLMs | N26, N27, N30, N31 | ST10 |

**Net:** the steelman establishes that A-weak and B-weak are feasible *with verifiers, harnesses and people who can still read code*, and that capability is rising fast. It does not establish A-strong, B-strong or C-strong, and SL3–SL4 show the practice can undermine its own preconditions.

---

## 3b. Verdicts after step 4

### Claims

| Claim | Today | Trend | Verdict |
|---|---|---|---|
| **A-strong** (nobody needs to read code) | Contradicted on the human side: skill loss when delegating (N2), novice over-confidence (N45), experience not replaced by AI for security (N43) | Capability gains (N1) don't change these human factors | **Not supported.** The strongest evidence against it is about humans, not agents, which GA lacks |
| **A-weak** (review moves from every diff to specs, tests, sampling) | Feasible where verifiers exist (ST5, ST6) and for low-impact change classes. Observed practice is *unstructured* dropping of review (N23) | Rising capability makes it applicable to more classes | **Supported as a design, conditional on:** (1) verifiers for the outcomes that matter, (2) *structured* sampling, not ad-hoc skipping, (3) people who keep code-reading skill. **Qualified (RA7):** fewer people and fewer parts of the process need coding knowledge, but where it is needed the depth does not fall. Coding knowledge concentrates; it is not diluted into a superficial skill |
| **B-strong** (regeneration beats maintenance for typical codebases) | Not supported: unguided agents fail on large repos (B3: 15% >50K LOC) and migrations (N12: ~52%) | Rising (N1, N6), but no cost data either way | **Not supported today; open as a trend.** Re-measure (P10) |
| **B-weak** (regeneration/migration for well-specified, well-tested scopes) | Supported with a harness (N3, N4) | Improving | **Supported, with the harness as a real, ongoing cost** (N14, N15, N37) |
| **C-strong** (source replaced by IR) | Not supported: IR does much worse than source on paired tasks (N26, N27); names and types help (N30, N31) | Specialised models narrow the gap (N28, B10), but there is no motive (R7) | **Not supported, and unlikely for lack of motive** |
| **C-weak** (source as a generated, disposable layer) | Already exists for some layers | — | **Supported but secondary.** Reduces to A-weak + B-weak; where intent lives matters more than source vs. IR |
| **Marginal-returns rule** (RM1–RM4) | Abstractions leak when constraints bind (N46, N47, B4). Returns on tokens saturate, and the verifier is the lever (N49, N51, N48). Returns on review fall with diff size (N50, vendor). No study computes the full trade-off | Token prices fall (cost side) but impact doesn't change | **Supported as a framework.** RM1 holds for shared, standard layers, and for generated code only as far as enforced standards constrain it; RM2 and RM3a supported; RM3b partly (mostly vendor); RM3c is this discussion's own framing, with measurable inputs. **Accepted (step 4 review)** as a framework, flagged as open. Recommended to replace GA §8 |

### GA sections (revises the last column of §2)

| GA § | Revised verdict |
|---|---|
| 1 | Keep B1 with caveats. Replace the B2 sentence with METR's own reading (possible speedup, unreliable signal) |
| 2 | Keep as evidence that **unguided** agents fail on large repos *today*. Add N12, N13 as corroboration. Drop the interpolated chart. Note the trend (N1, N6) |
| 3 | Reframe: "under-specified outcomes fail". Use as evidence for RM2 (constraints bind) and for performance budgets |
| 4 | Keep as trend with caveats. Add balance: DORA 2024 (+3.4% code quality, −7.2% stability, C3) and GitClear's own selection finding (C4) |
| 5 | Keep, and discuss C1/C2 instead of only listing them |
| 6 | Rewrite: B10 described correctly, plus C5, N26, N27 for point 1; N30, N31, N25 for point 2; point 3 labelled opinion; point 4 supported by N32, N33 |
| 7 | Replace "DORA 441%" with Faros AI 2026 (N23), **including +31% PRs merged with no review**. Word He et al. correctly. Label the loop a hypothesis |
| 8 | Replace the quadrant and viability table with the marginal-returns rule (RM3a–c): per change class, compare expected loss removed per unit of cost for tokens vs. developer effort; impact and binding constraints (RM2) push toward developer effort; the verifier is where developer effort pays most (N49). Present RM3c as a framework, not a measured result |
| 9 | Keep. Add: promotion to sampling-based phases requires evidence that sampling is *structured* (SL3) |
| 10 | Reword. Add the human-side evidence (N2, N43, N45), which is GA's biggest missing piece. Drop "five programs converge" |

---

## 4. Cross-cutting problems with GA

| # | Problem | Why it matters |
|---|---|---|
| S1 | **Snapshot vs. trend.** GA answers a forecast with present-day data and never engages with capability trends | It can show "not true today", not "wrong" |
| S2 | **Wrong unit of analysis for claim A.** Claim A is about *humans* needing to understand code. GA's evidence is almost entirely about *agents'* performance | Missing: evidence on what happens when humans stop reading code. **Now available (step 3):** N2 (skill formation), N45 (novice illusion of competence), N43 (experience and security), plus A5 (automation bias) |
| S3 | **No cost data for claim B.** Claim B is economic, and GA gives pass rates only | RepoMod shows failure without guidance. It doesn't show that guided regeneration costs more than maintenance. **Still open:** N48 (agent cost per task) may give the token side only |
| S4 | **"AI" vs. "unguided AI" confounded.** GitClear and He et al. measure adoption without a harness | Their results support "a harness is needed". They don't directly support "code reading is needed" |
| S5 | **Selective evidence.** Lists C1/C2 but doesn't discuss them; inverts B2 | Weakens trust in the whole document |
| S6 | **Outcome-only is a straw man.** Efficiency, maintainability and security can all be expressed as verifiable outcomes | The real debate is *how complete the outcome specification is*, not code vs. outcomes |
| S7 | **Thin, misdescribed evidence for the IR argument.** One source, wrong link, inaccurate summary, no IR-vs-source comparison (§2b) | GA's rebuttal of C is plausible but not demonstrated |

---

## 5. Position

### 5.1 Position (accepted 2026-11-12)

> **Understanding code stops being required for every diff, but stays required for the system, and it concentrates rather than thins out.** Fewer people and fewer parts of the process need coding knowledge; where it is needed, the depth required does not fall (RA7).
>
> **How much developer effort a change gets is a marginal decision, not a fixed rule.** For each class of change, the next unit of effort goes to tokens or to a developer, whichever removes more expected loss (probability of an escaped bug × its impact) per unit of cost (RM3c). Low-impact work with enforced standards can run on outcomes alone. High-impact work, or work under binding constraints (performance, memory, security, maintainability), needs developers who read and, where necessary, write the generated code, just as one reads the SQL an ORM generates when performance matters (RM1, RM2). Returns on extra tokens flatten once the spec and verifier are fixed, so developer effort pays most in the verifier and the spec (RM3a).
>
> **Reviewing less than every diff is safe only under three conditions:** verifiers for the outcomes that matter, including non-functional ones; *structured* sampling, because today review is being dropped rather than restructured (N23); and enforced standards for generated code, which is what earns it ORM-like trust (RM1).
>
> **Regeneration and AI-driven migration already pay off** for well-specified, well-tested scopes, always with a harness, and the harness is an ongoing cost that must be owned (B-weak, RB2). The evidence does not support it for typical large, coupled or performance-critical codebases today.
>
> **Demand for deep skill is likely to rise while its supply shrinks.** If cheaper development raises the volume of software (Jevons), demand for the concentrated coding skill and for harness design rises with it, the latter likely concentrated in platform roles that build standard harnesses (RA8, RB6). Meanwhile, people lose code-reading skill when they delegate to AI rather than use it to inquire (N2), and the junior pipeline that supplies future reviewers is narrowing (N18). Both are risks to manage, not facts to accept.
>
> **The boundary moves.** Agent capability doubles in months (N1), so every threshold in this position is re-measured on a fixed cadence (I12), not argued once.

**Claim verdicts** (from §3b): A-strong not supported. A-weak supported as a design, under the three conditions, with coding knowledge concentrated. B-strong not supported today, open as a trend. B-weak supported with a harness, at an ongoing cost. C-strong not supported and unlikely for lack of motive. C-weak supported but secondary. Marginal-returns rule supported as a framework, flagged as this discussion's own and open.

**On GA:** its conclusion ("concentrated, not eliminated") is directionally right, and this position adopts it with evidence GA lacked. GA overclaims ("the claims are wrong"), misreports or misattributes several sources (B2, B10, B11), omits counter-evidence (C1, C2), and lacks the human-side evidence (N2, N43, N45) that most directly answers claim A.

### 5.2 Original candidate position (kept for the record)

> **Understanding code stops being required per diff, but stays required per system.** As verifiers improve, review effort moves from reading every change to specifying and verifying outcomes, including the non-functional ones (performance, maintainability, security). The ability to read and reason about the code is kept for what verifiers can't cover yet: designing the verifiers, architecture decisions, incident diagnosis and accountability. AI-driven regeneration is already economical for well-specified, well-tested scopes (mechanical migrations, small modules). The evidence does not yet support it for large, coupled or performance-critical systems. That boundary is moving and should be re-measured on a fixed cadence, not argued once.

In short: **A-weak is supported and is what a sandboxed-autonomy level delivers. A-strong is not supported. B-weak is supported with a harness. B-strong is not supported today, and the trend is uncertain. C-strong is not supported today. C-weak already exists for generated layers, and whether the generated layer is source or IR matters less than where intent is specified.** GA's conclusion is directionally right about today, but it overclaims ("the claims are wrong") and its evidence is partly misreported.

---

## 6. Implications for practice

General consequences of the position in §5.1, for any team adopting coding agents. They are stated without reference to a particular organisation or maturity model; adopters map them onto their own process. Numeric thresholds are starting values, not evidence-based.

| # | Implication | Grounded in |
|---|---|---|
| I1 | **Human review stays the default.** A class of change moves to **structured sampling** (randomised, logged review of a share of changes) only when its impact is low, verifiers cover the outcomes that matter, enforced standards pass, and it has a record of zero escaped defects. Never skip review ad hoc. Keep human-reviewed changes small (e.g. ≤ ~400 LOC) | §5.1; N23 (review dropped, +31% unreviewed merges); N50 (review effectiveness falls with size, vendor) |
| I2 | **Rate changes by impact and binding constraints, not size.** Impact = cost of an escaped bug; binding constraints = performance, memory, security, maintainability. Size and coupling are inputs, never a fixed LOC threshold | RM3c, RM2; B3 is a snapshot (N1) |
| I3 | **Make the rating itself earned autonomy.** First the agent proposes a rating and a human confirms every one (default *high* when unsure, so a missing rating means more review, never a block). Then a rubric distilled from those corrections plus deterministic change signals, with spot-checks. Then a risk map of minimum ratings per module or path, enforced by a hook. Finally automatic rating, checked against outcomes; an under-rated change behind a high-impact incident raises that module's minimum and lowers its autonomy. The agent may always raise a rating; lowering needs evidence or a human. The rater is independent of the implementing agent. Promotion needs e.g. ≥ 90% agreement and zero under-ratings | N52 (change-level risk prediction), N54 (LLM reasoning adds little over change metrics), N53; N12 (agents game their own checks), N51 (poor self-assessment) |
| I4 | **Enforced standards are what earn generated code ORM-like trust**, and are a precondition for sampling: conventions, templates, lint and architecture rules, complexity and duplication gates | RM1 refinement; B6, B12 |
| I5 | **Constraint budgets trigger code reading.** Enforce performance, memory and security budgets in CI; a tight or breached budget means a human reads the generated code | RM2; B4, B5, N47 |
| I6 | **Verifier first.** Developer effort on agent work goes first to specs and verifiers (tests, budgets, checkers), not to re-prompting. Generated tests are approved by a human before they gate, and tests are protected from agent edits | RM3a; N49, N33; N12 |
| I7 | **Large migrations only as guided migrations:** implementation-agnostic tests written first, in batches, each through review | B3, N3, N4, N12, N13 |
| I8 | **The harness is a maintained product** (context files, skills, hooks, settings, verifiers) with a named owner, a budget and a refinement cadence. Prefer shared, standard harnesses over per-repo hand-tuning, and measure whether harness changes improve outcomes | RB2, RB5, RB6; N14, N15, N38 |
| I9 | **Refine the harness while prompting:** when the agent's output reveals a missing, stale, conflicting or ineffective instruction, the developer clarifies, fixes, adds or removes it in the same change. This also exercises code-reading | N37, N14 (edits mostly additive), N38, N15 |
| I10 | **Preserve code-reading skill.** Use AI for inquiry, not only delegation, while learning; keep pairing practices; name two risks with owners: skill atrophy and the shrinking junior pipeline | N2, N45, N43, N18; RA7, RA8 |
| I11 | **Measure review health and agent cost:** time in review, share of unreviewed merges, change size, escaped defects; agent/model evaluations per repository including cost per task and its variance | B1; N23, N24; C1, C2; N48, N51 |
| I12 | **Re-measure the boundary** every 6 months, or earlier when: METR's 50% time horizon doubles; SWE-Bench Pro (or its commercial set) rises > 10 pp; internal eval pass rates move > 10 pp; escaped-defect or unreviewed-merge rates move > 25% | N1, N6 |

---

## 7. Sources

All sources, with verification status and key figures, are in [guided_autonomy_references.md](guided_autonomy_references.md). IDs: **B#** sources cited in the original GA; **C#** counter-evidence; **A4-alt, A4-alt2, A4-alt3, A5** human oversight and automation bias; **N#** sources verified during this discussion.

---

## 8. Questions resolved

| # | Question | Outcome |
|---|---|---|
| G1 | Which versions of the claims does this discussion settle? | All of them, strong and weak, for A, B and C (2026-11-12) |
| G2 | What counts as evidence for a forecast? | Present data + trend data + explicit uncertainty (ground rules 3–4) |
| G3 | Keep, amend or replace GA's conclusion? | Amended: position in §5.1, accepted 2026-11-12 |
| G4 | What happens to the GA document itself? | Rewritten as a balanced evidence brief following §3b and §5.1 (v1.0, 2026-11-13) |
| G6 | Re-measurement cadence and triggers | Every 6 months, plus triggers (I12) |

---

## 9. Discussion checklist

- [x] **1. Claim versions (G1).** Confirmed 2026-11-12: the strong versions are the claims as originally made in the debate; the weak versions are the middle ground. Wording in §1 accepted as is.
- [x] **2. Author replies.** Done 2026-11-12 (RA1–RA8, RB1–RB6, RC1–RC3, RM1–RM4); research status filled in (§1b).
- [x] **3. Verify sources.** Done 2026-11-12: N1–N54, C3, C4 verified or corrected ([references](guided_autonomy_references.md)).
- [x] **4. Steelman and verdicts.** Reviewed by the author 2026-11-12 (refinements RA7, RM1, RM3c recorded): steelman and limits in §3; verdicts in §3b.
- [x] **5. Position (G3).** §5.1 accepted by the author 2026-11-12.
- [x] **6. Implications for practice.** §6, accepted 2026-11-12.
- [x] **7. Rewrite GA** as a balanced evidence brief (G4). Done 2026-11-13: v1.0; change history in §11.

---

## 10. Summary of results

**Position.** Understanding code stops being required for every diff but stays required for the system, and it concentrates rather than thins out: fewer people and parts of the process need it, at undiminished depth. How much developer effort a change gets is a marginal decision: the next unit goes to tokens or to a developer, whichever removes more expected loss (P(escaped bug) × impact) per unit of cost; binding constraints (performance, memory, security, maintainability) require reading the generated code, as with ORM-generated SQL, and developer effort pays most in specs and verifiers. Reviewing less than every diff is safe only with verifiers, *structured* sampling and enforced standards. Regeneration and AI migration pay off for well-specified, well-tested scopes with an owned harness, not yet for large, coupled or performance-critical codebases. Demand for deep coding and harness skill likely rises (Jevons) while its pipeline shrinks, a risk to manage. Thresholds are re-measured on a fixed cadence. (Full text: §5.1.)

**Claim verdicts.** A-strong: not supported · A-weak: supported as a design, under three conditions, with coding knowledge concentrated · B-strong: not supported today, open as a trend · B-weak: supported with a harness, at an ongoing cost · C-strong: not supported, unlikely for lack of motive · C-weak: supported but secondary · Marginal-returns rule: supported as a framework, this discussion's own, open.

**GA document.** Rewritten as a balanced evidence brief following §3b and §5.1: v1.0, 2026-11-13.

**Sources.** N1–N54 plus B, C and A-series entries in [guided_autonomy_references.md](guided_autonomy_references.md). Partly second-hand or corrected: N5, N12, N13, N19, N22, N50, N53, N54.

---

## 11. GA version history

The article is kept readable on its own and describes only the current state. Its change history lives here.

### v1.0 (2026-11-13): rewritten as a balanced evidence brief

Replaces the original version (2026-11-07). Each change traces to the verdicts in §3b and the position in §5.1.

| GA § | Change | Traces to |
|---|---|---|
| Thesis, claims | Thesis sharpened (concentration, marginal decision); claims table with strong/weak versions and verdicts added | §1, §3b, §5.1 |
| 1 | The 2026 METR follow-up had been reported as "confirmed 18% slowdown"; it reported a non-significant *speedup*, and METR calls the signal unreliable | B2 |
| 2 | RepoMod-Bench labelled a preprint (the "KDD 2026" venue is unconfirmed); interpolated chart and figures not in the abstract removed; results framed as *unguided* agents; guided successes (Google, Airbnb) and the capability trend (METR, SWE-Bench Pro) added | B3, N1, N3, N4, N6, N12; §3b row 2 |
| 3 | "Outcome-only evaluation fails" reframed as "under-specified outcomes fail"; EffiBench-X's Java finding and leaky abstractions (Spolsky, ORM anti-patterns) added | B5, N46, N47; §2 row 3, RM2 |
| 4 | GitClear caveats, DORA 2024 balance and GitClear's selection finding added; "velocity 281% → 0%" corrected to He et al. (lines added, gone after two months; warnings and complexity persist) | B6, B12, C3, C4 |
| 5 | Counter-evidence that had been listed but not discussed (C1, C2) is now discussed | C1, C2; S5 |
| 6 (new) | Human-side evidence: skill formation, novice over-confidence, expertise, oversight, concentration and labour signals | N2, N18, N41–N45, A4-alt2, A5; S2, RA7, RA8 |
| 7 | "+441% review time (DORA 2025)" was misattributed; the source is Faros AI 2026, which also reports +31% unreviewed merges | B11, N23, N24, N50 |
| 8 | LLM Compiler link corrected (it pointed to an unrelated paper) and its content described correctly (it does generate IR); paired source-vs-IR studies, names and types, ambiguity evidence and the steelman for C added; unsourced points sourced or dropped | B10, C5, N9, N11, N25–N33; §2b R1–R11 |
| 9 | The invented quadrant and viability table replaced by the marginal decision rule | RM1–RM4; §3b row 8 |
| 10 | Incremental risk rating, structured sampling, verifier first, constraint budgets, harness ownership and refinement, skill preservation, measurement and re-measurement added | §6 I1–I12 |
| 11 (new) | "What the evidence does not show": steelman and open gaps | §3 |
| 12 | "Five independent research programs converge" dropped; conclusion restated per §5.1 | §2 row 10, §5.1 |
| Charts | 20 diagrams using only figures verified on primary pages (values recorded in the references file, "Chart values" notes, 2026-11-13) | References file |
