# Principles

> **These principles define the long-term philosophy of AISpec.**
>
> Every architectural decision, feature request and future RFC must be evaluated against these principles.

---

# Principle 1 — Open Standard

AISpec is an open specification.

The specification must always remain publicly available.

Any developer, organization or vendor should be able to implement AISpec without requiring permission.

The ecosystem grows through interoperability, not lock-in.

---

# Principle 2 — Vendor Agnostic

AISpec must never depend on a specific AI provider.

Examples include, but are not limited to:

* OpenAI
* Anthropic
* Google
* xAI
* Mistral
* Local models

Providers are implementations.

AISpec is the language that describes them.

---

# Principle 3 — Framework Agnostic

AISpec should work with any AI framework.

Examples include:

* LangGraph
* CrewAI
* AutoGen
* n8n
* Custom applications

Frameworks evolve.

AISpec should remain stable.

---

# Principle 4 — Language Agnostic

AISpec should be implementable from any programming language.

Examples include:

* TypeScript
* Python
* Go
* Rust
* Java
* C#

The specification must never favor one language over another.

---

# Principle 5 — Version First

Versioning is the foundation of AISpec.

Every meaningful change should be representable as a new version.

History must be treated as a first-class concept.

---

# Principle 6 — Immutable History

Published versions should never be modified.

A correction creates a new version.

History remains permanent and auditable.

---

# Principle 7 — Human Readable

The specification should be understandable without proprietary software.

Configuration should remain readable and reviewable by humans.

---

# Principle 8 — Machine Friendly

Although human-readable, AISpec must also be deterministic and easy for software to parse.

Tools should never rely on ambiguous interpretations.

---

# Principle 9 — Portable

A project described using AISpec should be movable between environments with minimal changes.

Portability is more important than vendor-specific optimizations.

---

# Principle 10 — Extensible

The specification must evolve through extensions instead of breaking existing projects.

Backward compatibility should always be preferred.

---

# Principle 11 — Minimal Core

The core specification should remain intentionally small.

Only concepts that are universally useful belong in the core.

Specialized features should live in optional extensions.

---

# Principle 12 — Explicit Over Implicit

AISpec should avoid hidden behavior.

Configuration should be declared explicitly whenever possible.

Predictability is preferred over convenience.

---

# Principle 13 — Observable

Every version should be explainable.

Users should be able to understand:

* what changed,
* why it changed,
* when it changed,
* and how it affects the system.

---

# Principle 14 — Reproducible

A historical version should always be reproducible.

The same specification should describe the same system regardless of where it is executed.

---

# Principle 15 — Security by Design

AISpec should encourage secure defaults.

Sensitive information should never be embedded directly into the specification.

Secrets must be referenced, not stored.

---

# Principle 16 — Community Driven

AISpec evolves through public discussion.

Major changes should be proposed through RFCs.

The specification should grow through consensus instead of arbitrary decisions.

---

# Decision Checklist

Before introducing any new feature, ask:

* Does it preserve portability?
* Does it remain vendor agnostic?
* Does it simplify the specification?
* Does it improve reproducibility?
* Does it avoid breaking existing projects?
* Does it belong in the core instead of an extension?
* Will it still make sense in ten years?

If the answer to multiple questions is "no", the proposal should be reconsidered.

---

# Final Principle

AISpec is not designed for today's AI ecosystem.

AISpec is designed to remain useful as the AI ecosystem changes over the next decade.

The specification should outlive individual models, providers and frameworks.
