# The Standard for Agent Skills

A standard for **writing**, **consuming**, and **managing** skills for agents.

**Version 0.7.0**, under active authorship and not yet ratified. See [CHANGELOG.md](./CHANGELOG.md).

This repository is a *specification*, not a framework. It describes how a skill
should be authored, how an agent should read and act on it, and how skills should
be governed once they live among other skills. Implementations, including any
tooling or portal, are separate builds that **conform to** this document; the
document does not bend to them.

---

## The Tri-Nature Theory

Every system is three things:

- **Dependency**: what the thing is built on; what everything downstream depends on.
- **Purpose**: what it is *for*; the behavior, the doing, the logic core.
- **Exposure**: the outward contact surface where it meets the world.

The theory is *fractal*: three inside three, Dependency then Purpose then Exposure all
the way down. At every level the three appear in the same order, **D, P, E**. This
document is organized entirely along that spine, and each node declares which of the
three natures it is.

The order matters. A structure that seats its three parts cleanly, with no
nature-bleed and no mislabeled node, is one you can trust. Where the world resists the
lens, we trust the world and say so, rather than force the frame.

---

## The Spine

```
0 / Writing skills ............... DEPENDENCY   the artifact an agent depends on
1 / Consuming skills ............. PURPOSE       why skills exist: an agent using them
2 / Managing skills .............. EXPOSURE      the ecosystem: skills among skills, at scale
```

Writing, then Consuming, then Managing is itself a Dependency, Purpose, Exposure: you
build the thing depended upon, then the agent puts it to purpose, then it is exposed
and governed among the many.

| Chapter | Nature | Covers |
|---|---|---|
| [0 / Writing skills](./0-writing-skills) | Dependency | Structure, Rules, Language: how a skill is authored |
| [1 / Consuming skills](./1-consuming-skills) | Purpose | Priority, Implementation, Output: how an agent reads and acts on a skill |
| [2 / Managing skills](./2-managing-skills) | Exposure | Publishing, Governance, Registry: how skills live among skills |

---

## Table of Contents

- [Introduction](./introduction/README.md)
  - [Natural Language Is the New Programming Language](./introduction/README.md#natural-language-is-the-new-programming-language)
  - [Why Skills Must Be Standardized](./introduction/README.md#why-skills-must-be-standardized)
  - [The Standard, and Why a New One](./introduction/README.md#the-standard-and-why-a-new-one)
  - [Blessing or Curse](./introduction/README.md#blessing-or-curse)
- [The SKILL of All SKILLs (the constitution)](./the-skill-of-all-skills/SKILL.md)
- [0 Writing Skills](./0-writing-skills/README.md)
  - [0.0 Structure](./0-writing-skills/README.md#00-structure-dependency)
    - [0.0.0 Definition and Requirements](./0-writing-skills/README.md#000-definition-requirements-dependency)
    - [0.0.1 Action](./0-writing-skills/README.md#001-action-purpose)
    - [0.0.2 Outcomes](./0-writing-skills/README.md#002-outcomes-exposure)
  - [0.1 Rules](./0-writing-skills/README.md#01-rules-purpose)
  - [0.2 Language](./0-writing-skills/README.md#02-language-exposure)
    - [0.2.0 Terms](./0-writing-skills/README.md#020-terms-dependency)
    - [0.2.1 Directive](./0-writing-skills/README.md#021-directive-purpose)
    - [0.2.2 Clarity](./0-writing-skills/README.md#022-clarity-exposure)
- [1 Consuming Skills](./1-consuming-skills/README.md)
  - [Consumption is a Skill, Not an Interpretation](./1-consuming-skills/README.md#consumption-is-a-skill-not-an-interpretation)
  - [The Decision Realm: Gate, Brain, Judge](./1-consuming-skills/README.md#the-decision-realm-gate-brain-judge)
  - [1.0 Priority: the Gate](./1-consuming-skills/README.md#10-priority-dependency-the-gate)
  - [1.1 Implementation: the Brain](./1-consuming-skills/README.md#11-implementation-purpose-the-brain)
  - [1.2 Output: the Judge](./1-consuming-skills/README.md#12-output-exposure-the-judge)
- [2 Managing Skills](./2-managing-skills/README.md)
  - [2.0 Publishing: the Build Pipeline](./2-managing-skills/README.md#20-publishing-dependency-the-build-pipeline)
  - [2.1 Governance: the Life of the Pool](./2-managing-skills/README.md#21-governance-purpose-the-life-of-the-pool)
  - [2.2 Registry: the Compatibility Contract](./2-managing-skills/README.md#22-registry-exposure-the-catalog-and-the-compatibility-contract)

Status: all nine nodes now have a first full draft. Chapters 0 (Writing), 1 (Consuming),
and 2 (Managing) are complete. The Standard remains under active authorship and is not
yet ratified; ratification is reserved for version 1.0.0.
