# AGENTS.md — AI Agent Guidance for CDIF Discovery (composite application profile)

## Project context

This repository publishes the **CDIF Discovery application profile** — the composite that combines `cdifCore` + `cdifDiscovery` into a single, self-contained release. The thin profile modules it composes are published in `profile-core` and `profile-discovery`; do not duplicate that module-level content here.

## Key files

- `CDIFDiscoveryDocImplementationGuide.md` — implementation guide (required, conditional, and recommended elements; mappings to Dublin Core, schema.org, ISO 19115-1, DCAT, DDI-CDI, FDO)
- `CDIFDiscoveryDocStructuredSchema.json` — resolved JSON Schema (generated)
- `discoveryDocRules.shacl` — merged SHACL shapes (generated)
- `CDIFDiscoveryDoc-frame.jsonld` — JSON-LD frame used by `FrameAndValidate.py`
- `examples/` — validated JSON-LD examples (production catalogues + mBB-canonical)
- `FrameAndValidate.py` — frame + JSON Schema validation

## Synced files (manual sync from metadataBuildingBlocks)

These are generated from the source register and must be re-synced when the source changes:

- `CDIFDiscoveryDocStructuredSchema.json` ← `python tools/resolve_schema.py CoreDiscovery -o <file>`
- `discoveryDocRules.shacl` ← `python tools/validate_shacl.py CoreDiscovery --emit-shapes <file>`

Source composite dir: `metadataBuildingBlocks/_sources/profiles/cdifCompositeProfile/CoreDiscovery/`.

## Example conventions

1. `@context` declares explicit prefixes (`schema`, `dcterms`, `dcat`, `prov`) — never `@vocab`.
2. `schema:` prefix on all schema.org property names; namespace is `http://schema.org/` (never `https://`).
3. `@type` as arrays (e.g. `["schema:Dataset"]`).
4. `schema:subjectOf` carries a `dcat:CatalogRecord` whose `dcterms:conformsTo` includes both `https://w3id.org/cdif/core/1.1` and `https://w3id.org/cdif/discovery/1.1`.
5. Never strip unknown properties — validation is open-world.

## Validation

```bash
python FrameAndValidate.py examples/<file>.json --validate \
  --schema CDIFDiscoveryDocStructuredSchema.json --frame CDIFDiscoveryDoc-frame.jsonld
```

## Development branch

Active development for the 2026-06 review revision targets the `reviewRevision202606` branch; merged to `main` on release.
