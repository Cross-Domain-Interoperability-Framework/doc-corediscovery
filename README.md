# CDIF Discovery (composite application profile)

This repository holds the published artifacts for the **CDIF Discovery application profile** — the composite that combines `cdifCore` and `cdifDiscovery` from the [metadataBuildingBlocks](https://github.com/Cross-Domain-Interoperability-Framework/metadataBuildingBlocks) source register into a single, self-contained release.

> **Scope.** This is the *application profile* (human-facing content requirements for making datasets discoverable). The thin profile modules it composes — `cdifCore` and `cdifDiscovery` — are published in [profile-core](https://github.com/Cross-Domain-Interoperability-Framework/profile-core) and [profile-discovery](https://github.com/Cross-Domain-Interoperability-Framework/profile-discovery).

## Specification

- **[CDIFDiscoveryDocImplementationGuide.md](CDIFDiscoveryDocImplementationGuide.md)** — Implementation guide: required, conditional, and recommended elements; conformance rules; mappings to Dublin Core, schema.org, ISO 19115-1, DCAT, DDI-CDI, and FDO.
- **[CDIFDiscoveryDocStructuredSchema.json](CDIFDiscoveryDocStructuredSchema.json)** — Resolved JSON Schema (Draft 2020-12) generated from the source register.
- **[discoveryDocRules.shacl](discoveryDocRules.shacl)** — Self-contained SHACL shapes, merged from every composing building block plus the profile-level shapes.
- **[CDIFDiscoveryDoc-frame.jsonld](CDIFDiscoveryDoc-frame.jsonld)** — JSON-LD frame used by `FrameAndValidate.py`.

## Conformance

A conforming instance declares, in its `dcterms:conformsTo`, both:

- `https://w3id.org/cdif/core/1.1`
- `https://w3id.org/cdif/discovery/1.1`

## Examples

`examples/` holds JSON-LD discovery records, sourced from production catalogues (GeoCodes, NCEI NOAA, Copernicus CDS, Dataverse, ESIP, ODIS) and synthetic mBB-canonical examples. All declare the required `conformsTo` and pass JSON Schema validation. Validate one with:

```bash
python FrameAndValidate.py examples/CDIF-aloha-dataset.json --validate
```

`FrameAndValidate.py` frames the document against `CDIFDiscoveryDoc-frame.jsonld`, array-wraps the multi-valued properties, then validates against the JSON Schema. Validation is open-world: unknown properties pass.

## Synced from metadataBuildingBlocks

These generated artifacts are re-synced when the source register changes:

| file | source command |
|---|---|
| `CDIFDiscoveryDocStructuredSchema.json` | `python tools/resolve_schema.py CoreDiscovery -o CDIFDiscoveryDocStructuredSchema.json` |
| `discoveryDocRules.shacl` | `python tools/validate_shacl.py CoreDiscovery --emit-shapes discoveryDocRules.shacl` |

Source composite: `metadataBuildingBlocks/_sources/profiles/cdifCompositeProfile/CoreDiscovery/`.

## Changelog — reviewRevision202606 (updates since branched from `main`)

This release-review branch has diverged from `main` with the following updates,
synced from the CDIF **metadataBuildingBlocks** source (see
`git log main..reviewRevision202606` for the full per-commit history):

- **Populated from metadataBuildingBlocks** — `*StructuredSchema.json`, merged SHACL,
  JSON-LD frame, examples, and the normative `FrameAndValidate.py` generated from the
  building-block source; `Examples/` renamed to `examples/`.
- **CDIF v1.1** — profile conformance URIs migrated `/1.0` → `/1.1`.
- **License** standardized on CC-BY-4.0.
- **`@id`-reference tightening** — bare `{@id}` reference slots sealed
  (`additionalProperties: false` + `required: ['@id']`); a canonical `objectReference`
  building block introduced as the strict node reference.
- **`prov:used` wrapper reconciliation** — the base `generatedBy.prov:used` accepts
  role-keyed wrappers (`schema:instrument` / `bios:computationalTool` / `prov:reagent`)
  alongside string / `{@id}` / inline `prov:Entity`; profiles pin a wrapper's shape via
  a constraint-only `if/then` (never a narrowed `anyOf`).
- **`skos:notation` → single string** at concept level (consistent with the codelist
  single-notation design).
- **`FrameAndValidate.py`** (normative, drift-checked against
  `Cross-Domain-Interoperability-Framework/validation`) — two-frame root-`@type`
  selection, context-aware `schema:about`, `--conformance` detection, `cdif:`-`@id`
  re-expansion, and (2026-08) reference-collapse on all document types + blank-node
  dedupe + agent `schema:identifier` unwrap, so `@embed:@always`-framed documents
  validate against the tightened schemas.
- **Examples** conformed to the tightened schemas throughout (PrimaryKey →
  `cdi:ComponentPosition`, reference slots → `{@id}`, CVE `hasIntendedDataType` →
  string, `skos:notation` → string, `schema:additionalType` URI → `{@id}`).


## Development branch

Active work for the 2026-06 review revision is on the `reviewRevision202606` branch. `main` reflects the prior release state. New changes should target the review branch; it is merged to main on release.

## License

This work is licensed under [Creative Commons Attribution 4.0 International (CC BY 4.0)](LICENSE).
