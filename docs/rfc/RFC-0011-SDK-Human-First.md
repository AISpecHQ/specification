# RFC: Human-First

**Status:** Proposed
**Date:** 2026-08-13
**Scope:** Product / Data Model / Provenance

## Summary

AISpec treats AI as a tool within a human-directed workflow.

The system should preserve information about human contribution alongside AI operations, so that the history of a result does not reduce the work to a sequence of model calls.

AISpec should make it possible to understand:

> **Who contributed, what they contributed, what AI contributed, and how the final result was produced.**

## Motivation

AI-assisted workflows increasingly combine human decisions with automated generation, transformation, and evaluation.

Traditional AI tooling tends to focus primarily on the model:

* model
* prompt
* parameters
* output
* cost
* version

This provides technical reproducibility but can lose the human context behind the work.

AISpec should preserve both sides of the workflow.

The goal is not to prevent AI automation. The goal is to make AI-assisted work **attributable, traceable, and human-directed**.

## Principles

### 1. AI is a tool

AISpec does not assume that automation should replace human contributors.

AI operations should be represented as part of a larger workflow rather than as the sole source of authorship.

### 2. Human contribution is first-class metadata

Human participation should be recordable at the same level of importance as model and execution metadata.

A contribution may include:

* person
* role
* action
* timestamp
* relationship to a version or result

Example roles include:

* Creative Director
* Designer
* Editor
* Developer
* Researcher
* Reviewer
* Approver

### 3. AI contribution is explicit

AISpec should distinguish between human contribution and AI contribution.

AI contribution may include:

* model/provider
* model version
* prompt
* generation or transformation
* parameters
* output
* execution metadata

### 4. Provenance is preserved

A result should be traceable through the sequence of inputs, transformations, human decisions, AI operations, and versions that produced it.

Provenance answers:

> Where did this result come from?

### 5. Attribution is not a legal claim

AISpec should use terms such as:

* attribution
* contribution
* provenance
* authorship context
* traceability

AISpec should not claim that its metadata establishes legal copyright ownership.

## Data Model

Human-First information should initially be implemented as metadata associated with existing AISpec objects, particularly `Snapshot`, `Version`, and `Result`.

Conceptually:

```text
Snapshot
├── Human Contribution
│   ├── contributor
│   ├── role
│   └── action
│
├── AI Contribution
│   ├── provider
│   ├── model
│   ├── prompt
│   └── operation
│
├── Provenance
│   ├── source
│   ├── transformations
│   └── parent versions
│
└── Approvals
    ├── approver
    ├── status
    └── timestamp
```

This does not require a new top-level AISpec object.

## Example

A generated campaign image could contain:

```text
Human Contribution
Creative Director
Directed generation and selected final variation.

AI Contribution
Image Model
Generated initial visual variations from the provided prompt.

Human Contribution
Editor
Retouched the selected image and prepared the final asset.

Approval
Creative Director
Approved version v12.
```

The resulting history communicates not simply:

```text
Prompt → Model → Image
```

but:

```text
Human direction
      ↓
AI generation
      ↓
Human selection/editing
      ↓
Human approval
      ↓
Final result
```

## Product Implications

The existing AISpec workflow remains valid:

```text
Prompt
→ Version
→ Experiment
→ Model Provider
→ Result
→ Cost
→ Merge / Rollback
```

Human-First extends this workflow with attribution and provenance metadata rather than replacing the existing model.

The conceptual workflow becomes:

```text
Human Contribution
        ↓
Prompt / Experiment
        ↓
AI Contribution
        ↓
Result
        ↓
Human Review / Approval
        ↓
Version
```

## UI Principles

The product should make human contribution visible without making the interface unnecessarily complex.

A result should be able to answer:

* Who worked on this?
* What role did they have?
* What did AI do?
* Which model was used?
* What changed between versions?
* Who approved the result?
* Where did the underlying asset originate?

Human contribution should not be hidden in a secondary administrative interface.

## Non-Goals

Human-First does not attempt to:

* determine legal copyright ownership
* determine whether AI-generated work is legally protected
* prevent companies from using AI
* prohibit automation
* judge whether a workflow contains “too much” AI
* replace existing versioning or experiment tracking

AISpec provides the infrastructure for transparency and attribution.

## Long-Term Direction

AISpec should enable organizations to define their own policies around human involvement.

Future policy capabilities may include:

* required human approval
* required contributor attribution
* restricted AI operations
* consent requirements
* provenance requirements
* organization-specific human-in-the-loop policies

The underlying principle remains:

> **AI can participate in the work without making the human contribution invisible.**

## Decision

Adopt **Human-First** as a product principle and extend AISpec's existing metadata model to support human contribution, AI contribution, provenance, and approvals.

No new top-level object is required at this stage.

Implementation should begin with metadata and evolve based on real usage.
