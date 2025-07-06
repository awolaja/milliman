# milliman

## Project Overview

This project implements a basic data pipeline to process clinical documents in the C-CDA format. The pipeline:

1. Downloads clinical data from a list of pre-signed S3 URLs.
2. Parses relevant clinical domains (Medications and Problems) from the XML documents.
3. (Planned) Combines parsed data with claims data.
4. Stores the processed output in a flat file (CSV/Parquet) for ingestion into Databricks.
5. (Optional) Describes a pipeline-to-CDM mapping using FHIR/HL7.
