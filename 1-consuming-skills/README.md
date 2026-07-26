# 1 / Consuming Skills

**Nature: Purpose.**

This is why skills exist at all: for an agent to read one and act on it. This chapter
is about how an agent consumes a skill: pulling it in, applying it, and surfacing the
result. It decomposes into its own three natures:

```
1.0 Priority .......... (D)  intake: what to load, and how it ranks
1.1 Implementation .... (P)  the doing
1.2 Output ............ (E)  what the agent surfaces back
```

Resolve what to load and rank it, then do it, then surface the result. Dependency,
Purpose, Exposure.

---

## The decision realm: Gate, Brain, Judge

Consuming a skill is a decision, and every decision has three aspects:

- **Gate** *(Dependency)*: assembles what the decision depends on. It filters the pool
  of available skills down to the relevant, trusted, and affordable few, and it guards
  the context window from being flooded.
- **Brain** *(Purpose)*: the reasoning core. It reads the admitted skills and decides.
- **Judge** *(Exposure)*: evaluates the decision against the skill's outcome before the
  result is exposed.

These are not a second structure competing with Priority, Implementation, and Output.
They are the same three, viewed as a decision. The lifecycle lens says what happens, in
order; the decision lens says what machinery does it:

| Lifecycle | Decision aspect | Nature |
|---|---|---|
| 1.0 Priority | Gate | Dependency |
| 1.1 Implementation | Brain | Purpose |
| 1.2 Output | Judge | Exposure |

The decision lens earns its place by naming the Judge. "Output" says emit the result;
the Judge says evaluate it first, then emit. Exposure is judge-then-emit, not emit.

Gate, Brain, and Judge are not specific to skills: the same engine governs how an agent
admits memories and tools. It is a general agent decision primitive, and its shared
definition belongs at the `Standard.Agents` level. This chapter describes only how
consuming a skill uses it.

---

## 1.0 Priority, *(Dependency)*: the Gate

Priority is the intake layer, the precondition of consumption, and its engine is the
Gate. Before an agent acts, the Gate assembles what the Brain will depend on: it pulls
candidate skills, loads whatever a skill *references* (references are intake, a
dependency, not an exposure: the agent reaches inward for them), and resolves which
skills apply and how they rank.

The Gate has three duties, and the third is the one that keeps the agent alive.

### Relevance

Rank every candidate skill by how well it fits the prompt. Rank *generously*: do not
pre-exclude. A skill the Gate silently drops is one the Brain can never compensate for,
because it never sees what was withheld. A marginally relevant skill that slips through
is recoverable: the Brain can ignore it.

### Trust

The Gate is also a security boundary. A hostile or untrusted skill must not reach the
Brain. Relevance and trust pull opposite ways when the Gate is unsure, so the rule is:
pass what is relevant *and* trusted; when torn, err toward inclusion on relevance and
toward exclusion on trust.

### Context economy

The context window is the one truly scarce, shared resource, and the Gate is its
guardian. The Gate never makes a naive include-or-exclude call per skill. It ranks,
then admits a subset under a fixed token budget, cutting from the margin first. A blown
window degrades all of the Brain's reasoning at once, which is far worse than dropping a
single marginal skill. So the budget is a hard constraint that outranks relevance:
relevance ranks, the budget cuts.

Two mechanisms let the Gate stay lean without hiding anything:

- **Two-tier admission.** Every skill first contributes only its lightweight descriptor
  (name, description, trigger): tiny cost, near-total recall. Only when the Brain commits
  to a skill does its full body load. The agent never pays the full cost of a skill it
  does not use.
- **Re-gating.** The Gate is a standing service, not a one-shot upfront pass. If the
  Brain finds mid-task that it needs a skill trimmed from the margin, it re-queries the
  Gate. This is what lets the Gate stay stingy by default and still never lose a needed
  capability.

The principle underneath is ordinary dependency discipline stated for context: **a Gate
delivers the minimal sufficient dependency set, not the maximum available.**
Over-provisioning context is the same smell as over-injecting dependencies into a class.
Everything admitted must earn its tokens.

### Collision handling

Ranking has a failure mode: two skills that *collide*, directing the same thing in
opposite ways at the same standing. The Gate resolves conflict through a deterministic
ladder, and escalation is the **last** rung, not the first move:

| Situation | Resolution |
|---|---|
| Different priority | Higher priority wins. Deterministic. |
| Same priority, different level | The more specific or more local level wins. Deterministic. |
| Same priority, same level, **composable** | Do both. Not a collision. |
| Same priority, same level, **redundant** (same ask, same way) | Dedupe or soft-note. Not a collision. |
| Same priority, same level, **contradictory** (same ask, opposite ways) | **Genuine tie. Escalate.** |

The Gate must first *classify*: composable, redundant, or contradictory. Only a true
contradiction is a collision. On a genuine collision the agent must **fail closed**:

1. **Halt only the conflicted action**, not the whole task.
2. **Name the collision precisely.** Never a vague "I'm confused," and never a silent
   guess (silently choosing one of two contradictory directives is the worst outcome:
   non-deterministic, unauditable, possibly the exact opposite of intent):

   > "Skill **A** says *do X*; Skill **B** says *do not-X*. Both at priority P, level L.
   > I can't resolve this deterministically. Which should win?"

3. **Offer the tiebreak** so the human answers with a single choice.

A live collision is also an **Output** (see 1.2) event: it feeds back to the Managing
layer (Chapter 2), where the pool is checked *cold*, across all skills. The agent
detects collisions *hot*, in a real runtime context the static check could not predict.
The same concern refracted through two natures: Purpose teaching Exposure.

---

## 1.1 Implementation, *(Purpose)*: the Brain

> Status: to be drilled.

The act itself: the Brain reasoning over the admitted skills and applying them, once
the Gate has resolved intake and priority.

---

## 1.2 Output, *(Exposure)*: the Judge

> Status: to be drilled.

What the agent surfaces after applying the skill: the response, the action taken, the
result made visible. This is the true exposer of consumption, the thing crossing the
boundary back out. Its guardian is the Judge, which evaluates the result against the
skill's outcome (see `0.0.2`) before it is emitted, and which enforces the collision
escalation at runtime. Exposure is judge-then-emit. This is also the channel through
which runtime events, such as collisions, are reported to the Managing layer.
