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

Example:  
`:GeneticSample a owl:Class ; rdfs:label "Genetic Sample"@en ; rdfs:comment "Tissue or material used in genetic stock identification or lab analyses."@en ; rdfs:subClassOf dwc:MaterialSample ; rdfs:isDefinedBy <https://w3id.org/dfo/salmon> .`

### Object Properties

- `a owl:ObjectProperty`
- `rdfs:label` + `rdfs:comment`
- Domain/Range only when helpful (avoid over-constraining early)
- **Naming convention**: lowerCamelCase from subject → object (e.g., `aboutStock`, `usesMethod`)

Example:  
`:aboutStock a owl:ObjectProperty ; rdfs:label "about stock"@en ; rdfs:comment "Links a measurement to the stock it describes."@en ; rdfs:domain :EscapementMeasurement ; rdfs:range :Stock .`

### Datatype Properties

- `a owl:DatatypeProperty`
- `rdfs:label` + `rdfs:comment`
- Range must be explicit XSD type (`xsd:string`, `xsd:decimal`, `xsd:date`, etc.)
- Units & external references as **literals** (starter convention)

Examples:  
`:estimateValue   a owl:DatatypeProperty ; rdfs:range xsd:decimal .`  
`:estimateUnitIRI a owl:DatatypeProperty ; rdfs:range xsd:anyURI .`  
`:countValue      a owl:DatatypeProperty ; rdfs:range xsd:integer .`  
`:countUnitIRI    a owl:DatatypeProperty ; rdfs:range xsd:anyURI .`

### Minimum Fields Required

Every new class or property must have:

- `rdfs:label` (name)
- `rdfs:comment` (definition)

Optional but encouraged:

- `dcterms:source`, `dcterms:description`, `oboInOwl:hasExactSynonym`

---

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
