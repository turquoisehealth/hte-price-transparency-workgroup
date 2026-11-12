# SSP data dictionary

Generated from `schemas/` by the companion guide build. Do not edit by hand.

## ssp/<SSP_ID>.json and ssp.jsonl

One SSP with its clinical sub-variants and bundled contents. Generated from the SSP CSV exports. Schema: `schemas/ssp.schema.json`.

| Field | Type | Description | Allowed values |
|---|---|---|---|
| `id` | string | Five character SSP grouper ID, e.g. AE02Z. Billed in place of the anchor code. |  |
| `version` | string | SSP library release version. |  |
| `title` | string | Consumer-facing SSP name. |  |
| `description` | string | Consumer-facing plain text description of the SSP. |  |
| `type` | object | Level of care the package is structured at. |  |
| `type.code` | enum | item_service: the anchor code only. encounter: anchor code plus ancillary line items. episode: multi-visit journey. | `item_service`, `encounter`, `episode` |
| `type.label` | enum | Label as it appears in the source CSV. | `I&S`, `Encounter`, `Episode` |
| `disease_area` | string | Clinical grouping used in the SSP library coverage table, e.g. Musculoskeletal. |  |
| `place_of_service` | enum | Outpatient or inpatient setting. | `outpatient`, `inpatient` |
| `shoppability` | number | Turquoise Shoppability score: how far a patient can plan or shop for the service. |  |
| `apc` | string or null | CMS Ambulatory Payment Classification the SSP crosswalks to. Outpatient SSPs only; null when missing. |  |
| `ms_drg` | string or null | CMS MS-DRG the SSP crosswalks to. Inpatient SSPs only. |  |
| `anchor_codes` | array of object | Every code that rolls into this SSP: anchors from the contents export plus every sub-variant's anchor codes. Use this (or code_index.json) to map a billed code to an SSP. |  |
| `anchor_codes[].code` | string | Billing code, e.g. 99214. |  |
| `anchor_codes[].code_type` | enum | Code system of a billing code. | `CPT`, `HCPCS`, `MS-DRG`, `Rev Code` |
| `sub_variants` | array of object | Complexity tiers inside the SSP. Empty when the SSP has no sub-variants. |  |
| `sub_variants[].id` | string | Five character sub-variant ID, e.g. AE022. Shares its first four characters with the SSP ID. |  |
| `sub_variants[].name` | string | Consumer-facing sub-variant name, e.g. Moderate complexity (new or established). |  |
| `sub_variants[].anchor_codes` | array of object | Codes that place a claim in this sub-variant. May be empty in the current export. |  |
| `sub_variants[].anchor_codes[].code` | string | Billing code, e.g. 99214. |  |
| `sub_variants[].anchor_codes[].code_type` | enum | Code system of a billing code. | `CPT`, `HCPCS`, `MS-DRG`, `Rev Code` |
| `contents` | array of object | Services, codes and fees billed in association with the anchor code, as exported. |  |
| `contents[].code` | string | Billing code. |  |
| `contents[].code_type` | enum | Code system of a billing code. | `CPT`, `HCPCS`, `MS-DRG`, `Rev Code` |
| `contents[].fee_type` | enum | Claim the line is billed on. | `facility`, `professional` |
| `contents[].is_anchor` | boolean | Anchor flag as exported. The current export only sets it on facility lines; see anchor_codes for the full set. |  |
| `contents[].association_rate` | number or null | Share of historical anchor claims that included this line, 0 to 1. Null when not exported (MS-DRG anchors). |  |
| `contents[].description` | string | Plain language code description. |  |
| `source` | object | Provenance of this record. |  |
| `source.files` | array of string | CSV exports the record was built from. |  |

## ssp_index.json

Summary of every SSP, with the path to its full record. Schema: `schemas/ssp_index.schema.json`.

| Field | Type | Description | Allowed values |
|---|---|---|---|
| `version` | string | SSP library release version. |  |
| `ssps` | array of object | One entry per SSP, in the order of ssp_list.csv. |  |
| `ssps[].id` | string | SSP grouper ID. |  |
| `ssps[].title` | string | Consumer-facing SSP name. |  |
| `ssps[].type` | enum | Level of care. | `item_service`, `encounter`, `episode` |
| `ssps[].disease_area` | string | Clinical grouping, e.g. Musculoskeletal. |  |
| `ssps[].place_of_service` | enum | Outpatient or inpatient setting. | `outpatient`, `inpatient` |
| `ssps[].sub_variant_ids` | array of string | IDs of the SSP's sub-variants. Empty when it has none. |  |
| `ssps[].file` | string | Path to the full SSP record, relative to this file. |  |

## code_index.json

Reverse lookup from a billed anchor code to the SSP it rolls into. Schema: `schemas/code_index.schema.json`.

| Field | Type | Description | Allowed values |
|---|---|---|---|
| `version` | string | SSP library release version. |  |
| `codes` | object | Keyed by billing code, e.g. 99214. |  |
| `codes.<key>` | object | Where one anchor code rolls up. |  |
| `codes.<key>.code_type` | enum | Code system of the code. | `CPT`, `HCPCS`, `MS-DRG`, `Rev Code` |
| `codes.<key>.ssp_id` | string | SSP the code rolls into. |  |
| `codes.<key>.sub_variant_ids` | array of string | Sub-variants that list this code. Empty when the SSP has none or the code is in no sub-variant. |  |
