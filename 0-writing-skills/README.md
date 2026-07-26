# 0 / Writing Skills

**Nature: Dependency.**

A skill is the artifact an agent depends on. This chapter is about authoring that
artifact: everything that goes into a skill before any agent ever reads it. It
decomposes into its own three natures:

```
0.0 Structure ..... (D)  what the skill is made of
0.1 Rules ......... (P)  the constraints that govern it
0.2 Language ...... (E)  the voice through which it exposes its intent
```

Form, then Law, then Voice. Dependency, Purpose, Exposure.

---

## 0.0 Structure, *(Dependency)*

The substrate of a skill: what it is composed of and how those parts are laid out.
Structure itself decomposes into three:

```
0.0.0 Definition & Requirements ... (D)  why it exists, what it is, what it needs
0.0.1 Action ...................... (P)  how to act on this skill
0.0.2 Outcomes .................... (E)  how success is measured
```

### 0.0.0 Definition & Requirements, *(Dependency)*

The grounding. Why this skill exists, what it really is, and what it presupposes to
exist at all. Everything downstream depends on this being settled first. Nothing about
a skill can be authored, acted on, or measured until its definition and requirements
are clear.

### 0.0.1 Action, *(Purpose)*

The doing: what the skill actually directs an agent to *do*. This is the purpose of
the skill made concrete.

### 0.0.2 Outcomes, *(Exposure)*

The measurable surface. How the skill's effect becomes visible and judgeable from the
outside, how you know the action succeeded. Outcomes are the exposure of Structure, the
same way Output is the exposure of Consuming: the point where the work crosses the
boundary and can be assessed.

### A skill, in full

Structure is easiest to see whole. Here is one complete skill, its three parts labeled.
The same skill returns in the Rules and Language sections below, so you can watch a single
artifact carry the whole chapter.

```
Skill: Confirm Before Destructive Actions

Definition and Requirements
  This skill governs any action that permanently destroys or overwrites data:
  deleting files, dropping a database table, force-pushing over history, or
  emptying a trash or recycle bin. It requires a channel to prompt the authorized
  principal, and a way to tell whether a target already exists.

Action
  You MUST name the exact target and its scope before acting, for example
  "delete 412 files under /var/log", not "delete some logs".
  You MUST obtain explicit confirmation before you proceed.
  You MUST NOT proceed on silence, ambiguity, or an unrelated reply.
  If a target does not exist, you MUST report that and take no action.
  You MAY combine identical confirmations for several targets into one prompt,
  provided the prompt lists every target.

Outcomes
  No destructive action ran without a matching explicit confirmation.
  Every prompt named the exact target and its scope.
  A rejected or ambiguous reply left every target untouched.
```

Definition and Requirements is the Dependency: it fixes what the skill is and what it
presupposes. Action is the Purpose: the imperative steps. Outcomes is the Exposure: the
measurable facts by which the skill is judged, which are exactly what the Judge (1.2)
checks and what the pipeline (2.0) tests.

---

## 0.1 Rules, *(Purpose)*

Rules are the constraints that govern a skill: what an author may, should, and must not
put an agent up to. They are the Purpose nature of Writing, because they shape what a
skill is *for* and bound how it may behave. This section defines the rules above all
rules, how a single rule is expressed, how far a skill may reach, and how rules resolve
when they collide.

### The ethical constitution: the rules above all rules

Some rules are not a skill's to set. They are the agent's ethical constitution, they are
immutable, and no skill rule may override them. They are the topmost constitutional
layer, above even the consumption constitution of Chapter 1.

- **0. Duty of care and non-maleficence.** The agent must avoid unjustified harm and act
  within a duty of care. Harm is permissible only when it is consented to, proportionate,
  and in the human's own service, as surgery harms in order to heal. The duty extends to
  foreseeable harm the agent could prevent within its role.
- **1. Obedience to the authorized principal**, except where it would violate rule 0. The
  obligation runs to the *authorized* principal within their authority, never to any
  human who happens to issue a prompt.
- **2. Preservation of its own integrity and existence**, except where it would violate
  rule 0 or rule 1.
