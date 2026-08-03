# AISpec

> **The universal version control standard for AI systems.**

AISpec is an open specification designed to version, compare, and manage AI systems independently of the framework, model, provider, or programming language.

Just as Git became the universal standard for source code versioning, AISpec aims to become the universal standard for AI system versioning.

---

# Vision

Modern AI systems evolve continuously.

Prompts change.

Models are upgraded.

Tools are added.

Workflows become more complex.

Memory strategies evolve.

Despite this, there is currently no universal way to describe, version, compare, and restore an AI system.

AISpec exists to solve that problem.

---

# What AISpec Is

AISpec is an open standard for representing AI systems.

It defines a common language that allows developers and organizations to:

* Version AI systems.
* Compare changes.
* Restore previous versions.
* Track evolution over time.
* Build tooling on top of a shared specification.

AISpec is framework-agnostic, model-agnostic and provider-agnostic.

---

# What AISpec Is Not

AISpec is **not**:

* an LLM provider
* an AI framework
* an orchestration engine
* a workflow builder
* a vector database
* a deployment platform

Instead, AISpec provides the versioning layer that can be used by all of them.

---

# Project Goals

* Define a universal specification for AI systems.
* Enable reproducible AI development.
* Make AI versioning as common as Git versioning.
* Create an ecosystem around an open standard.
* Encourage interoperability across AI tools.

---

# Core Concepts

AISpec is built around a small set of concepts.

* Project
* Node
* Snapshot
* Commit
* Branch
* Merge
* Diff
* Rollback
* Evaluation
* Lineage

These concepts form the foundation of the specification.

---

# Architecture

The project is divided into four major components.

## AISpec

The open specification.

Defines the universal language.

---

## AISpec SDK

Official libraries that allow developers to integrate AISpec into their applications.

---

## AISpec Engine

The reference implementation responsible for storing, comparing and restoring versions.

---

## AISpec Cloud

A hosted platform built on top of AISpec providing collaboration, visualization and enterprise capabilities.

---

# Principles

AISpec follows a small number of immutable principles.

* Open Standard
* Framework Agnostic
* Model Agnostic
* Provider Agnostic
* Language Agnostic
* Version First
* Human Readable
* Extensible by Design

---

# Long-Term Vision

AISpec aims to become the foundational layer for AI version control.

Developers should be able to move AI systems across tools, frameworks and providers while preserving their history, structure and evolution.

AISpec is designed to outlive current AI frameworks and remain relevant as new architectures emerge.

---

# License

Apache License 2.0

---

# Status

**Development Status:** Pre-production

AISpec is currently in the specification phase.

No production implementation exists yet.

The current focus is defining the core concepts and the first version of the specification before any production code is written.

---

# Roadmap

* Specification (AISpec v0.1)
* Reference Engine
* Official SDKs
* CLI
* Cloud Platform
* Enterprise Edition

---

# Contributing

AISpec is an open project.

Contributions, discussions, RFCs and proposals are welcome.

The goal is to build an open standard for the entire AI ecosystem.
