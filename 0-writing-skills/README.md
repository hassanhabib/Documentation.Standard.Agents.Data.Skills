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

---

## 0.1 Rules, *(Purpose)*

> Status: to be drilled.

The constraints that govern a skill: what an author must and must not do. Scope and
single-responsibility live here: where one skill ends and another begins, so that a
skill stays one thing and does not sprawl into a god-skill.

---

## 0.2 Language, *(Exposure)*

> Status: to be drilled.

The voice through which a skill exposes its intent to the agent that reads it.
Structure is the form and Rules are the law; Language is how the instructions are
actually written so an agent reliably understands and obeys them: imperative,
unambiguous, addressed to the agent, worked examples over abstraction. It is the
most consequential and most commonly mishandled part of authoring.
