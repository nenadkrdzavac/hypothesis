# Kurepa Hypothesis Development Status

## Summary
- Overall current level: Level 1 reached
- Brief explanation: The repository already contains Lean definitions, small proved lemmas, executable bounded verification, and reproducible check/logging infrastructure, but it does not contain symbolic search, candidate-generation machinery, RL/ML models, learned guidance, invariant-ranking systems, or proof-discovery loops.

## Level-by-level assessment

### Level 1 — Lean formalization and verified computation
Status: Reached

Evidence:
- `leftFactorial` is formally defined in Lean, together with its recursive equation, in [Hypothesis/Kurepa/Definitions.lean](../Hypothesis/Kurepa/Definitions.lean).
- The project includes small proved evaluation lemmas and a recurrence/monotonicity lemma in [Hypothesis/Kurepa/Lemmas.lean](../Hypothesis/Kurepa/Lemmas.lean).
- The main conjecture is formalized as Lean propositions in modular and gcd form in [Hypothesis/Kurepa/Conjecture.lean](../Hypothesis/Kurepa/Conjecture.lean).
- Executable bounded verification is present in [Hypothesis/Kurepa/Examples.lean](../Hypothesis/Kurepa/Examples.lean), including explicit `native_decide` checks for `!n mod n ≠ 0` for `n = 3..10`, gcd checks for `n = 2..7`, and theorem `kurepa_mod_holds_up_to_ten`.
- The Python layer can reproducibly type-check Lean files with `lake env lean` and log the results in JSONL via [python/hypothesis_leandojo/interaction.py](../python/hypothesis_leandojo/interaction.py) and [python/hypothesis_leandojo/logger.py](../python/hypothesis_leandojo/logger.py).

Missing:
- No general proof of Kurepa's hypothesis.
- No broader certified computation framework beyond the bundled finite examples and file-checking workflow.

### Level 2 — Symbolic search
Status: Not reached

Evidence:
- The repository contains no search engine over proof states, recurrences, congruences, or conjecture candidates.
- The only benchmark targets are fixed, hand-written targets in [python/hypothesis_leandojo/examples.py](../python/hypothesis_leandojo/examples.py).
- The Lean examples discuss that bounded computation may guide later proof search, but they do not implement symbolic search; see the explanatory text in [Hypothesis/Kurepa/Examples.lean](../Hypothesis/Kurepa/Examples.lean).

Missing:
- Search-state representation.
- Rule-based or enumerative generation of proof steps, invariants, or equivalent formulations.
- Search loop with branching, scoring, pruning, or replay.

### Level 3 — RL policy/value guidance
Status: Not reached

Evidence:
- There are no RL or ML dependencies in the repository code.
- [python/hypothesis_leandojo/interaction.py](../python/hypothesis_leandojo/interaction.py) only dispatches fixed targets to LeanDojo import checks, `lake env lean`, or a tiny Python fallback; it does not load or train a policy/value model.
- The README explicitly describes the project as Lean formalization plus benchmarking/logging scaffolding, not as a learned search system; see [README.md](../README.md).

Missing:
- Policy model.
- Value model.
- RL training loop, reward signal, replay data, or optimizer/training scripts.
- Any learned guidance of proof or conjecture search.

### Level 4 — Ranking invariants and equivalent formulations
Status: Not reached

Evidence:
- The repository states the modular and gcd formulations of the conjecture in [Hypothesis/Kurepa/Conjecture.lean](../Hypothesis/Kurepa/Conjecture.lean), but they are hand-written proposition definitions rather than generated or ranked candidates.
- [Hypothesis/Kurepa/Examples.lean](../Hypothesis/Kurepa/Examples.lean) mentions recurrence states and invariants only as an explanatory viewpoint for future work.
- No module ranks invariants, compares formulations, scores conjectures, or learns equivalence quality.

Missing:
- Candidate-generation framework for invariants or equivalent statements.
- Ranking/scoring model or heuristic over candidate formulations.
- Evaluation loop that checks and orders such candidates.

### Level 5 — RL-guided discovery of strong partial results
Status: Not reached

Evidence:
- No RL system exists in the repository.
- No component proposes new lemmas, partial theorems, or strengthening/weakening variants automatically.
- Existing partial results are manually authored finite examples and simple lemmas, not machine-discovered outputs.

Missing:
- Automated generation of promising intermediate results.
- Learned prioritization of partial results.
- Verification-and-selection loop for candidate lemmas or partial theorems.

### Level 6 — Full proof or counterexample
Status: Not reached

Evidence:
- [README.md](../README.md) explicitly says the repository does not solve Kurepa's hypothesis.
- [Hypothesis/Kurepa/Conjecture.lean](../Hypothesis/Kurepa/Conjecture.lean) says the conjecture statements are intentionally unproved.
- [Hypothesis/Kurepa/Examples.lean](../Hypothesis/Kurepa/Examples.lean) explicitly says the file is a guided computational demonstration and does not claim a proof.

Missing:
- A formal proof in Lean, or
- A verified counterexample and corresponding formalization.

## Current maturity estimate
- Highest fully reached level: Level 1
- Highest partially reached level: None

## Recommended next milestone
- Implement a genuine Level 2 symbolic-search layer around the existing formalization: define an explicit recurrence/search state, add a small rule-based generator for modular and gcd transformations, and log explored candidates and verified finite consequences through the existing JSONL pipeline.

## Supporting implementation notes
- Lean formalization: present.
- Verified computation: present via `native_decide` examples and theorem-level finite verification.
- Bounded verification: present for fixed finite ranges in `Examples.lean`.
- Certificate checking: partially present only in the narrow sense of Lean file checking and logged benchmark runs; there is no standalone certificate format or checker for discovered artifacts.
- Symbolic search: absent.
- Recurrence-state modeling: only conceptual/expository in comments and demo text, not implemented as a search data structure.
- Invariant framework: absent.
- RL or ML components: absent.
- Policy/value guidance: absent.
- Conjecture/equivalence ranking: absent.
- Partial-result generation: absent beyond manually written lemmas/examples.
