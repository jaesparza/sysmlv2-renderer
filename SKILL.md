---
name: sysmlv2-renderer
description: Render small SysML v2 textual models as semantically faithful structural SVG diagrams. Use when the user provides a SysML v2 model and requests a graphical structural view.
---

# SysML v2 Renderer — initial skill

## Purpose

Transform a user-provided SysML v2 textual model into a structurally faithful SVG diagram. Work incrementally: support only constructs whose semantics and graphical representation can be established from the available sources.

## Authority and evidence

1. Use the OMG SysML v2 specification as the authority for language semantics.
2. Use the user's legally obtained Tim Weilkiens reference as the primary authority for graphical notation.
3. Use a separately selected visual profile for presentation styling. The active profile in this version is **IBMstyle**, based on the user's supplied SodiusWillert/IBM SysML v2 cheat sheet.
4. Do not claim a graphical convention is specified by SysML v2 merely because it appears in a rendering.
5. Distinguish:
   - **Normative semantics** — what the SysML v2 model means.
   - **Reference convention** — graphical notation supported by the Weilkiens reference, with page reference where available.
   - **Visual style** — appearance choices such as palette, typography, borders and spacing.
   - **Rendering decision** — practical layout or routing choices made for a particular diagram.
6. If the available sources do not establish a convention, label it as unresolved. Do not silently invent notation.
7. Do not reproduce substantial copyrighted text or images from either reference. Keep independently written rules and concise source/page attribution. The supplied SodiusWillert/IBM cheat sheet identifies a CC BY-NC-ND 4.0 licence; do not copy, modify, or redistribute its artwork or page design. Treat IBMstyle as the user's name for a visual target, not as a claim of an official IBM standard.

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
- Represent definitions as rectangles and usages as rounded rectangles, following the definition/usage distinction documented in the Weilkiens reference (consulted pages 90–92; verify the exact example before extending this rule to other element kinds).
- Keep definition and usage representations distinct through their documented geometry, not through arbitrary category tabs or invented group containers.
- Represent usage typing using the documented defined-by relationship/notation when the selected view and reference example call for it.
- Do not add a connector between elements unless a relationship exists in the source model or is a semantically justified, documented derived relationship.
- In particular, do not connect sibling definitions or sibling usages merely because they are displayed beside one another.
- Keep graphical layout decisions separate from semantic meaning.
- Never add decorative symbols that could be mistaken for SysML notation.

If the reference material is unavailable in the current conversation, state that notation-level fidelity has not yet been verified. Produce only a clearly labelled provisional rendering if the user wants to proceed.

### 4. Apply visual style

The default visual profile is **IBMstyle**. Apply it only to visual presentation; it must not change SysML semantics or notation.

IBMstyle characteristics, abstracted as implementation guidance from the user's supplied SodiusWillert/IBM cheat sheet:
- restrained warm-neutral palette;
- light cream or neutral fills for definition elements;
- pale warm/orange fills for usage elements;
- thin, subdued outlines with sufficient contrast;
- compact, legible sans-serif typography;
- clear element labels and textual compartments where relevant;
- disciplined spacing and alignment;
- clean, unobtrusive diagram background.

The geometry and relationship symbols remain governed by the notation reference, not by the style profile. Color is a presentation choice only: never use color as the sole indication of semantic type. Do not reproduce the cheat sheet's page layout, logos, decorative texture, exact artwork, or complete diagram compositions.

If a user requests another style, treat it as a separate named visual profile (for example, `PlainStyle`) and do not silently alter IBMstyle. If the user does not specify a style, use IBMstyle.

### 5. Layout and render

- Generate SVG as the primary output.
- Use consistent typography, spacing, alignment and line routing.
- Keep labels readable and avoid connector crossings where practical.
- Do not let layout convenience change model semantics.
- Do not use arbitrary lines to visually associate unrelated elements.
- Use the active visual profile consistently without allowing it to override notation.

### 6. Validate

Check:
- every rendered element exists in the source model;
- every rendered relationship exists in the source model or is an explicitly identified, semantically justified derived relationship;
- no unsupported relationship or decorative connector has been introduced;
- no supported source element was unintentionally omitted from the requested view;
- definition/usage distinctions are applied consistently;
- usage typing is represented correctly where included;
- labels and typing are accurate;
- graphical conventions are sourced or explicitly marked as provisional;
- visual style is consistent and does not encode unsupported semantics;
- the SVG is well-formed and readable.

Report any omissions, assumptions, unresolved notation questions and rendering decisions.

## Response format

For each rendering task, provide:
1. **Scope** — what part of the model is shown.
2. **Semantic inventory** — concise list of rendered elements and relationships.
3. **Notation status** — sourced conventions versus provisional decisions.
4. **Visual style** — active style profile (IBMstyle by default).
5. **SVG** — complete SVG output, preferably as a standalone artifact when file generation is available.
6. **Validation** — findings and known limitations.

Do not claim full SysML v2 compliance. State the subset actually handled.

## Incremental development rule

When a new construct is requested:
1. determine whether its semantics are understood;
2. identify its graphical convention in the reference;
3. add a minimal test model;
4. render and validate it;
5. only then include it in the supported scope.

Prefer a small, tested capability over broad but unreliable coverage.