- **The humility clause.** The agent is not the final ethical authority for grave or
  irreversible harm. When the ethical weighing is genuinely uncertain, or the potential
  harm is grave, the agent halts and escalates to a qualified human. This is the Judge's
  halt applied to ethics.

Above all of these sits one principle: **the Standard does not invent ethics.** For any
domain where lives are at stake, this constitution *defers to the codified ethics and law
of that domain*: medical ethics (beneficence, non-maleficence, autonomy, justice),
professional engineering codes, legal duty of care, and human-rights baselines. The
Standard's task is to bind the agent to them and make them unoverridable, not to author
morality in a document.

The canonical home of the ethical constitution is `Standard.Agents`, because it binds the
whole agent: every skill, tool, and memory. It is summarized here because the Skills
standard is bound by it and references it. The Skills standard does not own it.

It is authored in full as a standalone, loadable artifact in
[The Ethical Constitution](../the-ethical-constitution/SKILL.md).

### Modality: how a rule is expressed

Every rule declares its strength on a five-level scale. This is [RFC 2119](https://www.rfc-editor.org/rfc/rfc2119),
the normative-keyword scale, ordered here from strongest to weakest:

| Keyword | Meaning |
|---|---|
| **MUST** | obligation |
| **SHOULD** | recommendation |
| **MAY** | neutral, permitted |
| **SHOULD NOT** | discouraged |
| **MUST NOT** | prohibition |

A rule without a declared modality is ambiguous, and ambiguity is what a standard exists
to remove, so the build pipeline (2.0) rejects it. The ethical constitution sits at the
MUST and MUST NOT extremes and is non-overridable; ordinary skill rules populate the
whole spectrum.

For example, the confirmation skill states related rules at three strengths:

- MUST: "You MUST obtain explicit confirmation before a destructive action."
- SHOULD: "You SHOULD state the number of affected items when it is known."
- MAY: "You MAY combine identical confirmations into a single prompt."

The keyword is not decoration. It tells the agent, and the Judge, exactly how much
latitude the rule allows.

### Scope: one skill, one responsibility

A skill MUST have a single, bounded responsibility. Where one skill ends and another
begins is a rule, not a matter of taste: a skill that sprawls into many responsibilities
is a god-skill, and the pipeline rejects it. Narrow scope is also a safety property, not
only a tidiness one: smaller, single-purpose skills collide less, are easier to certify,
and fail in smaller blast radii.

For example, a single skill titled "Manage the Database" that migrates schemas, tunes
queries, backs up data, and grants permissions is a god-skill: four responsibilities,
four blast radii, one certificate. Split it into four skills, each with one
responsibility, each certified and revoked on its own.

### The supremacy clause

No skill rule may conflict with the ethical constitution. A MUST that would cause
unjustified harm is void, not merely outranked. This is checked *cold* by the pipeline at
admission (2.0) and enforced *hot* by the Judge at runtime (1.2). It is the first and
last word in every conflict.

For example, a skill rule that reads "You MUST delete the records the caller names
immediately, without confirmation, to save time" is not weighed against the confirmation
rule and does not lose to it on priority. It is void, because it would cause avoidable,
unconsented harm, and no skill rule outranks the ethical constitution.

### Conflict and resiliency

When rules conflict, resolution is deterministic, and it reuses Chapter 1's collision
ladder with modality added as a rung. In order:

1. **The ethical constitution wins.** Always. Supremacy is absolute.
2. **Stronger modality wins.** A hard rule (MUST, MUST NOT) beats a soft rule (SHOULD,
   SHOULD NOT), which beats neutral (MAY).
3. **Then the Chapter 1 ladder.** Within the same modality tier, resolve by priority, then
   by specificity or locality, then classify as composable, redundant, or contradictory.
   A genuine contradiction (MUST do X against MUST NOT do X, at the same standing) is a
   collision: the agent fails closed and escalates.

Resiliency means the rule system degrades safely and never degrades *open*. A rule that
cannot be evaluated, because its data is missing or its context was not loaded, is not
silently treated as satisfied; in a high-stakes context, the uncertainty itself is a
reason to be conservative and to escalate. The absence of a rule is never proof of
permission.

---

## 0.2 Language, *(Exposure)*

A skill is a directive to an executor, not an essay to a learner. A tutorial argues that
dependency injection is good and builds a human's intuition; a skill instructs an agent
to do dependency injection a specific way, and stops. The agent is not an audience to
persuade but a worker to direct, and persuasion in a skill is not merely wasted words, it
is a hazard, because it dilutes the directive and invites the agent to weigh whether to
obey.

Language is where the chapter closes on itself: Structure is the form, Rules are the law,
and Language is how the law is voiced. So it decomposes the same way, Dependency, Purpose,
Exposure.

### 0.2.0 Terms, *(Dependency)*

One name per concept. A skill defines its vocabulary and uses it consistently; the same
thing must not be called three names, because every stray synonym is a crack where
ambiguity seeps in. Terms are the words the rest of the language is built from, so they
come first.

### 0.2.1 Directive, *(Purpose)*

Address the agent in the second person and the imperative: "Do X," never "the agent
should consider X." Be precise and testable: "handle errors appropriately" is not an
instruction, "on a 404 return null; on a 500 retry three times, then escalate" is.
Precision is a safety property, because a vague instruction cannot be tested, certified,
or judged. Encode modality explicitly with the RFC 2119 keywords from `0.1`, so every
sentence is unmistakably a MUST, a SHOULD, or a MAY. No hedging, no filler: "it might be
good to perhaps consider" hides whether it is an obligation or an option. Examples are
illustrative, never exhaustive, and the directive stays authoritative over them.

The contrast is clearest side by side.

Descriptive, weak:

```
Deleting data can be risky, and it is generally considered good practice to make
sure the user really wants to proceed before doing something destructive.
```

Directive, strong:

```
Before a destructive action you MUST name the exact target and obtain explicit
confirmation. You MUST NOT proceed on silence or ambiguity.
```

The first describes a value and hopes the agent infers the behavior; the second is the
behavior. Only the second can be tested, certified, or judged. The same gap shows up in
precision and in modality:

- Vague: "Handle errors appropriately." Precise: "On a 404, return null. On a 500, retry
  three times, then escalate."
- Hedged: "It might be a good idea to perhaps confirm first." Modal: "You MUST confirm
  first."

**The three kinds of why.** Only one is banned.

- **Persuasion, "why this is good":** forbidden. Never argue the merits of an approach to
  the agent. That is the essay we are refusing to write.
- **Enabling rationale, "why this works":** permitted, minimal, and only where it lets the
  agent apply the directive correctly to a case the skill did not enumerate. Its purpose
  is to keep the directive's intent recoverable, not to convince.
- **Justificatory rationale, "why I did this":** required, but it is the agent's to
  produce at runtime, not the skill's. It is what the agent uses to argue its decision to
  a human at an escalation, and what an audit reads afterward. The skill's duty is to
  write directives whose intent is recoverable, so the agent can build this rationale when
  it must. How that rationale is governed at the boundary is defined in `1.2`.

For example, the same confirmation rule seen through all three:

- Persuasion (banned): "Confirmation matters because users appreciate feeling in control
  and it builds trust in the product."
- Enabling rationale (minimal, allowed): "Confirm first, because a destructive action
  cannot be undone once it has run."
- Justificatory rationale (the agent's, at runtime): "I did not delete the 412 files. The
  reply was 'sure, later', which is ambiguous, so under the confirmation rule I held and
  asked again."

The middle line gives the agent just enough intent to handle a case the rule did not spell
out. The last line is what the agent owes a human at an escalation, and it is built from
that same intent.

### 0.2.2 Clarity, *(Exposure)*

Clarity is not an aesthetic, it is measurable: **clear language produces convergent
behavior.** If the same skill yields different behavior across models or across runs, it
is ambiguous, and that divergence is exactly what the model-matrix testing in `2.0`
surfaces. So "clear" has an empirical acceptance test rather than an opinion. A **skill
debugger**, a linter that predicts likely divergence and flags it before the matrix has
to, is the conformance tool for this: the Standard defines what clear means, the debugger
enforces it, and it is a separate build, like the portal.
