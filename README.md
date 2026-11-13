# ai-discussions

Open, evidence-based discussions of claims about AI, especially about how AI changes software engineering. Each discussion takes a document or a claim, tests it against verified evidence, and states a position that can be revised as the evidence changes.

## Why

Debates about AI tend to be settled by confident forecasts and figures that nobody checks. This repository tries to do the opposite:

- every figure is traced to its primary source, with its verification status recorded;
- both sides get their strongest case;
- what the evidence shows today is kept apart from trends and opinion;
- conclusions are versioned and re-measured, not argued once.

## Methodology

Every discussion follows the same steps. A checklist at the end of each discussion file records progress.

### Ground rules

1. **Aim for a defensible position**, not confirmation of the author's view or the document's. Steelman both sides.
2. **A figure counts only if it has been verified** against its primary source and is listed in the discussion's references file.
3. **Separate three things:** what the evidence shows **today**, what the **trend** suggests, and what is **opinion**.
4. **Forecasts can't be refuted by snapshots.** A claim about "a few years from now" is judged as *supported*, *not supported yet*, or *contradicted by the trend*.

### Steps

1. **State the claims.** Write each claim in two versions:
   - a **strong** version, as originally made;
   - a **weak** version, the middle ground.

   Both are discussed. Rebutting only the strong version is easy and proves little.
2. **Audit the document section by section.** For each section, record what the document claims, the status of its evidence, and what that evidence actually supports, which is often narrower than the conclusion drawn from it.
3. **Verify every source.** Each citation gets a stable ID and a status:
   - ✅ verified;
   - ⚠️ real, but needs correction or is partly second-hand;
   - ❌ not found or wrong reference;
   - ➕ added during verification.

   Vendor reports, preprints and correlational data are labelled as such. Counter-evidence is actively looked for and listed alongside supporting evidence.
4. **Record replies as testable sub-claims.** Each reply is split into sub-claims with IDs. For each one, the discussion records:
   - what it relies on (a study, experience, an analogy or reasoning);
   - its type (today, trend, opinion or hypothesis);
   - its research status.

   Refinements are added with dates, not overwritten.
5. **Build the steelman and find its limits.** Write the best case *for* the claims using verified sources only, then list where that case stops, also with sources.
6. **Give verdicts.** Each claim version gets a verdict that separates today from the trend. Each section of the document gets a revised verdict: keep, correct, reframe or drop.
7. **State a position**, which the owner accepts, amends or rejects. Earlier candidate positions stay in the file for the record.
8. **Derive implications for practice.** Keep them general enough for any team to map onto its own process. Numeric thresholds are flagged as starting values unless evidence supports them.
9. **Rewrite the document** as a balanced evidence brief that follows the verdicts and the position.
10. **Re-measure.** Each discussion sets a review cadence and the triggers for an earlier review. Changes are dated in the changelog.

## Repository structure *(proposed)*

```
README.md
CHANGELOG.md
discussions/
  guided-autonomy/
    discussion.md     # the working discussion: claims, replies, audit, verdicts, position
    references.md     # source catalogue with stable IDs and verification status
    article.md        # the document under discussion, rewritten as a balanced brief
Versions/
  guided-autonomy/
    v1.0_2026-11.md   # periodic snapshots of the article, for readers who want the latest status
```

- **`discussions/`** holds the working material and changes often.
- **`Versions/`** holds periodic snapshots of each discussed article. If you just want the current state of a topic, read the latest file in its `Versions/` folder. Each snapshot states its date and the discussion version it reflects.
- **Tags** (e.g. `guided-autonomy-v1.0`) mark the discussion state behind each published version. Documents that cite a discussion should cite a tag, not the moving branch.

## Discussions

| Topic | Status | Latest version |
|---|---|---|
| Is *AI Coding: The Case for Guided Autonomy* right? | Initial Version | *pending* |

## Contributing

- **New evidence or a correction:** open an issue with the source (full reference and link), the claim it bears on, and whether you read it on the primary page.
- **A new reply or counter-argument:** open an issue or a pull request against the discussion file. It will be split into testable sub-claims and researched like any other.
- **A new topic:** open an issue proposing the document or claim and its strong and weak versions.

Research for these discussions uses AI assistance. The verification status on each source records what was read on the primary page and what is second-hand.

## Owner

Andrés Gómez
