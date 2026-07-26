# 2 / Managing Skills

**Nature: Exposure.**

This is the outermost layer — the ecosystem. A single agent with a single local skill
needs only Writing and Consuming; Managing matters once skills exist *at scale, among
other skills, across agents*. It is the outward surface where skills are stored,
governed, discovered, versioned, and retired. That makes it the true exposure layer,
and the reason it comes last.

It decomposes into its own three natures:

```
2.0 Storage ......... (D)  — where skills live
2.1 Governance ...... (P)  — the logic of a pool of skills
2.2 Distribution .... (E)  — the surface humans and agents touch
```

> 🟨 The three subsections below are sketched, not yet locked.

---

## 2.0 Storage — *(Dependency)*

> 🟨 Sketched.

The registry — where skills live, their identity, and their versions. The dependency
the rest of the ecosystem is built on.

---

## 2.1 Governance — *(Purpose)*

> 🟨 Sketched.

The logic of a *pool* of skills: skill-to-skill relationships, versioning and
deprecation, and collision detection across the whole pool — the *cold* counterpart to
the *hot* detection an agent performs at runtime (§1.0). Runtime collision events
emitted as Output (§1.2) are ingested here.

---

## 2.2 Distribution — *(Exposure)*

> 🟨 Sketched.

The surface humans and agents actually touch: discovery and search, publish and
deprecate controls, and the dashboard that raises warnings — including collisions.

---

## A note on the portal

Managing is where this standard meets tooling: it will need a real
**skills-management portal** — a registry, collision detection across the pool, and a
dashboard. That portal is a **separate build that conforms to this standard**. It does
not belong in this repository. The standard is written first; the portal is built to
match it; neither is allowed to bend the other.
