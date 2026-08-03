# RFC-0005 — Validation Rules

**Status:** Draft

**Version:** 0.1

---

# Purpose

This RFC defines the validation rules for AISpec repositories.

Validation ensures that every compliant repository is structurally correct, internally consistent, and portable across implementations.

---

# Philosophy

AISpec prioritizes deterministic behavior.

A valid repository should produce the same logical interpretation regardless of the implementation, operating system, or programming language.

Validation guarantees interoperability.

---

# Scope

This RFC defines:

* Repository validation
* Object validation
* Reference validation
* Schema validation
* Error severity

This RFC does not define:

* Object formats
* Storage engines
* Execution behavior
* Performance requirements

---

# Validation Levels

AISpec defines three validation levels.

## Error

An Error invalidates the repository.

The implementation MUST reject invalid objects.

Example:

* Missing Commit ID
* Broken Snapshot reference
* Duplicate object ID

---

## Warning

A Warning indicates a recommended improvement.

Warnings do not invalidate the repository.

Examples:

* Missing description
* Unused Branch
* Empty metadata

---

## Information

Informational messages provide implementation guidance.

They never affect validity.

---

# Repository Validation

A valid repository MUST:

* contain one `aispec.yaml`
* follow the Repository Layout specification
* contain unique object identifiers
* use valid object references
* contain no corrupted objects

---

# Commit Validation

Every Commit MUST:

* contain an ID
* contain a timestamp
* belong to exactly one Branch
* reference valid Snapshots
* contain valid parent references

Merge Commits MUST reference at least two parent Commits.

---

# Snapshot Validation

Every Snapshot MUST:

* contain an ID
* reference exactly one Node
* contain a valid version
* contain a creation timestamp

Configuration MUST be syntactically valid.

---

# Branch Validation

Every Branch MUST:

* contain a unique ID
* contain a unique name
* reference an existing HEAD Commit

Parent Branches, when specified, MUST exist.

---

# Reference Validation

Every object reference MUST resolve successfully.

Broken references invalidate the repository.

Examples:

* Missing Snapshot
* Missing Commit
* Missing Node
* Missing Connector

---

# Identifier Validation

Object identifiers MUST be unique within the repository.

Duplicate identifiers are invalid.

Reserved identifiers MUST NOT be reused.

---

# Schema Validation

Every object MUST conform to its corresponding schema.

Implementations SHOULD validate against the published AISpec schemas.

Unknown optional fields MUST be ignored.

Unknown required fields invalidate the object.

---

# Graph Validation

The repository graph SHOULD remain connected where appropriate.

Invalid graph structures include:

* orphaned objects
* invalid references
* impossible relationships

Cycles MAY exist only where explicitly permitted by future RFCs.

---

# Extension Validation

Extensions MUST NOT modify the behavior of the core specification.

Unknown extensions MUST be ignored.

Extension failures MUST NOT invalidate the core repository.

---

# Validation Process

A compliant validator SHOULD perform validation in the following order:

```text
Repository
    ↓
Schema
    ↓
Objects
    ↓
References
    ↓
Graph
    ↓
Extensions
```

Validation SHOULD stop only on unrecoverable errors.

---

# Compatibility

Future RFCs MAY introduce additional validation rules.

Existing valid repositories SHOULD remain valid whenever possible.

---

# Security Considerations

Validators MUST NOT execute repository content.

Validation is a read-only operation.

External resources SHOULD NOT be accessed during validation unless explicitly requested.

---

# Future Work

Future RFCs may define:

* Performance validation
* Security policy validation
* Cloud validation
* Enterprise compliance profiles

---

# Summary

Validation guarantees that every AISpec repository is structurally correct, internally consistent, and interoperable.

A compliant implementation should produce the same validation result for the same repository, regardless of language or platform.
