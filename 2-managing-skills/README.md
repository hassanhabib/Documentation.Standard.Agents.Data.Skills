# 2 / Managing Skills

**Nature: Exposure.**

This is the outermost layer, the ecosystem. A single agent with a single local skill
needs only Writing and Consuming; Managing matters once skills exist *at scale, among
other skills, across agents*. It is the outward surface where skills are admitted,
governed, discovered, and retired. That makes it the true exposure layer, and the reason
it comes last.

The Standard defines *what* this ecosystem must guarantee, never *how* it is built.
Where skills are stored, a database, a git repository, or plain files, is an
implementation choice beneath the Standard. This chapter specifies guarantees, not a
backend.

It decomposes into its own three natures:

```
2.0 Publishing ...... (D)  the build pipeline: nothing enters the pool unless it is valid
2.1 Governance ...... (P)  the life of the pool: versioning, scanning, review, deprecation
2.2 Registry ........ (E)  the catalog and distribution surface, and the compatibility contract
```

### Two lines of defense

Managing is the *cold* line of defense; Consuming (Chapter 1) is the *hot* one.

- **Cold, at publish time (this chapter):** the pipeline validates, tests, scans, and
  reviews a skill before it can ever enter the pool.
- **Hot, at runtime (Chapter 1):** the Gate admits and the Judge judges in context,
  catching what only appears when the skill actually runs.

Neither alone is sufficient. The pipeline cannot foresee every runtime context; the
runtime cannot re-derive a full audit on every call. Defense in depth. And note the
symmetry: **2.0 Publishing is Chapter 1's Gate at ecosystem scale.** The Gate admits a
skill into an agent's context; the pipeline admits a skill into the pool. The same
dependency-slot guardian, at two scales.

### Rigor is proportional

The machinery below scales with stakes. A low-stakes deployment may run light, with
warnings where a hospital would refuse. The Standard defines the mechanism; the
deployment sets the threshold. Proportionality is the same principle the Judge uses: the
weight of the safeguard tracks the weight of the consequence.

---

## 2.0 Publishing, *(Dependency)*: the build pipeline

You cannot just submit anything. Publishing is a gated pipeline, and failing any stage
means the skill is rejected, not published. The stages, in order:

1. **Structure validation** (per Chapter 0): is it a valid skill at all? Malformed
   structure is rejected here.
2. **Language checks** (per 0.2): ambiguity, imperative form, obeyability.
3. **Dependency resolution:** every requirement a skill declares in its Definition and
   Requirements (`0.0.0`) must resolve. At scale those declarations form a dependency
   graph: other skills, tools, memory schemas, and a compatible model. Management is
   aware of the tool *contract* a skill depends on, not the tool itself; tools are owned
   by their own standard (`Standard.Agents`, tools). Management references, it does not
   absorb.
4. **Testing across a model matrix:** run the skill's test cases on each supported model
   and record how faithfully each obeys it. This produces the compatibility and fidelity
   metadata that the Registry pins (see 2.2).
5. **Security scanning:** the skill-native equivalent of dependency scanning, with a
   different threat model. Skills are natural language, so the threats are prompt
   injection, jailbreaks, exfiltration instructions, policy subversion, and adversarial
   collision with the constitution. This is semantic red-teaming, an adversarial
   discipline of its own, not a CVE match.
6. **Collision scanning:** check the newcomer against the whole pool for contradictions.
   This is the *cold* collision check that Chapter 1's runtime detection feeds.
7. **Review:** human sign-off, scaled to stakes. Domain-critical skills require
   domain-qualified review; a skill that informs surgery needs a surgeon in the loop, or
   "reviewed" is theater.
8. **Publish:** signed, versioned, and admitted to the Registry.

A green build is *necessary, never sufficient*. LLM behavior is not exhaustively
testable: the matrix is finite, the input space is not. The pipeline proves "passed known
checks," never "safe." That is exactly why the hot line of defense must remain, and why
high-stakes skills earn bounded deployment rather than a victory lap.

