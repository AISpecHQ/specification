# 04 — AISpec Specification

---

# Purpose

AISpec is an open specification for versioning, describing, and managing AI systems.

It provides a universal, vendor-neutral standard for representing AI projects as structured, portable, and version-controlled repositories.

AISpec defines **how AI systems are described**, not **how they are executed**.

---

# Design Goals

AISpec is designed to be:

* Small
* Stable
* Predictable
* Portable
* Human-readable
* Extensible
* Language-independent
* Vendor-neutral

The specification should remain simple enough to implement while being powerful enough to support projects ranging from individual experiments to enterprise-scale AI systems.

---

# Core Concepts

AISpec is built around a small number of fundamental concepts.

* Repository
* Commit
* Snapshot
* Branch
* Graph
* Validation
* Engine
* SDK
* CLI
* Extensions

Every AISpec implementation is expected to build upon these concepts.

---

# Repository

A Repository is the root container of an AISpec project.

It contains every object required to reconstruct an AI system, including:

* Commits
* Snapshots
* Branches
* Nodes
* Configuration
* Metadata

The Repository is the primary unit of portability.

For repository layout, see **RFC-0001**.

---

# Commit

A Commit represents an immutable record of change.

Each Commit references one or more Snapshots and forms part of the permanent repository history.

Commits are never modified after creation.

For the Commit format, see **RFC-0002**.

---

# Snapshot

A Snapshot captures the complete state of a Node at a specific point in time.

Snapshots allow repositories to reconstruct historical states without modifying previous versions.

For the Snapshot format, see **RFC-0003**.

---

# Branch

Branches enable parallel development within a repository.

Multiple ideas, experiments, or releases may evolve independently before being merged into a common history.

For Branch behavior, see **RFC-0004**.

---

# Graph

Every AISpec repository represents an AI system as a directed graph.

Nodes describe entities.

Edges describe relationships.

The graph provides the structural representation of the repository independently of execution.

For the Graph Model, see **RFC-0006**.

---

# Validation

Validation guarantees repository integrity.

A valid repository has:

* consistent object identifiers
* valid references
* compliant schemas
* consistent graph relationships

Validation rules are defined in **RFC-0005**.

---

# Storage

AISpec repositories are stored as human-readable files.

The filesystem is the canonical storage model.

Indexes, databases, and caches are optional implementation details.

Storage behavior is defined in **RFC-0009**.

---

# API

The AISpec API defines the logical interface used by applications to interact with repositories.

The API abstracts storage details and exposes consistent operations across implementations.

See **05 — AISpec API**.

---

# Engine

The AISpec Engine is the reference implementation responsible for repository management.

It coordinates:

* validation
* history
* graph construction
* storage
* indexing

The Engine is implementation-specific but must comply with the AISpec specification.

See **06 — AISpec Engine**.

---

# SDK

AISpec SDKs provide language-specific developer libraries.

Official SDKs expose equivalent functionality regardless of programming language.

See **07 — AISpec SDK**.

---

# CLI

The AISpec Command Line Interface provides a standard terminal experience for interacting with repositories.

Typical operations include:

* repository creation
* commits
* branching
* validation
* graph inspection

See **11 — AISpec CLI**.

---

# Cloud

AISpec Cloud is the hosted collaboration platform built on top of the specification.

It provides synchronization, visualization, collaboration, and repository hosting.

Cloud services are optional and do not affect repository portability.

See **08 — AISpec Cloud**.

---

# Extensions

Extensions allow new capabilities to be added without modifying the core specification.

Implementations may support additional functionality while preserving compatibility with the standard.

Extension behavior is defined in **RFC-0007**.

---

# Versioning

AISpec follows Semantic Versioning.

Repositories declare the specification version they target.

Backward compatibility is prioritized whenever possible.

Versioning rules are defined in **RFC-0008**.

---

# Repository Lifecycle

The typical lifecycle of an AISpec repository is:

```text
Initialize Repository
        ↓
Create Nodes
        ↓
Create Snapshots
        ↓
Create Commits
        ↓
Create Branches
        ↓
Validate
        ↓
Merge
        ↓
Release
```

Every implementation should preserve this logical workflow.

---

# Ecosystem

The AISpec ecosystem consists of four primary layers:

```text
Applications

↓

SDKs

↓

AISpec API

↓

AISpec Engine

↓

Repository
```

Optional products built on top of this foundation include:

* AISpec CLI
* AISpec Cloud
* Enterprise solutions
* Extensions
* Third-party tooling

---

# Specification Structure

The AISpec specification is organized into two complementary sections.

**Normative Documents (RFCs)**

The RFC series defines the official rules of the specification.

These documents contain normative language such as **MUST**, **SHOULD**, and **MAY**.

**Reference Documentation**

The `docs/spec` directory explains the architecture, concepts, and intended usage of AISpec.

These documents are informative and designed to help developers understand the standard.

---

# References

Core specification:

* RFC-0000 — Core Philosophy
* RFC-0001 — Repository Layout
* RFC-0002 — Commit Format
* RFC-0003 — Snapshot Format
* RFC-0004 — Branch Format
* RFC-0005 — Validation Rules
* RFC-0006 — Graph Model
* RFC-0007 — Extension System
* RFC-0008 — Versioning Strategy
* RFC-0009 — Storage Engine
* RFC-0010 — SDK Compliance

Supporting documentation:

* 05 — AISpec API
* 06 — AISpec Engine
* 07 — AISpec SDK
* 08 — AISpec Cloud
* 09 — Roadmap
* 10 — Glossary
* 11 — CLI

---

# Summary

AISpec provides a universal, open, and portable specification for versioning AI systems.

By combining immutable history, graph-based modeling, deterministic validation, and language-independent tooling, AISpec establishes a common foundation upon which developers, organizations, and AI platforms can build interoperable tools and workflows for the next generation of AI engineering.
