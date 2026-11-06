# SysML v2 Renderer

A reusable, incrementally developed capability for rendering SysML v2 textual models as structurally faithful diagrams.

## Initial objective

Given a small SysML v2 textual model, generate a readable SVG structural view while preserving the model's semantics.

## Development principles

- Start with the smallest useful, testable capability.
- Keep semantic interpretation separate from graphical layout.
- Use the OMG SysML v2 specification for language semantics.
- Use Tim Weilkiens' uploaded reference as the primary source for graphical conventions.
- Document notation rules in original wording, with page references; do not redistribute the book.
- Mark unsupported or ambiguous conventions explicitly rather than inventing notation.
- Expand scope only after the current increment has been tested.

## Version 0.1 scope

- Input: a small SysML v2 textual model supplied in a ChatGPT conversation.
- View: a basic structural view (BDD-equivalent intent).
- Elements: package/namespace, definitions, usages, and explicitly modelled containment where supported by the source.
- Output: SVG.
- Validation: check that rendered elements and relationships are traceable to the input model.

Version 0.1 does not attempt comprehensive SysML v2 coverage, interconnection views, ports, connectors, behavioral views, or automated parsing.

## Repository structure

- `SKILL.md`: initial reusable rendering instructions.
- `references/`: sourced notation rules and semantic mapping notes.
- `tests/`: small input models and expected rendering characteristics.
- `docs/`: workflow and development notes.

## Current status

Initial baseline. The first milestone is to test whether the skill can produce a semantically faithful SVG for a deliberately small structural model.

## Copyright and references

The repository must not contain a copy of the copyrighted reference book. Record concise, independently written notation rules and cite relevant page numbers. Verify permissions before publishing any substantial derived material.
