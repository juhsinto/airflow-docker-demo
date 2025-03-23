
Setting up in docker - https://www.youtube.com/watch?v=aTaytcxy2Ck

Accuracies DAG example - https://www.youtube.com/watch?v=IH1-0hwFZRQ


Set up:
// initial set up
docker compose up airflow-init

Make sure enough memory:
`docker run --rm "debian:bookworm-slim" bash -c 'numfmt --to iec $(echo $(($(getconf _PHYS_PAGES) * $(getconf PAGE_SIZE))))'\n `

// make env file
echo -e "AIRFLOW_UID=$(id -u)\nAIRFLOW_GID=0" > .env

// start airflow
docker compose up

// check the services
docker ps

// check airflow version
docker exec 26e17224a6ea airflow version

// check if you can query the api without auth
curl -X GET "http://localhost:8080/api/v1/dags"

// check if you can query the api with auth
curl -X GET --user "airflow:airflow" http://localhost:8080/api/v1/dags"

Notes: 
- Tasks consist of operators
- There are several operators (Bash, Python, Postgres)
- The 'catchup' flag prevents running the DAG 'x' number of times between the start date and current date & only runs it from 'now' onwards according to the frequency.

![[dag_operation_graph.png]](screenshots/dag_operation_graph.png)