# RFC-0007 — Extension System

**Status:** Draft

**Version:** 0.1

---

# Purpose

This RFC defines the Extension System for AISpec.

Extensions allow implementations to introduce new capabilities without modifying or breaking the core specification.

The Extension System ensures that AISpec remains stable while allowing the ecosystem to evolve.

---

# Philosophy

The core specification should remain small.

Not every feature belongs in the standard.

AISpec defines only the universal foundation.

Everything else should be implemented as an extension.

---

# Scope

This RFC defines:

* Extension architecture
* Extension discovery
* Namespaces
* Compatibility rules
* Extension metadata

This RFC does not define:

* Specific extensions
* Execution behavior
* Plugin marketplaces
* Runtime loading

---

# Extension Overview

An Extension adds optional functionality to an AISpec repository.

Extensions never modify the meaning of the core specification.

Repositories remain valid even if an implementation does not recognize an Extension.

---

# Extension Object

Every Extension SHOULD define:

```yaml
id:
name:
namespace:
version:
author:
description:
entrypoint:
metadata:
```

---

# Definitions

## id

Globally unique identifier.

Example

```text
ext.memory.redis
```

---

## name

Human-readable name.

Example

```text
Redis Memory Extension
```

---

## namespace

Namespaces prevent collisions.

Examples

```text
org.aispec

com.company

io.openai

dev.manuel
```

Extensions SHOULD always belong to a namespace.

---

## version

Semantic Version of the Extension.

Example

```text
1.2.0
```

---

## author

Extension author.

May represent:

* Individual
* Company
* Organization
* Community

---

## description

Human-readable explanation.

---

## entrypoint

Optional implementation entrypoint.

The specification does not define its format.

---

## metadata

Optional implementation-specific information.

Unknown metadata MUST be ignored.

---

# Extension Discovery

Implementations SHOULD automatically discover Extensions.

Repositories MAY declare required Extensions.

Unknown Extensions MUST NOT invalidate a repository.

---

# Compatibility

Extensions MUST remain compatible with the AISpec version they target.

An Extension MUST declare the minimum AISpec version it supports.

Example

```yaml
requires:
  aispec: ">=1.0.0"
```

---

# Isolation

Extensions MUST remain isolated from the core specification.

They MUST NOT:

* redefine Commit behavior
* redefine Snapshot behavior
* redefine validation rules
* modify repository history

Extensions MAY introduce additional objects.

---

# Namespaces

Namespaces MUST be globally unique.

Examples

```text
org.aispec.memory

com.company.monitoring

dev.manuel.analytics
```

Namespaces prevent identifier conflicts across implementations.

---

# Extension Lifecycle

Typical lifecycle:

```text
Install

↓

Discover

↓

Validate

↓

Load

↓

Use

↓

Update

↓

Remove
```

Removing an Extension MUST NOT corrupt repository history.

---

# Validation Rules

A valid Extension MUST:

* contain an ID
* contain a namespace
* declare a version
* avoid identifier collisions

Unknown Extensions MUST be ignored.

Invalid Extensions MUST NOT invalidate the core repository.

---

# Serialization

Extensions SHOULD be serialized as YAML.

Alternative internal formats MAY be used.

The logical Extension object MUST remain equivalent.

---

# Security Considerations

Extensions execute outside the scope of the AISpec specification.

Implementations SHOULD:

* isolate Extension execution
* validate Extension metadata
* restrict privileged operations
* avoid automatic trust

Extensions SHOULD request only the permissions they require.

---

# Compatibility

Future versions MAY introduce:

* Extension registries
* Dependency resolution
* Capability negotiation
* Signed Extensions

Existing Extensions SHOULD remain compatible whenever possible.

---

# Future Work

Future RFCs may define:

* Official Extension Registry
* Package Distribution
* Extension Signing
* Capability Discovery
* Dependency Management

---

# Summary

The Extension System allows AISpec to evolve without increasing the complexity of the core specification.

By isolating optional functionality behind stable interfaces and namespaces, AISpec remains minimal, portable, and extensible while supporting a growing ecosystem of tools and integrations.
