# milliman

## Project Overview

This project implements a basic data pipeline to process clinical documents in the C-CDA format. The pipeline:

1. Downloads clinical data from a list of pre-signed S3 URLs.
2. Parses relevant clinical domains (Medications and Problems) from the XML documents.
3. (Planned) Combines parsed data with claims data.
4. Stores the processed output in a flat file (CSV/Parquet) for ingestion into Databricks.
5. (Optional) Describes a pipeline-to-CDM mapping using FHIR/HL7.


## Pipeline Steps and Rationale

### 1. Download C-CDA Files
- Reads URLs from a CSV file.
- Downloads each document using `requests` and saves to disk.
- **Why:** Ensures local access to clinical XML data.

### 2. Parse Medications and Problems
- Parses each XML document using `ElementTree` or `lxml`.
- Extracts medications (e.g., using `substanceAdministration` entries).
- Extracts problems (e.g., from `observation` nodes in problem sections).
- **Why:** Translates unstructured XML into structured domain-specific datasets.

### 3. (Planned) Combine with Claims Data
- Will merge clinical and claims data using a patient ID or similar key.
- **Why:** Provides a unified view of clinical and administrative data.

### 4. Output Final Dataset
- Saves to `combined_data.csv` or `combined_data.parquet`.
- Designed for easy import into Databricks.
