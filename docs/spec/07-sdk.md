# 07 — AISpec SDK

---

# Purpose

The AISpec SDK provides language-specific libraries that allow developers to integrate AISpec into their applications.

The SDK exposes a consistent programming interface while delegating repository management to the AISpec Engine.

It is the primary developer-facing component of the AISpec ecosystem.

---

# Philosophy

Developers should not manipulate AISpec repositories manually.

Instead, they interact with a simple, intuitive SDK that abstracts repository operations while preserving the guarantees of the specification.

Every SDK should feel natural in its programming language while remaining behaviorally identical.

---

# Design Goals

The SDK should be:

* Easy to learn
* Consistent
* Lightweight
* Cross-platform
* Language-native
* Fully compliant with AISpec

---

# Architecture

```text id="4df4rf"
Application

↓

AISpec SDK

↓

AISpec API

↓

AISpec Engine

↓

Repository
```

Applications communicate only with the SDK.

The SDK communicates with the Engine.

---

# Official SDKs

AISpec aims to provide official SDKs for major programming languages.

Initial targets include:

* Python
* TypeScript
* Go
* Rust
* Java
* C#
* Swift

Community-maintained SDKs are encouraged.

---

# Responsibilities

The SDK is responsible for:

* Opening repositories
* Creating Commits
* Creating Snapshots
* Managing Branches
* Navigating the Graph
* Running validation
* Serializing objects

The SDK is not responsible for:

* Executing AI models
* Running workflows
* Managing cloud infrastructure
* Providing user interfaces

---

# Core Capabilities

Every official SDK SHOULD support:

## Repository

* Create
* Open
* Save
* Close

---

## Commit

* Create
* Read
* List

---

## Snapshot

* Create
* Read
* Compare

---

## Branch

* Create
* Merge
* Switch
* Delete

---

## Graph

* Traverse
* Search
* Analyze

---

## Validation

* Validate Repository
* Validate Objects
* Validate Graph

---

# Language Independence

Every SDK MUST expose equivalent functionality regardless of programming language.

Syntax may differ.

Behavior MUST remain identical.

---

# Error Model

SDKs SHOULD expose structured exceptions or error objects.

Errors SHOULD include:

* Error code
* Description
* Affected object
* Suggested action (optional)

Applications SHOULD be able to recover from recoverable errors.

---

# Serialization

SDKs MUST support the canonical YAML representation.

JSON SHOULD also be supported.

Additional formats MAY be implemented without affecting compatibility.

---

# Version Compatibility

Every SDK MUST declare:

* SDK version
* Supported AISpec version

Applications SHOULD verify compatibility before interacting with repositories.

---

# Testing

Every SDK SHOULD include automated tests covering:

* Repository creation
* Commit operations
* Snapshot operations
* Branch management
* Validation
* Graph traversal
* Serialization

Compliance tests SHOULD produce identical results across languages.

---

# Distribution

SDKs SHOULD be distributed using the standard package manager for each language.

Examples:

* PyPI
* npm
* Cargo
* Maven
* NuGet
* Swift Package Manager

Installation should follow the conventions of each ecosystem.

---

# Security

SDKs SHOULD:

* validate repository input
* reject malformed objects
* avoid executing repository content
* preserve object integrity

Sensitive information SHOULD remain external to the repository.

---

# Extensibility

SDKs SHOULD support AISpec Extensions whenever possible.

Unsupported Extensions MUST be ignored gracefully unless explicitly required.

---

# Future Work

Future SDK releases may include:

* Async APIs
* Streaming APIs
* Remote Repository APIs
* Plugin APIs
* Enterprise integrations
* IDE extensions

---

# Summary

The AISpec SDK is the primary interface for developers building applications on top of AISpec.

By providing consistent, language-native libraries backed by the AISpec Engine, the SDK enables developers to create interoperable tools without needing to understand the internal repository format or storage implementation.
