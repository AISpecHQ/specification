# RFC-0002 — Commit Format

**Status:** Draft

**Version:** 0.1

---

# Purpose

This RFC defines the canonical structure of a Commit in AISpec.

A Commit records an immutable change in an AISpec repository.

Commits form the complete history of a project.

---

# Philosophy

A Commit represents a point in history.

It describes **what changed**, not the current state.

The current state is represented by Snapshots.

Commits are immutable.

Once created, they MUST never change.

---

# Scope

This RFC defines:

* Commit structure
* Required fields
* Parent relationships
* Merge commits
* Serialization
* Immutability rules

This RFC does not define:

* Snapshot contents
* Branch behavior
* Repository validation
* Storage implementation

---

# Commit Object

Every Commit MUST contain the following fields.

```yaml
id:
parents:
branch:
author:
timestamp:
message:
snapshotIds:
tags:
metadata:
```

---

# Definitions

## id

A globally unique immutable identifier.

Each Commit MUST have exactly one ID.

Example:

```text
c_8fd12ac93
```

---

## parents

References one or more parent Commits.

The first Commit has no parent.

Merge Commits MAY reference multiple parents.

Example:

```yaml
parents:
  - c_a9213
  - c_45ff2
```

---

## branch

The Branch where the Commit belongs.

Example:

```text
main
```

---

## author

Identifies who created the Commit.

The author MAY be:

* Human
* System
* Automation
* AI Agent

Example:

```text
manuel
```

---

## timestamp

Creation time.

MUST use ISO-8601 UTC.

Example:

```text
2026-08-02T14:25:16Z
```

---

## message

Human-readable description.

Examples:

```text
Initial Commit

Replace GPT-5 with Claude Sonnet

Improve Router Node

Update Evaluation Pipeline
```

---

## snapshotIds

References every Snapshot created by this Commit.

Example:

```yaml
snapshotIds:
  - s_7812
  - s_9183
```

---

## tags

Optional labels.

Examples:

* stable
* production
* release
* experimental

---

## metadata

Optional implementation-specific information.

Unknown metadata MUST be ignored.

---

# Commit Lifecycle

A typical Commit lifecycle is:

```text
Workspace

↓

Changes

↓

Snapshot

↓

Commit

↓

History
```

---

# Commit Types

AISpec does not define fixed Commit types.

Implementations MAY classify Commits.

Examples:

* Feature
* Fix
* Release
* Merge
* Migration

These classifications are informational only.

---

# Merge Commits

Merge Commits combine multiple histories.

A Merge Commit MUST reference more than one parent.

Example:

```yaml
parents:
  - c_101
  - c_204
```

---

# Immutability

Commits are immutable.

After creation:

* IDs MUST NOT change.
* Parents MUST NOT change.
* Messages SHOULD NOT change.
* Snapshot references MUST NOT change.

A modified Commit is considered a different Commit.

---

# Serialization

Commits SHOULD be stored as YAML.

JSON MAY be supported.

Alternative representations MAY exist internally.

The logical Commit object MUST remain equivalent.

---

# Validation Rules

A valid Commit MUST:

* contain an ID
* belong to exactly one Branch
* contain a timestamp
* reference valid Snapshots
* have unique identifiers

Merge Commits MUST reference at least two parents.

---

# Compatibility

Future versions MAY introduce optional fields.

Existing required fields MUST remain compatible.

Unknown optional fields MUST be ignored.

---

# Security Considerations

Commit metadata SHOULD NOT contain secrets.

Credentials MUST be referenced externally.

Sensitive information SHOULD NOT be stored in Commit messages.

---

# Future Work

Future RFCs define:

* Snapshot Format
* Branch Format
* Graph Model
* Validation Rules

---

# Summary

A Commit is the immutable historical record of an AISpec repository.

Commits provide traceability, reproducibility, and collaboration while remaining independent of any execution engine or AI provider.
