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

## 1.0 Priority, *(Dependency)*

The intake layer, the precondition of consumption. Before an agent acts, it must
pull the skill, load whatever the skill *references* (references are intake, a
dependency, not an exposure: the agent reaches inward for them), and resolve whether
the skill applies and how it ranks against everything else in play.

Priority is the mechanism that resolves conflict. Collision handling is its failure
mode.

### Collision handling

Two skills *collide* only when they direct the same thing in opposite ways at the same
standing. Priority resolves conflicts through a deterministic ladder, and escalation is
the **last** rung, not the first move:

| Situation | Resolution |
|---|---|
| Different priority | Higher priority wins. Deterministic. |
| Same priority, different level | The more specific or more local level wins. Deterministic. |
| Same priority, same level, **composable** | Do both. Not a collision. |
| Same priority, same level, **redundant** (same ask, same way) | Dedupe or soft-note. Not a collision. |
| Same priority, same level, **contradictory** (same ask, opposite ways) | **Genuine tie. Escalate.** |

The agent must first *classify*: composable, redundant, or contradictory. Only a
true contradiction is a collision.

On a genuine collision the agent must **fail closed**:

1. **Halt only the conflicted action**, not the whole task.
2. **Name the collision precisely.** Never a vague "I'm confused," and never a silent
   guess (silently choosing one of two contradictory directives is the worst outcome:
   non-deterministic, unauditable, possibly the exact opposite of intent):

   > "Skill **A** says *do X*; Skill **B** says *do not-X*. Both at priority P, level L.
   > I can't resolve this deterministically. Which should win?"

3. **Offer the tiebreak** so the human answers with a single choice.

A live collision is also an **Output** (see 1.2) event: it feeds back to the Managing
layer (Chapter 2), where the portal detects collisions *cold*, across the pool. The
agent detects them *hot*, in a real runtime context the static check could not predict.
The same concern refracted through two natures: Purpose teaching Exposure.

---

## 1.1 Implementation, *(Purpose)*

> Status: to be drilled.

The act itself: the agent applying the skill once intake and priority are resolved.

---

## 1.2 Output, *(Exposure)*

> Status: to be drilled.

What the agent surfaces after applying the skill: the response, the action taken, the
result made visible. This is the true exposer of consumption, the thing crossing the
boundary back out, and the channel through which runtime events (such as collisions)
are reported to the Managing layer.
