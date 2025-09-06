# DFO Salmon Ontology

**Namespace:** `https://w3id.org/dfo/salmon#` (prefix: `dfo:`)  
**License:** CC-BY 4.0  
**Status:** Single-file, OWL-only, WebProtégé-ready

The DFO Salmon Ontology is a **single OWL ontology** for salmon science data at Fisheries and Oceans Canada (DFO). It aligns with the Darwin Core (DwC) conceptual layer where helpful and adds DFO-specific concepts for stock assessment and genetics.  
**Goal:** Make salmon data interoperable, discoverable, and analyzable with minimal friction for scientists, data stewards, and managers.

---

## Table of Contents

- Overview
- Quickstart (WebProtégé & OntoGraf)
- Workflow & Editing Guidelines
- Modeling Approach
- Conventions (Updated)
- Ontology Scope
- IRI & Versioning Policy
- Contribution Workflow
- Roadmap
- Acknowledgments

---

## Overview

- **One file**: `dfo-salmon.ttl` (OWL/Turtle).
- **No SKOS, no SHACL** for now; focus on **classes + properties**.
- **Reuse before invent**: align to DwC (`dwc:Event`, `dwc:MaterialSample`, `dwc:MeasurementOrFact`) via `rdfs:subClassOf`, but don’t import DwC yet.
- **Units**: QUDT/OM **IRIs stored as literals** (starter convention).
- **Community-aligned**: builds on NCEAS Salmon Ontology, ENVO, and OBO Foundry vocabularies.

---

## Quickstart (WebProtégé & OntoGraf)

1. Create a new project in **WebProtégé** and upload `dfo-salmon.ttl`.
2. Use **OntoGraf** to explore class/property relationships interactively.
3. Discuss proposed edits in GitHub Issues.
4. Approved edits are applied directly to `dfo-salmon.ttl`.
5. **IRIs are permanent**: update labels/comments, not IRIs.

---

## Workflow & Editing Guidelines

- We are maintaining **one ontology file** in OWL format (`.ttl`) on GitHub as the single source of truth.
- All editing is done via GitHub Pull Requests (PRs).
- Use WebProtégé + OntoGraf to visualize and verify connections.
- **Before creating a new term**: search WebProtégé to ensure it doesn’t already exist.
- **Be consistent**: follow the conventions below.
- **Keep it simple**: avoid complex restrictions (e.g., `someValuesFrom`) unless agreed.
- **Document everything**: always include `rdfs:comment` and, if possible, a `dcterms:source`.
- **Discuss major changes**: use GitHub Issues for uncertain modeling decisions.

---

## Modeling Approach

- **OWL-only**: all terms are `owl:Class`, `owl:ObjectProperty`, or `owl:DatatypeProperty`.
- **Human + machine friendly**: every term has a label + definition.
- **Domain fit**: initial focus on stock assessment and genetics; expand iteratively.
- **Minimal constraints**: use domains/ranges only when they improve data quality.
- **Visualization**: OntoGraf helps verify relationships and explain the ontology.

---

## Conventions (Updated)

### Classes

Required:

- `a owl:Class`
- `rdfs:label "Human Name"@en`
- `rdfs:comment "1–2 sentence definition."@en`
- `rdfs:isDefinedBy <https://w3id.org/dfo/salmon>`

Optional:

- `dcterms:source <URL or citation>`
- `dcterms:description "Example usage."@en`
- `oboInOwl:hasExactSynonym` (if relevant)

### Object Properties

- `a owl:ObjectProperty`
- `rdfs:label` + `rdfs:comment`
- Domain/Range only when it helps data quality (avoid over-constraining early)
- **Naming convention**: lowerCamelCase from subject → object (e.g., `aboutStock`, `usesMethod`)
- Always add `rdfs:isDefinedBy`

### Datatype Properties

- `a owl:DatatypeProperty`
- `rdfs:label` + `rdfs:comment`
- Range must be an explicit XSD type (`xsd:string`, `xsd:decimal`, `xsd:date`, etc.)
- Units & IRIs as **literals** (starter convention)
- Always add `rdfs:isDefinedBy`

---

### Hierarchy & Relationships (NEW)

OWL is most powerful when terms are related to one another. We will keep it simple:

- **Subclassing required**: If a new class is a type of an existing one, assert `rdfs:subClassOf`.
  - Example: `EscapementSurveyEvent ⊑ SurveyEvent`
- **Equivalence optional**: Use `owl:equivalentClass` if two terms mean _exactly_ the same.
  - Example: if we align a DFO term to an NCEAS term that is identical.
- **Disjointness optional**: Use `owl:disjointWith` when two sibling classes should never overlap.
  - Example: `AutomatedCountingMethods ⊓ ExpertOpinion = ⊥`
- **Part–whole optional**: Use `hasPart` / `partOf` only when needed for compositions.
- **Do not use SKOS broader/narrower**: Stay in OWL; subclassing covers hypernym/hyponym.

---

### Beginner-Friendly Conventions

