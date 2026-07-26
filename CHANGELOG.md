# Changelog

The Agent Skills Standard is versioned `MAJOR.MEDIUM.MINOR`. Every iteration bumps the
version, and the bump follows the commit that carries it:

- **DOCUMENTATION**: brand new documentation. Establishes a baseline or adds a new document.
- **MINOR DOCUMENTATION**: a small change. Bumps MINOR.
- **MEDIUM DOCUMENTATION**: a substantive change. Bumps MEDIUM, resets MINOR.
- **MAJOR DOCUMENTATION**: a structural or breaking change. Bumps MAJOR, resets MEDIUM and MINOR.

A version below `1.0.0` means the Standard is still under active authorship and not yet
ratified. `1.0.0` is the first complete, ratified Standard. While the version is below
`1.0.0` the leading `0` is frozen until ratification: a MAJOR or MEDIUM change advances
the middle number and a MINOR change advances the last. On ratification the version
becomes `1.0.0`, after which the three positions map to MAJOR, MEDIUM, and MINOR distinctly.

## 0.5.0 - 2026-07-25

DOCUMENTATION. Added the Introduction chapter (front matter, outside the 0/1/2 spine).

- Natural language as the new programming language of Software Engineering 2.0, and what a skill is to an agent.
- Why skills must be standardized, and the danger of leaving them to raw model interpretation in high-stakes settings.
- The Standard, its lineage from The Standard for Software Engineering, and why a new one is needed for agents, skills, and memories. (History section to be personalized by the author.)
- Why standardizing AI matters: a skill is a blessing or a curse depending on how, where, and by whom it is used.
- Linked at the top of the Table of Contents.

## 0.4.0 - 2026-07-25

MEDIUM DOCUMENTATION. Drilled 0.2 Language and completed the first full draft of all nine nodes.

- **0.2 Language** as directive, not description: a skill is a directive to an executor, not an essay to a learner. Decomposed into Terms (Dependency: one name per concept), Directive (Purpose: imperative, second-person, precise, testable, RFC 2119 modality, no hedging), and Clarity (Exposure: measured by convergent behavior across models and runs, with the skill debugger as its linter).
- **The three kinds of why:** persuasion is banned, enabling rationale is minimal and permitted, justificatory rationale is required but produced by the agent at runtime.
- Enriched **1.2 (the Judge)** with the rationale a halt must carry: faithful and grounded, balanced, and non-manipulative. The persuasion ban survives at the human boundary: a skill may not argue the agent, and the agent may not argue the human.
- This completes a first full draft of the Standard. It remains unratified; 1.0.0 is reserved for ratification.

## 0.3.0 - 2026-07-25

MEDIUM DOCUMENTATION. Drilled 0.1 Rules.

- **The ethical constitution** as the topmost, immutable layer, above the consumption constitution: duty of care and non-maleficence (harm only when consented, proportionate, in the human's service), obedience to the authorized principal, self-preservation, and a humility clause (grave or uncertain ethics halts to a qualified human). The Standard does not invent ethics; it defers to codified domain ethics and law. Canonical home flagged as Standard.Agents.
- **Modality** on the RFC 2119 five-level scale (MUST, SHOULD, MAY, SHOULD NOT, MUST NOT); an unlabeled rule is rejected by the pipeline.
- **Scope:** one skill, one responsibility; god-skills are rejected; narrow scope framed as a safety property.
- **The supremacy clause:** no skill rule may conflict with the ethical constitution; checked cold at admission and hot by the Judge.
- **Conflict and resiliency:** ethics wins, then stronger modality, then the Chapter 1 collision ladder; the system degrades closed, never open.

## 0.2.1 - 2026-07-25

MINOR DOCUMENTATION. Added a nested, decimal-numbered Table of Contents to the root
README, linking every chapter and section, in the style of The Standard. Replaced the
flat status list with the Table of Contents plus a one-line status.

## 0.2.0 - 2026-07-25

MAJOR DOCUMENTATION. Completed Chapter 2 and reshaped its subsections.

- Reshaped 2 / Managing from the Storage / Governance / Distribution sketch to
  **Publishing / Governance / Registry** (Storage is now an implementation detail beneath the Standard).
- **2.0 Publishing:** the build pipeline. Structure validation, language checks, dependency resolution, testing across a model matrix, semantic security scanning, collision scanning, human review, then signed and versioned publish. A green build is necessary but never sufficient.
- **2.1 Governance:** skill versioning and breaking changes, deprecation with migration, continuous security and collision scanning, and the review lifecycle. The constitution is the extreme case.
- **2.2 Registry:** catalog, discovery, distribution, and the model-compatibility contract. Framed the two lines of defense (cold pipeline, hot runtime) and the severity ladder the Gate applies (pass / warning / error / critical fail), keyed on certification status crossed with stakes: incompatible is a hard block at any stakes, unknown fails closed.

## 0.1.0 - 2026-07-25

Formal versioning begins here. Baseline snapshot of the Standard to date.

- Tri-Nature spine established: Writing (Dependency), Consuming (Purpose), Managing (Exposure).
- **0 / Writing**: Structure drilled (Definition & Requirements, Action, Outcomes); Rules and Language stubbed.
- **1 / Consuming**: complete.
  - Foundational principle: consumption is a skill, not an interpretation. The SKILL for consuming skills is constitutional, never filtered by the Gate and never questioned by the Judge, immutable, signed, trusted-root, never self-amending.
  - The decision realm (Gate, Brain, Judge) inside a closed loop over Data, Decision, Direction.
  - 1.0 the Gate: relevance, trust, context economy, collision handling.
  - 1.1 the Brain: executes the consumption skill, free in the domain, bound in the protocol.
  - 1.2 the Judge: judges the outcome as a whole, before, during, and after the action; permit, reiterate, or halt; independent and adversarial; loop guardrails.
- **2 / Managing**: Storage, Governance, Distribution sketched.
