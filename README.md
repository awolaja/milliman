# Milliman Clinical & Claims Data Pipeline

This project demonstrates a Spark-based data pipeline for parsing clinical XML data (C-CDA format), joining it with health claims data, mapping it to FHIR-aligned structures, and exporting structured outputs ready for analysis or ingestion into platforms like Databricks.

##  Overview

- Downloads clinical C-CDA XML files using pre-signed S3 URLs
- Extracts Medications and Problems from XML using Python and ElementTree
- Joins parsed clinical data with claims and pharmacy claims CSVs
- Validates key fields (e.g., ClaimID, NDC, FromDate)
- Outputs clean Parquet and CSV files for downstream use
- Maps data into a simplified FHIR-aligned CDM structure
- Includes data quality tests implemented inline with PySpark

##  Setup Instructions

> **Dependencies:**
- Python 3.8+
- PySpark
- pandas (for early exploration)
- XML libraries (ElementTree)
- local Jupyter Notebook environment



### Local
```bash
pip install pyspark pandas
```

##  How to Run

1. Upload or mount the following files:
   - `ccda_pre_signed_urls.csv`
   - `data_engineer_exam_claims_final.csv`
   - `data_engineer_exam_rx_final.csv`
   - `data_overview.csv`

2. Run the notebook cells in order:
   - Step 1: Download XML files
   - Step 2: Parse C-CDA files
   - Step 3: Load and join with claims
   - Step 4: Export to Parquet
   - Step 5: FHIR/CDM mapping
   - Step 6–8: Optional unit tests & validations

3. Outputs will be saved to:
   ```
   /content/processed_data/
   /content/data/output/
   ```

## Output Files

| File                          | Format  | Description                              |
|------------------------------|---------|------------------------------------------|
| merged_medications.parquet   | Parquet | Medications + pharmacy claims            |
| merged_problems.parquet      | Parquet | Problems + diagnosis claims              |
| fhir_medicationstatement     | Parquet | FHIR-aligned MedicationStatement records |
| fhir_condition               | Parquet | FHIR-aligned Condition records           |

##  Data Quality Checks

The pipeline includes in-notebook tests for:
- Missing ClaimID / MemberID
- NDC format (Rx claims)
- Referential file integrity (`data_overview.csv`)
- Logical dates (FromDate <= ToDate)

##  Known Limitations

- Does not support nested FHIR resources (e.g., encounter, practitioner)
- FromDate/ToDate are assumed to be in US format (M/D/YYYY)
- NDC code regex is simplified (numeric only, min 5 digits)

##  Future Improvements

- Convert FHIR mappings to JSON bundles (optional)
- Use structured XML parsers (e.g., lxml or BeautifulSoup)
- Integrate with a real FHIR API or HAPI-FHIR server
- Replace string matching with code system validation (e.g., RxNorm/ICD)

##  File Structure

```
Milliman.ipynb                     # Main notebook
data_engineer_exam_claims_final.csv
data_engineer_exam_rx_final.csv
data_overview.csv
ccda_pre_signed_urls.csv
processed_data/                   # Exported CSV/Parquet outputs
```

---

Created by Adeyemi (Yemi) Awolajafor the Data Engineering assessment.
