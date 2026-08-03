# RFC-0003 — Snapshot Format

**Status:** Draft

**Version:** 0.1

---

# Purpose

This RFC defines the canonical structure of a Snapshot in AISpec.

A Snapshot represents the complete immutable state of an object at a specific point in time.

Snapshots are the source of truth for reproducibility.

---

# Philosophy

A Snapshot captures state.

Unlike a Commit, which records history, a Snapshot records the exact configuration of an object.

Every Snapshot is immutable.

Once created, it MUST never change.

---

# Scope

This RFC defines:

* Snapshot structure
* Required fields
* Object references
* Serialization
* Immutability rules

This RFC does not define:

* Commit history
* Branch behavior
* Storage implementation
* Repository validation

---

# Snapshot Object

Every Snapshot MUST contain the following fields.

```yaml
id:
nodeId:
version:
createdAt:
configuration:
capabilities:
connectors:
artifacts:
metadata:
```

---

# Definitions

## id

A globally unique immutable identifier.

Each Snapshot MUST have exactly one ID.

Example:

```text
s_91ab82
```

---

## nodeId

References the Node represented by this Snapshot.

Each Snapshot belongs to exactly one Node.

Example:

```text
router-node
```

---

## version

Represents the version of the Node.

Versions SHOULD increase monotonically.

Example:

```text
17
```

---

## createdAt

Creation timestamp.

MUST use ISO-8601 UTC.

Example:

```text
2026-08-02T16:42:11Z
```

---

## configuration

Stores every configurable property required to reproduce the Node.

Examples include:

* model
* prompt
* temperature
* timeout
* retry policy
* memory configuration

The specification does not restrict configuration keys.

---

## capabilities

Declares the capabilities supported by this Snapshot.

Examples:

```yaml
capabilities:
  - text-generation
  - web-search
  - memory
```

---

## connectors

References external systems used by the Node.

Examples:

* PostgreSQL
* Redis
* Slack
* Gmail
* S3

Connectors describe dependencies.

They do not store credentials.

---

## artifacts

References versioned assets required by the Snapshot.

Examples:

* prompts
* templates
* datasets
* images
* documents
* workflows

Artifacts are immutable references.

---

## metadata

Optional implementation-specific information.

Unknown metadata MUST be ignored.

---

# Snapshot Lifecycle

A Snapshot follows this lifecycle:

```text
Workspace

↓

Edit

↓

Snapshot

↓

Commit

↓

Evaluation

↓

Release
```

Snapshots may exist before they are committed.

---

# Immutability

Snapshots are immutable.

After creation:

* IDs MUST NOT change.
* Configuration MUST NOT change.
* Connectors MUST NOT change.
* Artifacts MUST NOT change.

A modified Snapshot becomes a new Snapshot.

---

# Relationships

A Snapshot:

* belongs to one Node
* may be referenced by many Commits
* may be evaluated multiple times
* never stores history

History belongs to Commits.

---

# Serialization

Snapshots SHOULD be stored as YAML.

JSON MAY be supported.

Alternative internal formats are allowed.

The logical Snapshot MUST remain identical.

---

# Validation Rules

A valid Snapshot MUST:

* contain an ID
* reference one Node
* contain a version
* contain a creation timestamp
* contain valid configuration

Referenced Artifacts and Connectors SHOULD exist.

---

# Compatibility

Future versions MAY introduce optional fields.

Existing required fields MUST remain compatible.

Unknown optional fields MUST be ignored.

---

# Security Considerations

Snapshots SHOULD NOT contain secrets.

Credentials MUST be stored externally.

Sensitive configuration SHOULD be referenced, not embedded.

---

# Future Work

Future RFCs define:

* Branch Format
* Graph Model
* Validation Rules
* Storage Engine

---

# Summary

A Snapshot represents the complete immutable state of a Node at a specific moment.

Snapshots enable reproducibility, portability, comparison, auditing, and deterministic execution across different AISpec implementations.
