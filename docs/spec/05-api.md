# 05 — AISpec API

---

# Purpose

The AISpec API defines the logical interface used to interact with an AISpec repository.

It provides a consistent abstraction for creating, reading, updating, validating, and navigating repositories, regardless of the underlying programming language or storage implementation.

The API represents the contract between applications and the AISpec Engine.

---

# Design Goals

The API should remain:

* Simple
* Predictable
* Language-independent
* Stateless
* Deterministic
* Easy to implement

Every AISpec SDK should expose equivalent operations, even if syntax differs.

---

# Architecture

```text
Application
      │
      ▼
 AISpec SDK
      │
      ▼
 AISpec API
      │
      ▼
 AISpec Engine
      │
      ▼
 Repository
```

The API does not manipulate files directly.

It communicates with the Engine.

The Engine manages persistence.

---

# Core Objects

The API operates on a small set of objects.

* Repository
* Commit
* Snapshot
* Branch
* Node
* Edge
* Connector
* Artifact
* Evaluation

Every operation acts upon one or more of these objects.

---

# Core Operations

Every AISpec implementation should expose the following logical operations.

## Repository

* Create
* Open
* Save
* Close
* Validate

---

## Commit

* Create
* Read
* List
* Search

---

## Snapshot

* Create
* Read
* Compare
* Restore

---

## Branch

* Create
* Switch
* Merge
* Delete
* List

---

## Graph

* Traverse
* Search
* Visualize
* Analyze

---

## Validation

* Validate Repository
* Validate Object
* Validate Graph

---

# Object Lifecycle

Typical workflow:

```text
Repository

↓

Edit Node

↓

Create Snapshot

↓

Create Commit

↓

Validate

↓

Push
```

The API exposes every step.

---

# Stateless Design

API operations SHOULD be stateless.

Each request contains all information required to complete the operation.

The API SHOULD NOT rely on hidden global state.

---

# Deterministic Behavior

Given the same repository and the same operation:

The API MUST always produce the same result.

Behavior MUST remain deterministic across implementations.

---

# Error Handling

Every operation SHOULD return structured errors.

Errors SHOULD include:

* Code
* Message
* Object
* Cause

Example:

```text
INVALID_SNAPSHOT_REFERENCE
```

Errors should be machine-readable.

---

# Serialization

The API SHOULD accept and produce canonical AISpec objects.

Canonical serialization:

* YAML

Optional serialization:

* JSON

Other formats MAY exist internally.

---

# Version Negotiation

The API SHOULD expose the supported AISpec version.

Example:

```text
AISpec 1.0.0
```

Applications SHOULD verify compatibility before executing operations.

---

# Thread Safety

Concurrent operations SHOULD produce deterministic results.

Implementations MAY provide synchronization internally.

The specification does not require a specific concurrency model.

---

# Security

The API SHOULD:

* validate all inputs
* reject malformed objects
* avoid executing repository content
* never expose secrets

Credentials SHOULD remain outside the repository.

---

# Extensibility

The API SHOULD remain minimal.

New functionality SHOULD be introduced through Extensions whenever possible.

The core API should evolve slowly.

---

# Compatibility

Future API versions SHOULD preserve backward compatibility.

Breaking changes SHOULD occur only during Major releases.

Unknown optional fields MUST be ignored.

---

# Future Work

Future versions may define:

* Remote API
* Streaming API
* Cloud Synchronization API
* Enterprise API
* Event API
* WebSocket API

---

# Summary

The AISpec API provides a stable, deterministic, and language-independent interface for interacting with AISpec repositories.

It separates applications from storage details, enabling every SDK and Engine to expose a consistent programming model while preserving interoperability across the AISpec ecosystem.
