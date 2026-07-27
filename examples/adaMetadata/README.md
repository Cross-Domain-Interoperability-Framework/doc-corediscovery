# adaMetadata examples

10 CDIF metadata records drawn from the ADA (Astromaterials Data
Archive) sample-analysis corpus. Each record describes analytical
data on OSIRIS-REx Bennu samples. All 10 validate clean against the
CoreDiscovery composite schema and declare
`https://w3id.org/cdif/core/1.1`, `https://w3id.org/cdif/discovery/1.1`,
and `https://w3id.org/cdif/manifest/1.1` in
`schema:subjectOf/dcterms:conformsTo`. Non-CDIF conformance URIs
(`ada:*`) are preserved alongside.

## The 10 examples cover these axes of variability

Selected from a 69-record source corpus to span measurement modality
and dataset shape. The remaining 59 records are archived at
`../../archive/adaMetadata/` for full-corpus reference.

| File | Technique | Vars |
|------|-----------|-----:|
| `metadata_10.60707-fzjk-kt84.json` | Quadrupole ICP-MS (Q-ICP-MS bulk elemental analysis) | 195 |
| `metadata_10.60707-rm08-bg04.json` | ICP-OES (chemical composition) | 45 |
| `metadata_10.60707-2mdz-qh58.json` | Accelerator Mass Spectrometry (10Be dating) | 18 |
| `metadata_10.60707-j16b-6288.json` | Electron microprobe analysis (major element mapping) | 11 |
| `metadata_10.60707-y3a1-7706.json` | Noble gas + Nitrogen static mass spectrometry | 11 |
| `metadata_10.60707-7hya-7y42.json` | Gas pycnometry (physical property) | 8 |
| `metadata_10.60707-mayf-0w17.json` | Raman vibrational spectroscopy | 3 |
| `metadata_10.60707-64vm-zd18.json` | Structured Light Scanning (3D imaging) | 0 |
| `metadata_10.60707-4b5r-q306.json` | X-ray computed tomography | 0 |
| `metadata_10.60707-1svq-4w22.json` | Scanning electron microscopy | 0 |

**Coverage:**

- **Modality**: mass-spec (3 flavors: Q-ICP-MS, AMS, noble-gas static),
  chemical composition (ICP-OES, EMP), imaging (SEM, X-ray CT,
  Structured Light Scanning), spectroscopy (Raman), physical property
  (gas pycnometry).
- **Variable count**: 0 (3 examples — image / 3D-scan / metadata-only),
  3, 8, 11, 11, 18, 45, 195. Covers "image-only" through
  "tabular-with-many-columns" shapes.

## Provenance

Records originally in `profile-datastructure/archive/exampleMetadata/adaMetadata/`.
Detected conformance via `validation/tools/FrameAndValidate.py --conformance`
(uses `detect_conformance.py`). Framing pass, `@context` normalization
(`https://schema.org/` → `http://schema.org/`), `schema:subjectOf`
CatalogRecord additionalType patch, `schema:dateModified` back-fill
from `schema:datePublished`, and `schema:MonetaryGrant` funding sentinel
(`schema:name = "Missing"`) all applied automatically. See the batch
audit report at
`profile-datastructure@reviewRevision202606:archive/exampleMetadata/batch_audit_report.{txt,csv,json}`
for full provenance.
