# Data Engineering Project

A hands-on project to build and practice data engineering skills using modern tools and technologies.

## Overview

This project ingests NYC Yellow Taxi trip data into a PostgreSQL database, containerized with Docker for reproducibility. The goal is to progressively cover the full data engineering stack — from ingestion and storage to infrastructure and orchestration.

## Stack

| Area | Tools |
|---|---|
| Language | Python 3.13 |
| Package manager | uv |
| Containerization | Docker, Docker Compose |
| Database | PostgreSQL 18 |
| DB UI | pgAdmin 4 |
| Data processing | Pandas, PyArrow |
| Infrastructure | Terraform *(upcoming)* |

## What's been built

### Data Ingestion
- Script (`ingest_data.py`) that downloads NYC Yellow Taxi CSV data and loads it into PostgreSQL
- Chunked ingestion to handle large files without running out of memory
- CLI interface via Click — configurable host, port, credentials, year/month

### Infrastructure
- `Dockerfile` — containerizes the ingestion pipeline using Python slim + uv
- `docker-compose.yml` — spins up PostgreSQL + pgAdmin with persistent named volumes

### Exploration
- Jupyter notebook for initial data exploration and schema analysis

## Getting started

```bash
# Start the database and pgAdmin
docker compose up -d

# Run the ingestion pipeline
docker build -t taxi_ingest .
docker run --network=host taxi_ingest \
  --user=root --password=root --host=localhost --port=5432 \
  --db=ny_taxi --table_name=yellow_taxi_data --year=2021 --month=1
```

pgAdmin is available at `http://localhost:8085` (admin@admin.com / root).

## Roadmap

- [ ] Terraform for cloud infrastructure (GCP / AWS)
- [ ] Workflow orchestration (Airflow / Prefect)
- [ ] Data warehouse (BigQuery / Redshift)
- [ ] dbt for data transformation
- [ ] Data visualization
