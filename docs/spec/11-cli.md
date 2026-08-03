# 11 — AISpec CLI

---

# Purpose

The AISpec Command Line Interface (CLI) is the primary tool for interacting with AISpec repositories from the terminal.

It provides a simple, consistent, and scriptable interface for creating, managing, validating, and inspecting AISpec projects.

The CLI is built on top of the AISpec Engine.

---

# Philosophy

The CLI should make the most common repository operations fast and intuitive.

Every command should produce deterministic results and remain consistent across operating systems.

The CLI is designed for both individual developers and automation systems.

---

# Design Goals

The AISpec CLI should be:

* Simple
* Fast
* Cross-platform
* Scriptable
* Deterministic
* Easy to automate

---

# Architecture

```text id="s3u9xk"
User

↓

AISpec CLI

↓

AISpec Engine

↓

Repository
```

The CLI never manipulates repository files directly.

All operations are delegated to the Engine.

---

# Repository Commands

Initialize a new repository.

```bash id="v8j4pa"
aispec init
```

Open an existing repository.

```bash id="nnr3r5"
aispec open
```

Validate a repository.

```bash id="24h0hr"
aispec validate
```

Display repository information.

```bash id="qmy4gr"
aispec info
```

---

# Commit Commands

Create a Commit.

```bash id="z7edmb"
aispec commit
```

List repository history.

```bash id="gk7v8u"
aispec log
```

Show Commit details.

```bash id="m7u1dv"
aispec show
```

---

# Snapshot Commands

Create a Snapshot.

```bash id="mn3j3q"
aispec snapshot
```

Compare two Snapshots.

```bash id="pj2wba"
aispec diff
```

Restore a Snapshot.

```bash id="6chd4e"
aispec restore
```

---

# Branch Commands

Create a Branch.

```bash id="m1e3fo"
aispec branch create
```

Switch Branches.

```bash id="rw6s4z"
aispec checkout
```

Merge Branches.

```bash id="jv8mns"
aispec merge
```

List Branches.

```bash id="d4kp9g"
aispec branch list
```

---

# Graph Commands

Display the repository graph.

```bash id="8gvzxe"
aispec graph
```

Export the graph.

```bash id="x8qv2m"
aispec graph export
```

Analyze graph dependencies.

```bash id="9mewnr"
aispec graph analyze
```

---

# Validation Commands

Validate the complete repository.

```bash id="tb3h7d"
aispec validate
```

Validate a specific object.

```bash id="bb6h8q"
aispec validate commit c_001
```

---

# Configuration

The CLI SHOULD support local configuration.

Example:

```yaml id="y9q4cv"
version: 1.0.0

defaultBranch: main

autoValidate: true
```

Configuration files SHOULD remain optional.

---

# Output Formats

The CLI SHOULD support multiple output formats.

Examples:

* Human-readable
* JSON
* YAML

Machine-readable output enables automation and CI/CD integration.

---

# Exit Codes

Commands SHOULD return standard exit codes.

| Exit Code | Meaning              |
| --------- | -------------------- |
| 0         | Success              |
| 1         | General Error        |
| 2         | Validation Error     |
| 3         | Repository Not Found |
| 4         | Invalid Command      |
| 5         | Internal Error       |

---

# Automation

The CLI SHOULD support:

* shell scripts
* CI/CD pipelines
* GitHub Actions
* GitLab CI
* Azure Pipelines
* Jenkins

Every command should behave predictably in automated environments.

---

# Security

The CLI SHOULD:

* validate all user input
* avoid exposing secrets
* never execute repository content
* preserve repository integrity

---

# Compatibility

The CLI MUST remain compatible with the supported AISpec specification version.

Future versions SHOULD preserve backward compatibility whenever possible.

---

# Future Work

Future releases may introduce:

* Interactive Mode
* Repository Wizard
* Live Graph Viewer
* Remote Repository Commands
* Cloud Integration
* Plugin Management
* AI-assisted Repository Analysis

---

# Summary

The AISpec CLI is the primary interface for developers working with AISpec repositories.

It provides a simple, scriptable, and deterministic command-line experience built on top of the AISpec Engine, enabling repository creation, version management, validation, graph inspection, and automation across all supported platforms.
