# 10 — Glossary

---

# Purpose

This glossary defines the official terminology used throughout the AISpec specification.

Every term has one canonical meaning.

Implementations SHOULD use these definitions consistently to ensure interoperability across the ecosystem.

---

# Agent

An autonomous software entity capable of performing tasks, making decisions, and interacting with other components within an AI system.

---

# API

The logical programming interface used by applications to interact with AISpec repositories through the Engine.

---

# Artifact

Any generated resource associated with a repository.

Examples include:

* documents
* datasets
* images
* prompts
* evaluation reports
* configuration files

Artifacts may be versioned through Snapshots.

---

# Branch

An independent line of development within a repository.

Branches allow parallel experimentation while preserving repository history.

---

# Canonical Format

The official representation of AISpec objects.

The canonical serialization format is YAML.

---

# Commit

An immutable record describing one repository change.

A Commit references one or more Snapshots and preserves repository history.

---

# Connector

A component that connects a Node to an external system, service, model, API, or data source.

---

# Edge

A directional relationship between two Nodes in the AISpec Graph.

Edges describe structure, not execution.

---

# Engine

The reference implementation responsible for managing repositories, validation, history, graph construction, and storage coordination.

---

# Extension

An optional capability that extends AISpec without modifying the core specification.

Extensions remain isolated from the standard.

---

# Graph

The complete structural representation of an AI system.

The Graph consists of Nodes connected by Edges.

---

# Node

A logical object representing an entity within an AI system.

Examples include:

* Agent
* Tool
* Workflow
* Memory
* Connector
* Model
* Prompt

---

# Repository

The complete AISpec project.

A repository contains all objects, history, metadata, and configuration required to reconstruct an AI system.

---

# RFC

A Request for Comments document.

RFCs define the normative rules of the AISpec specification.

---

# SDK

A Software Development Kit that provides language-specific access to AISpec repositories.

SDKs expose the AISpec API to developers.

---

# Snapshot

An immutable representation of the state of a Node at a specific point in time.

Snapshots capture object evolution independently of repository history.

---

# Specification

The complete collection of RFCs and documentation that define AISpec.

The specification describes expected behavior but does not prescribe implementation details.

---

# Storage Engine

The logical subsystem responsible for persisting, indexing, retrieving, and reconstructing repository objects.

The filesystem is the canonical storage model.

---

# Validation

The process of verifying that a repository conforms to the AISpec specification.

Validation checks object integrity, references, schemas, and graph consistency.

---

# Version

The declared release of the AISpec specification used by a repository or implementation.

AISpec follows Semantic Versioning.

---

# YAML

The canonical serialization format used by AISpec.

Repositories SHOULD remain human-readable and editable using standard YAML documents.

---

# Interoperability

The ability of different implementations, SDKs, Engines, and platforms to exchange AISpec repositories without modification or loss of information.

Interoperability is one of the primary goals of the specification.

---

# Vendor Neutral

A design principle stating that AISpec is independent of any programming language, AI provider, cloud platform, framework, or commercial vendor.

Repositories remain portable across implementations.

---

# Deterministic

A property of AISpec stating that identical inputs should always produce identical logical outputs, regardless of implementation.

Deterministic behavior is essential for validation and interoperability.

---

# Immutability

The principle that Commits and Snapshots cannot be modified after creation.

Changes are represented by creating new objects rather than editing existing ones.

---

# Semantic Versioning

The versioning strategy used by AISpec.

Version numbers follow the format:

```text id="3o7r2u"
MAJOR.MINOR.PATCH
```

Major versions introduce breaking changes.

Minor versions add compatible functionality.

Patch versions fix errors without changing behavior.

---

# Summary

This glossary establishes a shared vocabulary for the AISpec ecosystem.

By defining consistent terminology across the specification, documentation, SDKs, and implementations, AISpec ensures that developers, organizations, and tools interpret the standard in the same way, strengthening interoperability and long-term maintainability.
