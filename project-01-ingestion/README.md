## Architecture

The project demonstrates three ingestion approaches using the Online Retail II dataset in Databricks.

```text
Online Retail II CSV Files
          |
          v
   Unity Catalog Volume
          |
          +--------------------+
          |                    |
          v                    v
   PySpark DataFrame       Cleaned CSV Files
          |                    |
          v                    +------------------+
   retail_bronze                                  |
                               +------------------+
                               |                  |
                               v                  v
                         COPY INTO           Auto Loader
                               |                  |
                               v                  v
                       retail_copy_into   retail_autoloader_bronze
```

## Ingestion Methods

1. **PySpark write:** Read the source CSV, standardize column names, and save the data as a Delta table.
2. **COPY INTO:** Load CSV files into a Delta table using SQL, with file-tracking metadata to avoid reloading previously processed files.
3. **Auto Loader:** Use `cloudFiles` with Structured Streaming and checkpoints to ingest new files incrementally.

## Validation

- Verified row counts across the three ingestion tables.
- Tested incremental ingestion using two sample records.
- Reran `COPY INTO` to validate that previously loaded files were skipped.

## Technologies

- Databricks
- Apache Spark / PySpark
- Delta Lake
- Unity Catalog Volumes
- Auto Loader
- Structured Streaming
- SQL

## Dataset

Online Retail II dataset from Kaggle. The dataset is not included in this repository; users must obtain it from the original source.
