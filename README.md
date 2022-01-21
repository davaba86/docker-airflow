# Docker Airflow

## Up and Running

### Requirements

Allow at least 4 GB memory to Docker or preferable 6 GB in the settings.

Docker -> Settings -> Resources -> Memory

Once settings are changed and applied, Docker VM will restart automatically.

### Setup Environment

```bash
curl -LfO 'https://airflow.apache.org/docs/apache-airflow/2.2.3/docker-compose.yaml'
mkdir dags logs plugins
echo -e "AIRFLOW_UID=$(id -u)\nAIRFLOW_GID=0" > .env
```

```bash
docker-compose up airflow-init
```

```bash
airflow-init_1       | User "airflow" created with role "Admin"
airflow-init_1       | 2.2.3
docker-airflow_airflow-init_1 exited with code 0
```

```bash
docker-compose up
```

Visit [localhost:8080](localhost:8080) on your web browser.

### Cleanup

```bash
docker-compose down --volumes --remove-orphans
rm docker-compose.yaml
rm -rf dags logs plugins .env
```

### Additional Information

<https://airflow.apache.org/docs/apache-airflow/stable/start/docker.html>

## Usage

### API

Ensure that `AIRFLOW__API__AUTH_BACKEND: 'airflow.api.auth.backend.basic_auth'` is defined as and env var.

```bash
curl -X GET --user "airflow:airflow" "http://localhost:8080/api/v1/dags"
```
