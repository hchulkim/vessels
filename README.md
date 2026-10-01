# vessels

Vessel identifiers and characteristics, combined from several sources into one CSV.

## Contents

- [Overview](#overview)
- [Citation](#citation)
- [Data structure](#data-structure)
- [Data pipeline](#data-pipeline)
- [References](#references)
- [Use of AI](#use-of-ai)
- [Contact](#contact)

## Overview

Download [data/vessels.csv](data/vessels.csv) for **68,324 vessels**, with one row per
IMO number. The dataset includes names, identifiers, vessel types, dimensions,
tonnage, and construction details where available.

This release is a historical collection, not a list of all currently active vessels.
Coverage varies across sources and fields. Names, flags, and MMSIs may have changed;
an identifier in this file should not be assumed to be current.

Release date: **2026-10-01**.

## Citation

If you use this dataset, please cite it and state the release date:

> Kim, Hyoungchul (2026). *Vessels: Vessel Identifiers and Characteristics*.
> Release 2026-10-01. https://github.com/hchulkim/vessels

```bibtex
@misc{kim2026vessels,
  author = {Kim, Hyoungchul},
  title = {Vessels: Vessel Identifiers and Characteristics},
  year = {2026},
  note = {Dataset, release 2026-10-01},
  url = {https://github.com/hchulkim/vessels}
}
```

Please also acknowledge the original sources relevant to your use, listed below.

## Data structure

`data/vessels.csv` is a UTF-8 CSV. Blank cells indicate missing values. Read IMO and
MMSI identifiers as text, rather than measurements.

| Columns | Description |
|---|---|
| `imo` | Unique seven-digit vessel IMO number with a valid checksum. |
| `mmsi`, `call_sign` | Additional identifiers; these may change over time. |
| `ship_name`, `ship_type`, `flag` | Vessel name, type, and flag. Source labels are not fully standardized. |
| `year_built`, `builder`, `build_location` | Construction information, where available. |
| `inception_time_literal` | Wikidata inception timestamp. Its date precision varies; it is not necessarily the build year. |
| `gross_tonnage`, `net_tonnage`, `deadweight` | Tonnage and capacity measures from the sources. |
| `length_m`, `beam_m`, `depth_m` | Dimensions explicitly recorded in metres. Depth is not draught. |
| `length`, `beam`, `ship_draught` | Original source dimensions with unverified units; do not assume metres. |
| `powered_by`, `energy_source`, `engine_power_kw` | Propulsion, energy source, and engine power where available. Coverage is sparse; engine power is currently empty. |
| `ais_vessel_type_code`, `gfw_ship_type` | Separate source classifications; `gfw_ship_type` is currently empty. |
| `sources`, `*_source_*`, `local_sources` | Source attribution for the baseline and added values. |
| `as_of_*`, `first_observation`, `last_observation` | Dates from baseline observations, not a last-verification date for every field. |
| `conflict_latest_*`, `local_conflict_*` | Indicators of conflicting source values. |
| `n_observations`, `n_sources`, `n_local_observations`, `in_*` | Counts and indicators used during construction. |

## Data pipeline

1. Collect company directories and vessel records from EU MRV and the INTERTANKO
   member fleet. Clean company names and keep company IDs separate from vessel IMOs.
2. Combine vessel records by checksum-valid IMO. For dated baseline records, use the
   latest nonmissing value; leave conflicting values at the same date unresolved.
3. Add vessels from MarineVessels and IMO-Vessel-Codes. Keep existing values and fill
   missing fields only when the added records agree. This produces 68,324 unique IMOs.
4. Fill further gaps from Wikidata and existing NOAA AIS downloads. Preserve source
   attribution and keep conflicting values unresolved.
5. Add GFW information using an existing partial snapshot and a 40-vessel API pilot.
   Match by IMO first. MMSI-only links require a matching name or callsign and
   overlapping dated evidence; reject MMSIs associated with multiple IMOs.
6. Check that all IMOs are unique and existing nonmissing values are preserved, then
   export the final table as `data/vessels.csv`.

The GFW step added 109 values across 80 vessels, mainly gross tonnage and length.
It did not query the whole dataset. No Equasis records are included.

This repository currently distributes the final CSV. The build scripts, cached
responses, and detailed audit tables remain in the originating research project
under `code/build/10-build-imo/`; they are not yet included here.

## References

- EU MRV vessel reports (2018–2025) and the INTERTANKO member fleet table.
- [MarineVessels](https://github.com/rich-iannone/MarineVessels).
- [IMO-Vessel-Codes](https://github.com/warrantgroup/IMO-Vessel-Codes).
- [Wikidata](https://www.wikidata.org/).
- NOAA Marine Cadastre AIS downloads.
- [Global Fishing Watch](https://globalfishingwatch.org/), vessel identity dataset
  `public-global-vessel-identity:v4.0`.

## Use of AI

OpenAI Codex assisted with writing and debugging the data-processing code,
validation checks, and documentation. Vessel facts were taken from source records,
not generated by AI. Checks cover identifier validity, duplicate IMOs, matching
rules, and preservation of existing values; they do not independently verify every
source record. Responsibility for the dataset remains with the maintainer.

## Contact

Hyoungchul Kim — [hkim.inbox@gmail.com](mailto:hkim.inbox@gmail.com)
