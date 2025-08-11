# Healthcare-Data-Engineering-for-Clinical-Analytics-Reporting (IN PROGRESS..)

### Project Goal
To design and implement a dimensional data warehouse to integrate CMS synthetic claims data with simulated EHR/FHIR extracts, supporting operational reporting and BI use cases.

### Architecture

1. **Data Sources:** CMS synthetic claims CSVs; simulated FHIR JSON extracts for encounters, observations, and medications.
2. **Staging Layer (SQL Server):** Raw data loaded into staging tables; JSON parsed via `OPENJSON()` to relational format.
3. **Transformation:** Data cleansing, ICD/CPT code standardization, payer normalization, deduplication, SCD logic for dimensions, and fact table population.
4. **Warehouse Layer:** Star schema with conformed dimensions (patient, provider, payer, facility, date) and indexed fact tables (claims, encounters) for reporting.
5. **Semantic Layer:** Indexed views and summary tables for BI consumption in Tableau.

### Data Modeling

* **Star Schema Design:** Fact tables keyed to conformed dimensions.
* **Index Strategy:** Clustered indexes on surrogate keys, nonclustered indexes on frequent query filters, and partitioning.

### ETL Logic (T-SQL and Python)

* **Extract:** BULK INSERT for CSV; OPENROWSET and OPENJSON for JSON parsing.
* **Transform:** Apply business rules, lookup dimension keys, standardize code formats, handle nulls, enforce referential integrity.
* **Load:** Transactional batch loads with rollback on failure, incremental updates via change tracking columns.

### Data Quality

* Post-load validation with row count comparison, and anomaly detection queries.
* PII fields masked in reporting views using `MASKED WITH (FUNCTION = 'default()')` for HIPAA compliance.
* Role-based security in SQL Server for restricting sensitive data.

### Reporting & Visualization

* Build Tableu dashboards connected to SQL Server views, visualizing claims volume trends, denial patterns, and cost/utilization KPIs.

### Technologies

**SQL Server Express**, **T-SQL**, **Tableu**, SSMS, CSV/JSON parsing, HIPAA-compliant data handling.


