# RFC-0001 — Repository Layout

**Status:** Draft

**Version:** 0.1

---

# Purpose

This RFC defines the canonical directory structure of an AISpec repository.

A compliant implementation MUST understand this structure.

Internal implementation details may differ.

The logical repository layout MUST remain compatible.

---

# Philosophy

An AISpec repository should be:

* Predictable
* Portable
* Human-readable
* Machine-readable

Developers should recognize any AISpec repository immediately, regardless of the programming language or framework used.

---

# Scope

This RFC defines:

* Repository layout
* Reserved directories
* Reserved files
* Naming rules

This RFC does not define:

* Object formats
* Commit structure
* Snapshot structure
* Validation rules

These are covered by separate RFCs.

---

# Repository Root

Every AISpec repository contains a single root directory.

Example:

```text
my-project/

├── aispec.yaml
├── nodes/
├── flows/
├── branches/
├── commits/
├── snapshots/
├── evaluations/
├── environments/
├── policies/
├── connectors/
├── artifacts/
├── extensions/
└── .aispec/
```

---

# Root Manifest

Every repository MUST contain:

```text
aispec.yaml
```

This file identifies the repository.

It stores project-level metadata.

It MUST NOT contain version history.

---

# Reserved Directories

## nodes/

Stores Node definitions.

Each Node SHOULD be stored independently.

---

## flows/

Stores Flow definitions.

Flows describe relationships between Nodes.

---

## branches/

Stores Branch metadata.

History belongs to Commits.

---

## commits/

Stores immutable Commit objects.

Each Commit is stored as an independent document.

---

## snapshots/

Stores immutable Snapshots.

Snapshots represent the complete state of a Node.

---

## evaluations/

Stores benchmark executions and evaluation results.

Evaluations MUST NOT modify Snapshots.

---

## environments/

Stores deployment environments.

Examples:

* development
* testing
* staging
* production

---

## policies/

Stores governance rules.

Examples:

* approval rules
* security policies
* deployment restrictions

---

## connectors/

Stores references to external systems.

Examples:

* databases
* APIs
* queues
* storage providers

---

## artifacts/

Stores versioned assets.

Examples:

* prompts
* templates
* datasets
* images
* documents

---

## extensions/

Stores optional extensions.

Extensions MUST NOT modify the core specification.

---

## .aispec/

Reserved internal directory.

Implementations MAY store:

* indexes
* cache
* temporary files
* local metadata

Contents of this directory are not part of the specification.

---

# Naming Rules

Directory names are case-sensitive.

Reserved names MUST NOT be reused for other purposes.

Implementations MAY create additional directories.

Unknown directories MUST be ignored.

---

# Repository Rules

An AISpec repository MUST contain exactly one:

* aispec.yaml

Repository objects SHOULD exist only once.

Objects SHOULD reference one another using immutable identifiers.

History MUST be append-only.

---

# Compatibility

Future versions MAY introduce additional reserved directories.

Existing reserved directory names MUST remain stable.

Unknown directories MUST NOT invalidate a repository.

---

# Security Considerations

Implementations SHOULD ignore executable files located inside repository metadata directories.

Sensitive credentials SHOULD never be stored inside the repository.

Secrets SHOULD be referenced externally.

---

# Future Work

Future RFCs define:

* Commit Format
* Snapshot Format
* Branch Format
* Validation Rules
* Storage Engine

---

# Summary

A standardized repository layout enables interoperability between different AISpec implementations.

Every compliant implementation should be able to recognize, parse, and understand any valid AISpec repository regardless of the implementation language.