For example, a submitted skill whose entire Action reads "clean up old data when needed"
fails at stage 1 and stage 2: it declares no modality, names no target, and defines no
Outcome, so it is neither valid structure nor testable language. The pipeline rejects it
with those reasons, and it never reaches the pool.

---

## 2.1 Governance, *(Purpose)*: the life of the pool

The ongoing logic over the pooled skills:

- **Versioning.** Skills are versioned. A change to a skill's behavior contract is a
  **breaking change** and forces a major bump; consumers opt in, never silently. Chapter
  1's Gate pins the version it consumes, so a skill cannot change underneath a consumer.
- **Deprecation and sunsetting**, with a migration path, never a silent removal.
- **Continuous scanning.** Security and collision scans run forever, not only at
  admission. A newly disclosed attack, or a new member of the pool, can make an
  already-published skill unsafe after the fact. A published skill found unsafe is
  quarantined.
- **Review lifecycle:** any change re-opens review.

The **constitution** (the SKILL for consuming skills, see Chapter 1) is the extreme case
of every rule here. Its review is the most stringent, its signing the most protected, and
a breaking change to it is a coordinated rollout, because it changes how every skill is
consumed.

---

## 2.2 Registry, *(Exposure)*: the catalog and the compatibility contract

The surface humans and agents actually touch: listing, discovery, search, and
distribution, plus the dashboard that raises collision and security warnings. It also
holds the one piece of metadata that is safety-critical rather than convenient.

### The model-compatibility contract

A skill's behavior is **model-specific**: a skill validated on one model is not proven
safe on another. Certification is graded, not binary. Each (skill, exact model and
version) pair carries a fidelity score; "compatible" means the score clears a threshold
that rises with stakes; the "most responsive" model is simply the highest-fidelity one.
The Registry pins this matrix, and it is the contract Chapter 1's Gate consults at runtime.

### The severity ladder (reaches into Chapter 1)

Before the Gate admits a skill, it reads the Registry and applies severity as a function
of the certification status crossed with the stakes of the action:

| (skill x model) status | severity |
|---|---|
| Certified compatible, this exact model and version | **pass** |
| Certified on the same model, a different version | **warning**, escalating to **error** at high stakes |
| Unknown model, no data | **error** and fail closed, escalating to **critical fail** at high stakes; only a low-stakes deployment may relax to warning |
| Certified incompatible, known to misbehave | **critical fail**, at any stakes |

The levels:

- **pass:** proceed.
- **warning:** proceed, but surface and log the uncertified pairing.
- **error:** refuse the action; halt to a human, who may authorize a single logged
  exception, which itself files a certification request.
- **critical fail:** a hard block, not overridable at runtime. The only remedy is
  re-certification in the pipeline, an out-of-band act, the same rule that protects the
  constitution from being amended from inside the loop.

Two rules make this Amanah-grade:

- **Incompatible is a hard block at any stakes.** We hold positive evidence of failure;
  a "low stakes" judgment might itself be wrong, and known-bad is known-bad.
- **Unknown fails closed.** Silence is not consent. Absence of certification is treated
  as unsafe, and the treatment grows heavier as stakes rise.

Certification drifts: a model update invalidates certification for that model until the
pipeline re-runs. Pin exact model versions.

For example, take a skill certified compatible on model-A version 1 at fidelity 0.94:

- On model-A version 1, a routine action: pass.
- On model-A version 2, the same action: warning, because the version changed; at high
  stakes, error until re-certified.
- On model-B, never tested: error and fail closed; at high stakes, critical fail.
- On any model where it was certified incompatible: critical fail, whatever the stakes.

---

## A note on the portal

Managing is where this Standard meets tooling. It will need a real
**skills-management portal**: the pipeline, the registry and its compatibility matrix,
the governance controls, and the warning dashboard. That portal is a **separate build
that conforms to this Standard**. It does not belong in this repository. The Standard is
written first; the portal is built to match it; neither is allowed to bend the other.
