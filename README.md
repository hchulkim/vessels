# vessels

Vessel identifiers and characteristics, combined from several sources into one CSV.

## Contents

- [Overview](#overview)
- [Citation](#citation)
- [Data content](#data-content)
- [Data structure](#data-structure)
- [Data pipeline](#data-pipeline)
- [References](#references)
- [Use of AI](#use-of-ai)
- [Contact](#contact)

## Overview

Download [data/vessels.csv](data/vessels.csv) for **68,324 vessels**, with one row per
IMO number. The dataset includes names, identifiers, vessel types, dimensions,
tonnage, and construction details where available.

**Note:** This dataset is a best-effort compilation of historical vessel records
from publicly available sources. Many fields contain missing values, partly
because these sources vary in coverage and completeness. See [Data content](#data-content)
for missing-value statistics by column. The dataset does not provide a complete
inventory of currently active vessels. Names, flags, and MMSIs can change over
time, so the recorded values may no longer reflect a vessel's current identity or
status.

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

## Data content

The 2026-10-01 release contains **68,324 rows and 91 columns**. Each row
represents a unique IMO number; columns include vessel characteristics, source
attribution, observation dates, and quality-control indicators.

### Missing values

The tables below summarize every column in `data/vessels.csv`. Missingness is the
number of blank or whitespace-only cells divided by all 68,324 rows. Values such
as `0` and `FALSE` count as present. Percentages are rounded to two decimal places,
so a displayed 100.00% can include a few nonmissing values; use the counts to
distinguish these cases.

IMO numbers are complete. Vessel names are missing for 5.21% of rows, vessel types
for 13.19%, MMSIs for 17.81%, and flags for 25.72%. Construction and dimension fields
have larger gaps. `depth_m`, `engine_power_kw`, and `gfw_ship_type` are entirely
empty in this release.

| Column | Missing rows | Missing (%) |
|---|---:|---:|
| `imo` | 0 | 0.00% |
| `mmsi` | 12,170 | 17.81% |
| `call_sign` | 38,497 | 56.34% |
| `ship_name` | 3,561 | 5.21% |
| `ship_type` | 9,011 | 13.19% |
| `flag` | 17,575 | 25.72% |
| `year_built` | 39,290 | 57.51% |
| `builder` | 40,185 | 58.82% |
| `build_location` | 67,675 | 99.05% |
| `inception_time_literal` | 68,081 | 99.64% |
| `gross_tonnage` | 12,737 | 18.64% |
| `net_tonnage` | 45,136 | 66.06% |
| `deadweight` | 41,789 | 61.16% |
| `length_m` | 63,174 | 92.46% |
| `beam_m` | 63,384 | 92.77% |
| `depth_m` | 68,324 | 100.00% |
| `length` | 42,701 | 62.50% |
| `beam` | 42,701 | 62.50% |
| `ship_draught` | 45,457 | 66.53% |
| `powered_by` | 68,141 | 99.73% |
| `energy_source` | 68,318 | 99.99% |
| `engine_power_kw` | 68,324 | 100.00% |
| `ais_vessel_type_code` | 63,124 | 92.39% |
| `gfw_ship_type` | 68,324 | 100.00% |

<details>
<summary>Missingness in source, date, count, and quality-control columns</summary>

Metadata columns describe particular sources or processing steps. A blank metadata
cell does not necessarily mean the corresponding vessel characteristic is missing.

| Column | Missing rows | Missing (%) |
|---|---:|---:|
| `first_observation` | 41,378 | 60.56% |
| `last_observation` | 41,378 | 60.56% |
| `n_observations` | 41,378 | 60.56% |
| `n_sources` | 41,378 | 60.56% |
| `sources` | 41,378 | 60.56% |
| `as_of_deadweight` | 64,154 | 93.90% |
| `as_of_flag` | 64,154 | 93.90% |
| `as_of_gross_tonnage` | 64,154 | 93.90% |
| `as_of_ship_name` | 41,378 | 60.56% |
| `as_of_ship_type` | 41,378 | 60.56% |
| `as_of_year_built` | 64,154 | 93.90% |
| `conflict_latest_deadweight` | 64,154 | 93.90% |
| `conflict_latest_flag` | 64,154 | 93.90% |
| `conflict_latest_gross_tonnage` | 64,154 | 93.90% |
| `conflict_latest_ship_name` | 41,378 | 60.56% |
| `conflict_latest_ship_type` | 41,378 | 60.56% |
| `conflict_latest_year_built` | 64,154 | 93.90% |
| `in_step03` | 0 | 0.00% |
| `in_previous_imo_list` | 0 | 0.00% |
| `local_source_ship_name` | 30,030 | 43.95% |
| `local_conflict_ship_name` | 0 | 0.00% |
| `local_source_ship_type` | 35,913 | 52.56% |
| `local_conflict_ship_type` | 0 | 0.00% |
| `local_source_flag` | 21,753 | 31.84% |
| `local_conflict_flag` | 0 | 0.00% |
| `local_source_gross_tonnage` | 43,497 | 63.66% |
| `local_conflict_gross_tonnage` | 0 | 0.00% |
| `local_source_deadweight` | 45,959 | 67.27% |
| `local_conflict_deadweight` | 0 | 0.00% |
| `local_source_year_built` | 43,460 | 63.61% |
| `local_conflict_year_built` | 0 | 0.00% |
| `local_source_mmsi` | 13,057 | 19.11% |
| `local_conflict_mmsi` | 0 | 0.00% |
| `local_source_call_sign` | 41,908 | 61.34% |
| `local_conflict_call_sign` | 0 | 0.00% |
| `local_source_net_tonnage` | 45,136 | 66.06% |
| `local_conflict_net_tonnage` | 0 | 0.00% |
| `local_source_ship_draught` | 45,457 | 66.53% |
| `local_conflict_ship_draught` | 0 | 0.00% |
| `local_source_length` | 42,701 | 62.50% |
| `local_conflict_length` | 0 | 0.00% |
| `local_source_beam` | 42,701 | 62.50% |
| `local_conflict_beam` | 0 | 0.00% |
| `local_sources` | 7,626 | 11.16% |
| `n_local_observations` | 7,626 | 11.16% |
| `public_source_ship_name` | 68,324 | 100.00% |
| `public_source_mmsi` | 67,439 | 98.70% |
| `public_source_call_sign` | 64,923 | 95.02% |
| `public_source_gross_tonnage` | 41,782 | 61.15% |
| `public_source_builder` | 40,185 | 58.82% |
| `public_source_build_location` | 67,675 | 99.05% |
| `public_source_powered_by` | 68,141 | 99.73% |
| `public_source_energy_source` | 68,318 | 99.99% |
| `public_source_inception_time_literal` | 68,081 | 99.64% |
| `public_source_length_m` | 63,215 | 92.52% |
| `public_source_beam_m` | 63,384 | 92.77% |
| `public_source_ais_vessel_type_code` | 63,124 | 92.39% |
| `gfw_source_ship_name` | 68,324 | 100.00% |
| `gfw_source_call_sign` | 68,314 | 99.99% |
| `gfw_source_mmsi` | 68,322 | 100.00% |
| `gfw_source_flag` | 68,316 | 99.99% |
| `gfw_source_gfw_ship_type` | 68,324 | 100.00% |
| `gfw_source_gross_tonnage` | 68,276 | 99.93% |
| `gfw_source_length_m` | 68,283 | 99.94% |
| `gfw_source_year_built` | 68,324 | 100.00% |
| `gfw_source_depth_m` | 68,324 | 100.00% |
| `gfw_source_engine_power_kw` | 68,324 | 100.00% |

</details>

### Example rows

The first five rows of the CSV are shown below with selected columns. An em dash
(`—`) represents a blank cell in the file. These rows illustrate the format and
are not a representative sample of vessel types or data completeness. Values and
source labels are reproduced as stored.

| `imo` | `ship_name` | `ship_type` | `flag` | `mmsi` | `gross_tonnage` | `year_built` |
|---|---|---|---|---|---|---|
| 1000019 | LADY K II | Yacht | — | 235095435 | 551 | 1961 |
| 1000021 | MONTKAJ | Yacht | — | 319904000 | 2000 | 1995 |
| 1000057 | LIMA | Pleasure Craft | SA | 403070000 | 234 | — |
| 1000069 | LADY BEATRICE | — | UK | 233219000 | 17 | 1994 |
| 1000239 | MQ2 | Yacht | — | 229551000 | 467 | — |

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