- **Keep labels and comments human-readable**: short, clear, plain language.
- **Always check if a concept already exists** before creating a new one.
- **Start flat, then nest**: define a new class with a label/comment; only add `subClassOf` once we’re sure it belongs under another.
- **Examples are optional but helpful**: use `dcterms:description` to give a short usage case.
- **Don’t panic about being “wrong”**: IRIs are permanent, but labels/comments can be refined over time.

---

### Intermediate Conventions

- **Use domains/ranges with care**: add them where it helps catch obvious mistakes, but don’t over-constrain.
- **Re-use external terms where practical**: align via `rdfs:subClassOf` or equivalence instead of inventing new classes.
- **Deprecate, don’t delete**: if a term is replaced, mark with `owl:deprecated true` and point to the replacement with `rdfs:seeAlso`.
- **Organize hierarchies thoughtfully**: group related methods, measurements, or events so the class tree is intuitive.
- **Use consistent property naming**: lowerCamelCase, subject → object.

---

### Future Advanced Conventions (for later discussion)

These are not required now but should be on our radar:

- **OWL restrictions**: e.g., `someValuesFrom`, `allValuesFrom` for richer constraints.
- **Property characteristics**: functional, inverse functional, transitive, symmetric, etc.
  - Example: `hasConservationUnit` could eventually be functional (a Stock has only one CU).
- **Property chains**: define reasoning shortcuts (e.g., Sample `ofStock` + Stock `hasCU` → Sample `ofCU`).
- **Ontology modularization**: break into thematic modules (stock assessment, genetics, habitat) with clear integration.
- **Logical definitions**: define classes based on property restrictions (e.g., “EscapementSurveyEvent ≡ SurveyEvent ⊓ ∃usesMethod.EscapementMethod”).
- **Linking to external ontologies**: move from literal IRIs to object links with imports (GBIF, ENVO, OBI, QUDT).
- **Reasoning & validation**: run OWL reasoners to classify automatically; use SHACL for data validation.

---

⚖️ **Key Principle:** Start simple with clear labels, comments, and subclassing. Add structure gradually as we gain confidence.

## Ontology Scope (Current)

**Core Classes**

- `dfo:Stock`, `dfo:ConservationUnit`, `dfo:ManagementUnit`
- `dfo:SurveyEvent` (⊑ `dwc:Event`)
- `dfo:EscapementMeasurement` (⊑ `dwc:MeasurementOrFact`)
- `dfo:Indicator`, `dfo:Dataset` (⊑ `schema:Dataset`)

**Stock Assessment Specializations**

- `dfo:EscapementSurveyEvent`
- `dfo:SonarCountMeasurement`, `dfo:WeirCountMeasurement`, `dfo:AerialCountMeasurement`
- `dfo:EscapementMethod` + subclasses (`AreaUnderTheCurve`, `AutomatedCountingMethods`, `UnknownMethod`, …)

**Genetics (GSI)**

- Classes: `dfo:GeneticSample`, `dfo:GSIRun`, `dfo:GSICompositionMeasurement`, `dfo:ReportingUnit`, `dfo:Assay`, `dfo:MarkerPanel`, `dfo:Protocol`
- Object properties: `sampledDuring`, `ofStock`, `usedAssay`, `usedMarkerPanel`, `usedProtocol`, `analyzesSamples`, `producedMeasurement`, `derivedFromSample`, `aboutReportingUnit`, `hasReportingUnit`
- Datatypes: `estimateValue`, `estimateUnitIRI`, `standardError`, `ciLower`, `ciUpper`, `confidenceLevel`, `methodName`, `baselineName`, `runDate`, `sampleID`, `tissueType`, `collectionMethod`

---

## IRI & Versioning Policy

- Base IRI: `https://w3id.org/dfo/salmon#`
- Instances: mint under same base (`…#Stock/SkeenaSockeye`)
- External alignments: keep as literals for now (e.g., GBIF taxon → `dfo:taxonIRI`)
- Units: QUDT IRIs as literals in `…UnitIRI` properties
- Versioning:
  - Maintain `owl:versionInfo` in ontology header
  - Tag GitHub releases (e.g., `v0.1.0`)
  - Archive via Zenodo for DOI

---

## Contribution Workflow

- Propose changes in GitHub Issues.
- Discuss/agree on definitions before structural edits.
- Keep edits atomic (one conceptual change per PR).
- Do not rename IRIs; if refactoring, deprecate and add `rdfs:seeAlso`.

**Definition quality checklist:**

- One clear concept per term
- Human-readable label and comment
- Example/source if contentious
- Avoid over-constraining with domains/ranges

---

## Roadmap

- Fill missing `rdfs:comment` definitions.
- Add minimal individuals for examples.
- Consider SHACL validation later.
- Decide when to replace literal IRIs with object links.
- Publish docs via pyLODE/Widoco.
- Register W3ID redirects.

---

## Acknowledgments

This ontology builds on:

- Darwin Core / GBIF (conceptual backbone)
- NCEAS Salmon Ontology, ENVO, and OBO Foundry ontologies
- Input from DFO biologists, data stewards, and the RDA Salmon Ontology WG
- Guidance from the Salmon Data Stewardship community
