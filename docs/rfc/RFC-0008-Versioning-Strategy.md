# RFC-0008 — Versioning Strategy

**Status:** Draft

**Version:** 0.1

---

# Purpose

This RFC defines how AISpec evolves over time while preserving compatibility across repositories, SDKs, implementations, and tooling.

A predictable versioning strategy ensures long-term stability and interoperability.

---

# Philosophy

AISpec is designed to become foundational infrastructure.

Stability is more valuable than rapid change.

Breaking changes should be extremely rare.

Repositories created today should remain usable for many years.

---

# Scope

This RFC defines:

* Specification versioning
* Repository versioning
* Compatibility guarantees
* Deprecation policy
* Migration strategy

This RFC does not define:

* Application versions
* AI model versions
* Extension versions
* Git versioning

---

# Semantic Versioning

AISpec follows Semantic Versioning.

Format:

```text id="bqm8rh"
MAJOR.MINOR.PATCH
```

Example:

```text id="5udqbf"
1.0.0
```

---

# Major Version

A Major version introduces breaking changes.

Examples:

* incompatible object format
* removed required fields
* incompatible validation rules

Major releases SHOULD be rare.

---

# Minor Version

A Minor version introduces new functionality without breaking compatibility.

Examples:

* optional fields
* new object types
* additional capabilities
* new RFCs

Repositories SHOULD remain compatible.

---

# Patch Version

A Patch version fixes errors.

Examples:

* documentation improvements
* clarification
* typo corrections
* schema corrections

Patch releases MUST NOT change behavior.

---

# Repository Version

Every repository MUST declare the AISpec version it targets.

Example:

```yaml id="n9mlvl"
aispec:
  version: 1.0.0
```

Implementations MUST use this version during validation.

---

# Compatibility Policy

Implementations SHOULD support older repositories whenever possible.

Repositories MUST declare only one AISpec version.

Future implementations MAY support multiple specification versions simultaneously.

---

# Backward Compatibility

Backward compatibility has priority.

Minor and Patch releases SHOULD preserve existing repositories.

Breaking compatibility requires a Major release.

---

# Forward Compatibility

Implementations SHOULD ignore unknown optional fields.

Unknown required fields MAY invalidate a repository.

Future repositories SHOULD degrade gracefully on older implementations.

---

# Deprecation

Deprecated features SHOULD remain supported for at least one Major release.

Deprecated behavior SHOULD generate warnings.

Deprecated features MUST be documented.

Removal MUST occur only in a future Major version.

---

# Migration

Migration paths SHOULD be documented before introducing breaking changes.

Automatic migration tools MAY be provided.

Repositories SHOULD migrate without losing history.

---

# Extension Compatibility

Extensions MUST declare:

* supported AISpec version
* Extension version

Example:

```yaml id="r1it5g"
requires:
  aispec: ">=1.0.0"
```

Implementations MAY refuse incompatible Extensions.

---

# SDK Compatibility

SDKs SHOULD support multiple Minor versions.

SDK maintainers SHOULD clearly document supported specification versions.

---

# Validation Rules

A valid repository MUST:

* declare an AISpec version
* follow Semantic Versioning
* target an existing specification version

Invalid version identifiers MUST invalidate the repository.

---

# Compatibility Matrix

Example:

```text id="2d8ndt"
AISpec 1.0
├── SDK 1.x
├── CLI 1.x
├── Engine 1.x
└── Cloud 1.x
```

Major versions define compatibility boundaries.

---

# Security Considerations

Version negotiation MUST NOT modify repository contents.

Automatic upgrades SHOULD require explicit user approval.

Implementations SHOULD warn before opening unsupported repositories.

---

# Future Work

Future RFCs may define:

* Long-Term Support (LTS)
* Compatibility Profiles
* Enterprise Releases
* Automatic Migration Framework
* Version Negotiation Protocol

---

# Summary

AISpec adopts Semantic Versioning to provide a stable foundation for long-lived AI repositories.

By prioritizing backward compatibility and controlled evolution, AISpec enables repositories, SDKs, Engines, and future implementations to evolve independently while remaining interoperable across the ecosystem.
