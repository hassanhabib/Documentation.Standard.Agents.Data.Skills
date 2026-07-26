# The Standard for Agent Skills

A standard for **writing**, **consuming**, and **managing** skills for agents.

**Version 0.1.0**, under active authorship and not yet ratified. See [CHANGELOG.md](./CHANGELOG.md).

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
| [2 / Managing skills](./2-managing-skills) | Exposure | Storage, Governance, Distribution: how skills live among skills |

---

## Status

This standard is being written. Each node below is marked with its state.

- **0 / Writing skills**
  - 0.0 Structure: [drilled]
  - 0.1 Rules: [to drill]
  - 0.2 Language: [to drill]
- **1 / Consuming skills**
  - 1.0 Priority: [drilled] (the Gate: relevance, trust, context economy, collision handling)
  - 1.1 Implementation: [drilled] (the Brain: executes the consumption skill; free in domain, bound in protocol)
  - 1.2 Output: [drilled] (the Judge: judges the whole before/during/after; permit/reiterate/halt; closed loop)
- **2 / Managing skills**
  - 2.0 Storage: [sketched]
  - 2.1 Governance: [sketched]
  - 2.2 Distribution: [sketched]
