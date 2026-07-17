# Workflows & Commands Cheat-Sheet

A collection of copy-pasteable shell commands for compilation, testing, and linting.

## Gradle & Kotlin Connectors (Bulk CDK)

All JVM/Kotlin connectors and the Bulk CDK are managed via Gradle. Execute commands from the repository root.

### 1. Build and Compile
- Build entire project (excluding tests):
  ```bash
  ./gradlew build -x test
  ```
- Build a specific connector (e.g., Clickhouse):
  ```bash
  ./gradlew :airbyte-integrations:connectors:destination-clickhouse:build -x test
  ```
- Build the Bulk CDK base module:
  ```bash
  ./gradlew :airbyte-cdk:bulk:core:base:build
  ```

### 2. Testing
- Run Unit/Component Tests (using Testcontainers where configured):
  ```bash
  ./gradlew :airbyte-integrations:connectors:destination-clickhouse:test
  ```
- Run Integration Tests (verifies DI, write initialization):
  ```bash
  ./gradlew :airbyte-integrations:connectors:destination-clickhouse:integrationTest
  ```

### 3. Formatting
- Format Kotlin code automatically with Spotless:
  ```bash
  ./gradlew spotlessApply
  ```

---

## Python Connectors

Python connectors use Poetry. Change directory to the target connector folder before running commands.

### 1. Installation
  ```bash
  poetry install
  ```

### 2. Running Tests
  ```bash
  poetry run pytest unit_tests
  poetry run pytest integration_tests
  ```

### 3. Formatting & Linting
  ```bash
  poetry run ruff format .
  poetry run ruff check . --fix
  ```

---

## Docker Workflows

To verify how the platform executes a connector:

### 1. Build Docker Image
  ```bash
  ./gradlew :airbyte-integrations:connectors:destination-clickhouse:airbyteDocker
  ```

### 2. Test Connector Cột mốc (`--spec`, `--check`, `--write`)
- Run Spec:
  ```bash
  docker run --rm airbyte/destination-clickhouse:dev --spec
  ```
- Run Check (with a local `config.json` mounted):
  ```bash
  docker run --rm -v $(pwd)/secrets:/secrets airbyte/destination-clickhouse:dev --check --config /secrets/config.json
  ```
- Run Write (verifies streaming record ingestion using configuration and catalog):
  ```bash
  # Run Write (verifies streaming record ingestion using configuration and catalog)
  docker run --rm -v $(pwd)/secrets:/secrets -v $(pwd)/integration_tests:/integration_tests airbyte/destination-clickhouse:dev --write --config /secrets/config.json --catalog /integration_tests/configured_catalog.json
  ```

---

## Staging CI/CD Pipeline

The repository includes an automated staging pipeline configured for GitHub Actions and Docker Hub.

### 1. Triggering Deployment
- Push or merge changes into the **`staging`** branch.
- This triggers `.github/workflows/deploy-staging.yml` which builds the target connector, publishes the image to Docker Hub tagged as `:staging`, and logs into the staging VPS via SSH to run a pulling restart.

### 2. VPS Setup (Traefik-Integrated)
- The staging VPS runs Traefik, Portainer, and Docker.
- To configure the connector container stack on the VPS, use the template at [docker-compose.staging.yml](../../docker-compose.staging.yml) which integrates automatically with the Traefik public load-balancer.
