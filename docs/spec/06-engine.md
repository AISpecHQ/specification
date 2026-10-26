# 06 — AISpec Engine

---

# Purpose

The AISpec Engine is the reference execution layer responsible for managing AISpec repositories.

It provides the core functionality required to create, read, validate, version, index, and reconstruct repositories while remaining independent of user interfaces and programming languages.

The Engine is the implementation of the AISpec specification.

---

# Philosophy

The Engine is the heart of AISpec.

Applications interact with the Engine rather than directly manipulating repository files.

The Engine guarantees that every operation complies with the AISpec specification.

---

# Design Goals

The Engine should be:

* Fast
* Deterministic
* Portable
* Extensible
* Reliable
* Language-independent

Implementations should behave consistently across operating systems and programming languages.

---

# Responsibilities

The Engine is responsible for:

* Repository management
* Commit creation
* Snapshot creation
* Branch management
* Graph construction
* Validation
* Object indexing
* Repository reconstruction

The Engine is not responsible for:

* Running AI models
* Executing workflows
* User interfaces
* Cloud synchronization

---

# High-Level Architecture

```text id="jv4i8p"
Applications

↓

SDK

↓

API

↓

AISpec Engine

↓

Storage Engine

↓

Repository
```

The Engine acts as the central coordinator between applications and storage.

---

# Core Modules

The Engine is composed of several logical modules.

## Repository Manager

Creates, opens, saves, and closes repositories.

---

## Commit Manager

Creates immutable Commit objects.

Maintains repository history.

---

## Snapshot Manager

Creates immutable Snapshots.

Tracks object state over time.

---

## Branch Manager

Creates, merges, and manages Branches.

Maintains independent development histories.

---

## Graph Manager

Builds and traverses the repository graph.

Provides dependency analysis.

Supports visualization tools.

---

## Validation Manager

Validates repositories according to the published RFCs.

Produces deterministic validation results.

---

## Storage Manager

Reads and writes repository objects.

Coordinates with the Storage Engine.

---

## Index Manager

Builds optional indexes for fast lookup.

Indexes are disposable.

The repository remains the source of truth.

---

# Engine Lifecycle

Typical lifecycle:

```text id="ig74nk"
Open Repository

↓

Load Objects

↓

Build Graph

↓

Validate

↓

Apply Changes

↓

Create Snapshot

↓

Create Commit

↓

Update Index

↓

Save Repository
```

For filesystem-backed Engines, saving synchronizes canonical file contents
through the operating system's file synchronization mechanism. This is not an
atomic multi-file transaction; the persistence limits are defined by
[RFC-0010](../rfc/RFC-0010-SDK-Compliance.md) and
[RFC-0009](../rfc/RFC-0009-Storage-Engine.md).

---

# Object Cache

The Engine MAY maintain an in-memory cache.

The cache SHOULD improve:

* repository loading
* graph traversal
* object lookup
* validation

The cache MUST NOT become the source of truth.

---

# Deterministic Behavior

The Engine MUST produce identical logical results for identical repositories.

Object ordering, validation, graph construction, and history reconstruction should remain deterministic.

---

# Performance

The Engine SHOULD optimize:

* repository loading
* commit history traversal
* snapshot lookup
* graph traversal
* validation

Performance optimizations MUST NOT change repository semantics.

---

# Error Handling

The Engine SHOULD return structured errors.

Every error SHOULD include:

* error code
* message
* affected object
* severity

Errors should remain implementation-independent.

---

# Security

The Engine SHOULD:

* validate repository integrity
* reject malformed objects
* avoid executing repository content
* isolate external extensions
* prevent data corruption

Secrets SHOULD never be stored inside repository objects.

---

# Extensibility

The Engine SHOULD support optional Extensions.

Extensions MUST NOT modify core Engine behavior.

Unsupported Extensions SHOULD be ignored gracefully.

---

# Compatibility

Every Engine implementation MUST comply with the AISpec specification.

Different Engine implementations should produce equivalent repositories when performing identical operations.

---

# Future Work

Future versions may introduce:

* Incremental loading
* Distributed repositories
* Remote repositories
* Cloud synchronization
* Background indexing
* Live collaboration
* Incremental validation

---

# Summary

The AISpec Engine is the core implementation of the AISpec specification.

It manages repositories, preserves history, constructs the graph, validates objects, and coordinates storage while remaining deterministic, portable, and independent of user interfaces or AI frameworks.

It serves as the foundation upon which SDKs, CLIs, desktop applications, web platforms, and enterprise solutions are built.
