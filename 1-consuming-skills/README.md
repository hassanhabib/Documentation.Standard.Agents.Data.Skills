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
- **Judge** *(Exposure)*: evaluates the outcome as a whole, before, during, and after
  the action, and permits, reiterates, or halts.

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

### The decision realm sits inside a closed loop

The decision realm is not a pipeline with an end. It is one turn of a cycle. An agent
has three macro-realms, and they too are a Dependency, Purpose, Exposure:

- **Data** *(Dependency)*: what everything is built on. Skills, prompt, memories, and
  the results of prior actions. The Gate guards this realm.
- **Decision** *(Purpose)*: the reasoning. Gate, Brain, and Judge live here.
- **Direction** *(Exposure)*: contact with the world. Taking the action.

Exposure feeds back into Dependency, and that feedback is what makes it a loop instead
of a line: the action produces new data, the data re-enters the Data realm, and the
next decision is asked for.

```
   ,--> Data (Gate, D) --> Decision (Brain, P) --> potential Direction (E)
   |            \________________ Judge ________________/
   |                       permit | reiterate | halt
   |                              |
   |                       Direction executes
   |                              |
   `----- new data (the result) --'   the Judge judges this too (after)
```

An agent that decides, acts, and walks away is *open-loop*, and open-loop is the
dangerous kind: fire the instruction, never check the result. Closed-loop is cut, watch
the bleeding, adjust. The after-judgment is the feedback that closes the loop; without
it the agent is blind the instant it acts.

Data, Decision, and Direction, and the loop that binds them, are `Standard.Agents`-level
concepts. The Skills standard references them; it does not own them.

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
Brain, and this is where policies, rules, and conditions are enforced: do no harm and so
on. Relevance and trust pull opposite ways when the Gate is unsure, so the rule is: pass
what is relevant *and* trusted; when torn, err toward inclusion on relevance and toward
exclusion on trust.

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
opposite ways at the same standing. The Gate flags collisions between relevant skills in
real time and resolves conflict through a deterministic ladder, where escalation is the
**last** rung, not the first move:

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

A live collision is also fed back to the Managing layer (Chapter 2), where the pool is
checked *cold*, across all skills. The agent detects collisions *hot*, in a real runtime
context the static check could not predict. The same concern refracted through two
natures: Purpose teaching Exposure.

---

## 1.1 Implementation, *(Purpose)*: the Brain

> Status: to be drilled.

The act itself: the Brain reasoning over the admitted skills and producing a decision,
along with the *potential direction* it intends, once the Gate has resolved intake and
priority. The Brain proposes; it does not commit. Nothing it produces becomes action
until the Judge has judged it.

---

## 1.2 Output, *(Exposure)*: the Judge

What the agent surfaces after applying the skill is not just a result; it is an outcome
that has passed judgment. The Judge is the exposer of consumption and the commit gate
between deciding and acting: nothing becomes an executed direction until the Judge
permits it.

### The Judge judges the whole

The Judge does not check the decision in isolation. It judges the **outcome as a whole**,
three layers at once:

- **Data**: skills, prompt, memories. The grounds. What was known and what was asked.
- **Decision**: what the Brain concluded.
- **Potential direction**: the concrete action the decision intends, not yet executed.

The reason it must judge the whole, and not each part in turn, is that every part can be
locally valid and the whole still lethal. The data is right, the correct patient and the
correct scan. The decision is sound given the data, that vessel must be clamped. And the
potential direction still kills someone if *here* is two millimeters off, because the
action did not faithfully carry the decision into the body. **Correctness of every part
is not coherence of the whole.** Emergent failure lives in the seams between valid parts,
and only a faculty that sees all three at once can see the seam.

That is why it must be the Judge specifically: it is the only faculty with a panoramic
view. The Gate sees inputs. The Brain sees inputs and produces a decision. The Judge sees
inputs, decision, and intended action together.

### The verdict space is three, not two

- **Permit**: the whole coheres; the potential direction may execute.
- **Reiterate**: send it back, and name where it broke. This is an attribution, not a
  blind retry. A data failure re-gates (see 1.0). A decision failure returns to the
  Brain. A direction failure means a sound decision was not faithfully carried into
  action.
- **Halt**: refuse, and surface to a human. Sometimes the correct output is no action
  and an escalation, exactly like the collision tie. A Judge that can only permit or loop
  will eventually loop itself into acting.

### The Judge is independent and adversarial

If the faculty that decided also judges, it rubber-stamps its own reasoning. The Judge
reasons from the outcome backward and tries to *refute* the direction, not confirm it. In
a critical system its job is to hunt for the reason *not* to act; only when it cannot
find one does it permit. The burden of proof is on the action, and rigor scales with the
potential direction: a low-stakes action gets a light pass; an irreversible or harmful
one gets maximum scrutiny, and above a harm threshold the permit is not the Judge's to
give alone, it requires a human.

### The Judge judges before, during, and after

Because the decision realm sits inside a closed loop, the Judge is not a checkpoint at a
single instant. It runs across the whole action, in three modes:

- **Before** (the potential direction): permit, reiterate, or halt. Should we act at all?
- **During** (the action unfolding): continue or abort. Is it going as intended? This
  requires the action to be abortable; for a live procedure it is a genuine kill-switch.
- **After** (the produced data): confirmed or diverged. Did it achieve the outcome? A
  divergence is not garbage to discard; it is the signal that drives the next cycle, or
  trips a halt.

The Judge is the only faculty that persists across the action, which is why it can hold
the agent accountable for what the action *did*, not only what it *intended*.

### Guardrails the loop cannot ship without

1. **A closed loop can be unstable.** The after-judge finds divergence, re-decides, acts,
   diverges again, without end. The loop needs convergence criteria and an iteration
   budget, and non-convergence is itself a halt-to-human verdict. A feedback system with
   no stability condition is an oscillator, not a safeguard.
2. **Weight the Judge by reversibility.** The less abortable the action, the more the
   *before* mode must carry, because *during* and *after* cannot undo it. Once you have
   cut, after-judgment can only mitigate, never reverse. Irreversibility shifts the
   burden forward, onto the pre-commit judgment.
3. **The after-verdict becomes data.** Not only the raw result re-enters the Data realm,
   but the Judge's assessment of it: "we tried X, it diverged, here is why." The next
   Gate admits it and the next Brain does not repeat the mistake. That is how the loop
   *learns* instead of merely spinning. The Judge is both the referee and the author of
   the next round's evidence.
