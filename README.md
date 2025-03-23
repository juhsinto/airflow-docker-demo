
# Airflow Docker Setup Guide

## Video Resources
- [Setting up Airflow in Docker](https://www.youtube.com/watch?v=aTaytcxy2Ck)
- [Accuracies DAG Example](https://www.youtube.com/watch?v=IH1-0hwFZRQ)

## Setup Steps

### Initial Setup
1. Initialize Airflow:
   ```bash
   docker compose up airflow-init
   ```

2. Check available memory:
   ```bash
   docker run --rm "debian:bookworm-slim" bash -c 'numfmt --to iec $(echo $(($(getconf PHYSPAGES) * $(getconf PAGE_SIZE))))'
   ```

3. Create environment file:
   ```bash
   echo -e "AIRFLOW_UID=$(id -u)\nAIRFLOW_GID=0" > .env
   ```

4. Start Airflow:
   ```bash
   docker compose up
   ```

### Verification

1. Check running services:
   ```bash
   docker ps
   ```

2. Verify Airflow version:
   ```bash
   docker exec <container_id> airflow version
   ```

3. Test API access without authentication:
   ```bash
   curl -X GET "http://localhost:8080/api/v1/dags"
   ```

4. Test API access with authentication:
   ```bash
   curl -X GET --user "airflow:airflow" "http://localhost:8080/api/v1/dags"
   ```
Notes: 
- Tasks consist of operators
- There are several operators (Bash, Python, Postgres)
- The 'catchup' flag prevents running the DAG 'x' number of times between the start date and current date & only runs it from 'now' onwards according to the frequency.

![[dag_operation_graph.png]](screenshots/dag_operation_graph.png)
