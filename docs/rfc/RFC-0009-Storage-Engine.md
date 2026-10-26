# RFC-0009 — Storage Engine

**Status:** Draft

**Version:** 0.1

---

# Purpose

This RFC defines the logical storage model used by AISpec.

The Storage Engine is responsible for persisting, indexing, retrieving, and reconstructing repository objects.

This RFC specifies the logical behavior of storage.

It does not mandate a particular database or filesystem implementation.

---

# Philosophy

AISpec repositories should remain:

* Portable
* Human-readable
* Deterministic
* Implementation-independent

The canonical repository is always represented as files.

Indexes and databases are implementation details.

---

# Scope

This RFC defines:

* Canonical storage
* Object persistence
* Object indexing
* Cache behavior
* Hashing
* Repository reconstruction

This RFC does not define:

* Execution engines
* Cloud synchronization
* Replication
* Database implementations

---

# Canonical Storage

The canonical representation of an AISpec repository is the filesystem.

Objects SHOULD be stored as individual YAML documents.

Example:

```text
commits/
    c_001.yaml
    c_002.yaml

snapshots/
    s_001.yaml
    s_002.yaml

nodes/
    router.yaml
    memory.yaml
```

The filesystem is the source of truth.

---

# Object Storage

Every logical object SHOULD be stored independently.

Examples:

* Commit
* Snapshot
* Branch
* Node
* Connector
* Artifact

Objects MUST NOT be embedded inside unrelated objects.

---

# Persistence Synchronization

An SDK that exposes `saveRepository()` MUST complete pending persistence work
and synchronize canonical data according to the storage backend's guarantees
before reporting success, as defined by RFC-0010.

For filesystem-backed storage, this operation MUST synchronize the contents of
all canonical repository files through the operating system's file
synchronization mechanism. This does not guarantee directory-entry metadata,
atomic persistence across multiple files, or durability beyond the guarantees
of the operating system, filesystem, and hardware. Synchronizing files may
partially succeed before a later synchronization fails; implementations MUST
report the failure and MUST NOT claim that the repository was fully saved.

An implementation MAY persist mutations immediately. In that case,
`saveRepository()` remains an explicit synchronization barrier and MUST NOT
create or alter logical repository objects.

---

# Serialization

The canonical serialization format is YAML.

Implementations MAY additionally support:

* JSON
* Binary
* SQLite
* LMDB

The logical content MUST remain equivalent.

---

# Repository Reconstruction

A repository MUST be reconstructable using only its canonical files.

No cache, database, or index may be required to restore the complete repository.

---

# Indexes

Implementations MAY generate indexes.

Indexes exist solely to improve performance.

Examples:

* Commit index
* Branch index
* Snapshot index
* Dependency index
* Graph index

Indexes MUST be disposable.

Deleting indexes MUST NOT corrupt the repository.

---

# Cache

Implementations MAY maintain cache files.

Caches SHOULD accelerate:

* parsing
* searching
* graph traversal
* validation

Caches MUST NOT become the source of truth.

---

# Hashing

Objects SHOULD be hashable.

Hashes MAY be used for:

* integrity verification
* deduplication
* change detection
* synchronization

The specification does not mandate a specific hashing algorithm.

---

# Compression

Repositories MAY compress stored objects.

Compression MUST remain transparent to users.

Compressed repositories MUST preserve logical equivalence.

---

# Repository Integrity

The Storage Engine SHOULD detect:

* corrupted objects
* missing files
* invalid hashes
* duplicate identifiers
* inconsistent references

Integrity failures SHOULD be reported during validation.

---

# Performance

Implementations SHOULD optimize:

* repository loading
* Commit lookup
* Snapshot retrieval
* graph traversal
* history reconstruction

Performance optimizations MUST NOT change repository behavior.

---

# Scalability

AISpec repositories SHOULD support:

* small personal projects
* enterprise repositories
* distributed development
* millions of objects

Storage implementations SHOULD scale without changing repository semantics.

---

# Validation Rules

A valid Storage Engine MUST:

* preserve every object
* preserve object identifiers
* preserve object relationships
* reconstruct the repository without information loss

Indexes and caches MUST NOT affect repository validity.

---

# Compatibility

Future implementations MAY introduce:

* object databases
* distributed storage
* cloud-native storage
* remote repositories

Canonical repository behavior MUST remain unchanged.

---

# Security Considerations

Storage engines SHOULD:

* protect against file corruption
* detect tampering
* validate object integrity
* avoid storing secrets in canonical objects

Credentials SHOULD remain external to the repository.

---

# Future Work

Future RFCs may define:

* Distributed Storage
* Incremental Synchronization
* Remote Repositories
* Object Deduplication
* Content Addressable Storage
* Storage Encryption

---

# Summary

The AISpec Storage Engine defines a portable, deterministic, and implementation-independent storage model.

Canonical repositories are always represented as human-readable files, while indexes, caches, and databases remain optional implementation details. This separation guarantees long-term interoperability, portability, and reproducibility across all AISpec implementations.
