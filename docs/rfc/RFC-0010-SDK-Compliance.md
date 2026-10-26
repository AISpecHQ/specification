# RFC-0010 — SDK Compliance

**Status:** Draft

**Version:** 0.1

---

# Purpose

This RFC defines the minimum requirements for a Software Development Kit (SDK) to be considered AISpec compliant.

A compliant SDK provides a consistent interface for creating, reading, validating, and manipulating AISpec repositories across programming languages.

---

# Philosophy

AISpec is language-independent.

Developers should be able to use the specification from any programming language while obtaining identical behavior.

SDKs are the bridge between applications and the AISpec specification.

Consistency is more important than implementation details.

---

# Scope

This RFC defines:

* Compliance requirements
* Required interfaces
* Required operations
* Validation behavior
* Compatibility requirements

This RFC does not define:

* Internal architecture
* Performance
* Programming language
* Package management

---

# Compliance Levels

AISpec defines three SDK compliance levels.

## Core

Supports reading and writing AISpec repositories.

Required for all SDKs.

---

## Standard

Supports validation, graph navigation, and repository manipulation.

Recommended for production use.

---

## Full

Supports every published AISpec RFC and optional extensions.

May include additional developer tooling.

---

# Required Operations

Every compliant SDK MUST implement the following operations.

## Repository

* createRepository()
* openRepository()
* saveRepository()

### `saveRepository()` contract

`saveRepository()` takes no arguments. It MUST complete any pending persistence
work and return successfully only after the repository's canonical data has
been synchronized using the guarantees available from its storage backend.
Implementations MUST report storage or synchronization failures and MUST NOT
report success after a failed synchronization.

The operation MUST NOT change the repository's logical contents. Repeating it
without intervening changes MUST be safe and MUST NOT create additional
repository objects. A failure may occur after some files have already been
synchronized; `saveRepository()` is not a multi-object transaction and does
not roll back successful earlier writes.

For filesystem-backed implementations, canonical repository files MUST be
flushed through the operating system's file synchronization mechanism before
the operation returns. This guarantees that file contents have been handed to
the operating system's storage layer, subject to the guarantees of the
operating system, filesystem, and hardware. It does not independently
guarantee directory-entry metadata, atomic persistence across multiple files,
or survival of hardware or power failure.

This contract resolves an ambiguity in the original required-operation list.
It does not require deferred writes or an in-memory dirty buffer. Engines that
persist each mutation immediately still provide `saveRepository()` as an
explicit synchronization barrier.

---

## Commit

* createCommit()
* getCommit()
* listCommits()

---

## Snapshot

* createSnapshot()
* getSnapshot()
* listSnapshots()

---

## Branch

* createBranch()
* getBranch()
* listBranches()
* mergeBranches()

---

## Validation

* validateRepository()
* validateObject()

---

## Graph

* getNode()
* getChildren()
* getParents()
* traverse()

---

# Error Handling

SDKs SHOULD expose deterministic error messages.

Errors SHOULD include:

* error code
* description
* affected object
* suggested action (optional)

Unknown repository objects MUST NOT crash the SDK.

---

# Serialization

SDKs MUST support the canonical YAML representation.

JSON support is RECOMMENDED.

Additional formats MAY be supported.

Serialization MUST preserve repository semantics.

---

# Compatibility

A compliant SDK MUST declare:

* supported AISpec version
* SDK version

Example:

```yaml id="s9w2de"
sdk:
  name: aispec-python
  version: 1.0.0

supports:
  aispec: 1.0.0
```

---

# Validation Behavior

SDK validation MUST follow the Validation Rules defined by RFC-0005.

Validation results SHOULD be deterministic.

Different SDK implementations SHOULD produce equivalent validation results.

---

# Object Integrity

SDKs MUST preserve:

* object identifiers
* references
* timestamps
* history
* graph relationships

SDKs MUST NOT silently modify repository contents.

---

# Extension Support

SDKs MAY support Extensions.

Unsupported Extensions MUST be ignored unless explicitly required by the repository.

Extensions MUST NOT alter core SDK behavior.

---

# Testing

Every compliant SDK SHOULD provide automated tests covering:

* repository creation
* commit creation
* snapshot creation
* branch operations
* validation
* graph traversal
* serialization

Official compliance tests MAY be published by the AISpec project.

---

# Certification

Future AISpec releases MAY define an official compliance certification.

Certified SDKs SHOULD pass the official compliance test suite without modification.

Certification ensures interoperability across implementations.

---

# Security Considerations

SDKs SHOULD:

* validate all input
* reject malformed repositories
* avoid executing repository content
* protect against path traversal attacks
* preserve object integrity

Security behavior SHOULD remain consistent across implementations.

---

# Future Work

Future RFCs may define:

* Official Compliance Test Suite
* SDK Benchmark Suite
* Performance Profiles
* Streaming APIs
* Remote Repository APIs
* Language-specific Best Practices

---

# Summary

The SDK Compliance specification guarantees that every AISpec SDK behaves consistently regardless of programming language or implementation.

By defining a common set of interfaces, validation rules, and compatibility requirements, AISpec enables developers to build interoperable tools that share the same repositories, history, and graph model across the entire ecosystem.
