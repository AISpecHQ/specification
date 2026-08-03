# RFC-0004 — Branch Format

**Status:** Draft

**Version:** 0.1

---

# Purpose

This RFC defines the canonical representation of Branches in AISpec.

Branches provide isolated lines of development, allowing experimentation, parallel work, and controlled integration without modifying existing history.

---

# Philosophy

Branches represent independent development paths.

They allow multiple ideas to evolve simultaneously while preserving a shared history.

A Branch does not contain data.

A Branch references Commits.

---

# Scope

This RFC defines:

* Branch structure
* Branch metadata
* Parent relationships
* Merge behavior
* Naming rules

This RFC does not define:

* Commit format
* Snapshot format
* Storage implementation
* Repository validation

---

# Branch Object

Every Branch MUST contain the following fields.

```yaml
id:
name:
parent:
head:
createdAt:
author:
description:
tags:
metadata:
```

---

# Definitions

## id

Globally unique immutable identifier.

Example

```text
b_81a92
```

---

## name

Human-readable Branch name.

Examples

```text
main

feature/router

experiment/gpt5

release/v1
```

Names SHOULD be descriptive.

---

## parent

References the Branch from which this Branch originated.

The primary Branch MAY have no parent.

Example

```yaml
parent: main
```

---

## head

References the latest Commit in the Branch.

Example

```yaml
head: c_918ab
```

---

## createdAt

Creation timestamp.

MUST use ISO-8601 UTC.

Example

```text
2026-08-02T18:14:03Z
```

---

## author

Creator of the Branch.

The author MAY be:

* Human
* System
* Automation
* AI Agent

---

## description

Optional human-readable description.

Example

```text
Testing Claude Sonnet against GPT-5.
```

---

## tags

Optional labels.

Examples

* production
* experiment
* release
* archived

---

## metadata

Optional implementation-specific information.

Unknown metadata MUST be ignored.

---

# Branch Lifecycle

Typical lifecycle:

```text
Create

↓

Commits

↓

Experiment

↓

Merge

↓

Archive
```

Deleting a Branch MUST NOT delete its Commits.

---

# Default Branch

Repositories SHOULD contain one default Branch.

The default Branch is typically:

```text
main
```

Implementations MAY use another name.

---

# Merge

A Merge combines the history of two or more Branches.

The resulting Merge Commit references multiple parent Commits.

The source Branch MAY remain available after merging.

---

# Branch Rules

A Branch:

* has one unique ID
* has one HEAD Commit
* references Commit history
* never owns Commits
* may be merged
* may be archived

---

# Naming Rules

Branch names SHOULD:

* be lowercase
* avoid spaces
* use "/" for hierarchy

Examples

```text
feature/auth

feature/memory

experiment/router-v2

release/v1.0
```

---

# Serialization

Branches SHOULD be stored as YAML.

JSON MAY be supported.

Internal implementations MAY use different storage formats.

The logical Branch object MUST remain equivalent.

---

# Validation Rules

A valid Branch MUST:

* contain an ID
* contain a name
* reference an existing HEAD Commit
* avoid duplicate names within the repository

If a parent Branch is specified, it MUST exist.

---

# Compatibility

Future versions MAY introduce optional fields.

Existing required fields MUST remain compatible.

Unknown optional fields MUST be ignored.

---

# Security Considerations

Branches SHOULD NOT contain secrets.

Sensitive information SHOULD remain outside repository metadata.

---

# Future Work

Future RFCs define:

* Validation Rules
* Graph Model
* Storage Engine

---

# Summary

Branches organize independent lines of development while preserving a shared immutable history.

They provide a predictable and portable mechanism for collaboration, experimentation, and release management across all AISpec implementations.
