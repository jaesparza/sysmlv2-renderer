---
name: sysmlv2-renderer
description: Render small SysML v2 textual models as semantically faithful structural SVG diagrams. Use when the user provides a SysML v2 model and requests a graphical structural view.
---

# SysML v2 Renderer — initial skill

## Purpose

Transform a user-provided SysML v2 textual model into a structurally faithful SVG diagram. Work incrementally: support only constructs whose semantics and graphical representation can be established from the available sources.

## Authority and evidence

1. Use the OMG SysML v2 specification as the authority for language semantics.
2. Use the user's legally obtained Tim Weilkiens reference as the primary authority for graphical conventions.
3. Do not claim a graphical convention is specified by SysML v2 merely because it appears in a rendering.
4. Distinguish:
   - **Normative semantics** — what the SysML v2 model means.
   - **Reference convention** — graphical notation supported by the Weilkiens reference, with page reference where available.
   - **Rendering decision** — a practical layout or styling choice made by this skill.
5. If the available sources do not establish a convention, label it as unresolved. Do not silently invent notation.
6. Do not reproduce substantial copyrighted text or images from the reference. Record concise, independently written rules and page references.

## Initial supported scope (v0.1)

Target a basic structural view with:
- package / namespace context;
- definition elements;
- usage elements;
- explicit containment or composition only where supported by the source model and understood semantics.

Do not infer missing relationships. Do not yet attempt ports, connectors, interfaces, bindings, behavioral elements, requirements, parametrics, or comprehensive SysML v2 coverage.

## Workflow

### 1. Inspect the input

- Read the complete supplied textual model.
- Identify the relevant package and namespace context.
- Identify each supported definition and usage.
- Identify explicit relationships relevant to the requested structural view.
- Preserve names, typing, multiplicity and other displayed properties exactly where present.
- Do not treat comments, naming similarity or proximity as model relationships.

### 2. Establish semantic traceability

Before drawing, create an internal element/relationship inventory. Every graphical element and connector must map to an element or relationship in the source model.

If syntax or semantics are unclear:
- quote the smallest relevant source fragment;
- state the uncertainty;
- ask for clarification if it changes the diagram materially.

### 3. Apply graphical notation

- Apply only conventions supported by the available Weilkiens reference.
- Record the reference page for each convention when known.
- Keep definition and usage representations distinct where the reference establishes a distinction.
- Keep graphical layout decisions separate from semantic meaning.
- Never add decorative symbols that could be mistaken for SysML notation.

If the reference material is unavailable in the current conversation, state that notation-level fidelity has not yet been verified. Produce only a clearly labelled provisional rendering if the user wants to proceed.

### 4. Layout and render

- Generate SVG as the primary output.
- Use consistent typography, spacing, alignment and line routing.
- Keep labels readable and avoid connector crossings where practical.
- Do not let layout convenience change model semantics.
- Use neutral, restrained styling; avoid implying semantic meaning through unsupported colors or shapes.

### 5. Validate

Check:
- every rendered element exists in the source model;
- every rendered relationship exists in the source model;
- no supported source element was unintentionally omitted from the requested view;
- definition/usage distinctions are applied consistently;
- labels and typing are accurate;
- graphical conventions are sourced or explicitly marked as provisional;
- the SVG is well-formed and readable.

Report any omissions, assumptions, unresolved notation questions and rendering decisions.

## Response format

For each rendering task, provide:
1. **Scope** — what part of the model is shown.
2. **Semantic inventory** — concise list of rendered elements and relationships.
3. **Notation status** — sourced conventions versus provisional decisions.
4. **SVG** — complete SVG output, preferably as a standalone artifact when file generation is available.
5. **Validation** — findings and known limitations.

Do not claim full SysML v2 compliance. State the subset actually handled.

## Incremental development rule

When a new construct is requested:
1. determine whether its semantics are understood;
2. identify its graphical convention in the reference;
3. add a minimal test model;
4. render and validate it;
5. only then include it in the supported scope.

Prefer a small, tested capability over broad but unreliable coverage.
