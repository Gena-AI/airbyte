# AI Agent Documentation System Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Create a high-density, AI-optimized documentation system containing `AI.md` at the root and four supporting files in `docs/ai/` to orient, guide, and instruct AI coding agents working on the Gena-AI/airbyte repository.

**Architecture:** A lightweight, single-entry router file (`AI.md` at the root) directing agents to specific high-density cheat sheets (`docs/ai/*`) based on their task. These sheets provide exact file paths, copy-pasteable commands, architectural Kotlin CDK mental models, and strict coding and PR rules.

**Tech Stack:** Markdown, Git, Mermaid diagrams, Shell commands, Kotlin/Bulk CDK (Micronaut), Python.

## Global Constraints
- **No Placeholders:** Avoid any "TBD", "TODO", or vague descriptions. All code blocks, file paths, and commands must be exact and operational.
- **Tone & Style:** Minimal prose, direct instruction, maximum concentration of syntax, paths, and diagrams.
- **Repository Integrity:** Follow the existing project structure and Kotlin/Python tools exactly.

---

### Task 1: Create `AI.md` at Repository Root

**Files:**
- Create: `AI.md`

**Interfaces:**
- Consumes: None (main entry point)
- Produces: Quick navigation matrix and core guardrails for future AI agent sessions.

- [ ] **Step 1: Write the entry-point router file `/AI.md`**

Write the following content to the root `AI.md` file:
```markdown
# AI Agent Workspace Entry Point

Welcome, AI Agent. This is the `Gena-AI/airbyte` repository (a high-performance fork of Airbyte). 
To optimize your performance, minimize token usage, and prevent errors, use this quick router map to load the correct documentation for your current task.

## Quick Navigation Matrix

| Task / Intent | Target File | What You Will Find |
| :--- | :--- | :--- |
| Find files, understand repository structure | [codebase-map.md](file:///Users/quocnguyen/4_projects/1connector/airbyte/docs/ai/codebase-map.md) | Trimmed directory tree and explanation of core modules. |
| Build, run, test, or lint connectors | [workflows.md](file:///Users/quocnguyen/4_projects/1connector/airbyte/docs/ai/workflows.md) | Copy-pasteable shell commands for Gradle, Python, and Docker. |
| Code or modify Kotlin/Java Bulk Destination Connectors | [bulk-cdk-guide.md](file:///Users/quocnguyen/4_projects/1connector/airbyte/docs/ai/bulk-cdk-guide.md) | Sơ đồ luồng, core interface, DI rules, and testing environments. |
| Review styling, exception handling, and PR guidelines | [standards-and-rules.md](file:///Users/quocnguyen/4_projects/1connector/airbyte/docs/ai/standards-and-rules.md) | Airbyte coding rules, security guidelines, and PR checkpoints. |

## Core Workspace Guardrails

1. **Check for Skills:** Always run a skill check before any implementation step or answering clarifying questions.
2. **Follow Existing Patterns:** Follow existing patterns in the directory you are working in. Do not refactor unrelated code.
3. **No Placeholders:** Never output `TODO` or `TBD` in your code edits. Write clean, complete, functional implementations.
4. **Preserve Comments:** Keep all original comments and docstrings intact unless explicitly requested to change them.
```

- [ ] **Step 2: Verify file creation**

Run: `ls -la AI.md`
Expected: File exists and has size > 500 bytes.

- [ ] **Step 3: Commit**

```bash
git add AI.md
git commit -m "docs(ai): create root AI.md router"
```

---

### Task 2: Create `docs/ai/codebase-map.md` (Codebase Map)

**Files:**
- Create: `docs/ai/codebase-map.md`

**Interfaces:**
- Consumes: `/AI.md`
- Produces: Precise physical layout mapping of the repository for AI agents.

- [ ] **Step 1: Write the codebase map document**

Write the following content to `docs/ai/codebase-map.md`:
```markdown
# Codebase Map for AI Agents

Use this map to instantly locate source files, CDK implementations, and developer guides.

## Trimmed Directory Structure

```
airbyte/
├── AI.md                                    # AI entry-point router
├── airbyte-cdk/                             # Connector Development Kits (CDK)
│   ├── java/                                # Legacy Java CDK
│   ├── python/                              # Python Source/Destination CDK
│   └── bulk/                                # High-performance Kotlin Bulk CDK (Core & Toolkits)
│       ├── core/                            # Micronaut-based core engines (base, extract, load)
│       └── toolkits/                        # Shared utility modules (e.g. extract-jdbc)
├── airbyte-integrations/
│   └── connectors/                          # Source and Destination Connectors
│       ├── source-github/                   # Example Python source connector
│       ├── destination-clickhouse/          # Example Kotlin Bulk destination connector
│       └── destination-snowflake/           # Example Kotlin Bulk destination connector
├── connector-writer/
│   └── destination/                         # Step-by-step guides for writing destination connectors
│       └── step-by-step/                    # 0-introduction.md to 8-validation.md Kotlin guides
└── docs/
    └── ai/                                  # This directory (AI-specific documentation)
```

## Core Module Explanations

### 1. Bulk CDK (`airbyte-cdk/bulk/`)
- Written in Kotlin and powered by the **Micronaut framework** for Dependency Injection.
- Separated into three primary modules:
  - `core/base/`: Fundamental classes shared across extract and load.
  - `core/extract/`: Engine for high-performance source extraction.
  - `core/load/`: Engine for high-performance destination loading (referred to as the Dataflow CDK).

### 2. Connectors (`airbyte-integrations/connectors/`)
- Contains all connectors. Kotlin Bulk connectors are prefixed with `destination-` (e.g., `destination-clickhouse`, `destination-snowflake`) and are structured as Micronaut Gradle subprojects.
- Python connectors are standard Python packages using Poetry.

### 3. Developer Guides (`connector-writer/destination/`)
- A highly complete reference for writing Destination Connectors with the Dataflow CDK. Refer to these files when building new Kotlin connectors.
```

- [ ] **Step 2: Verify file creation**

Run: `ls -la docs/ai/codebase-map.md`
Expected: File exists and has size > 1000 bytes.

- [ ] **Step 3: Commit**

```bash
git add docs/ai/codebase-map.md
git commit -m "docs(ai): create codebase-map.md"
```

---

### Task 3: Create `docs/ai/workflows.md` (Workflows Cheat-Sheet)

**Files:**
- Create: `docs/ai/workflows.md`

**Interfaces:**
- Consumes: None
- Produces: Fast development command reference.

- [ ] **Step 1: Write the workflows file**

Write the following content to `docs/ai/workflows.md`:
```markdown
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
```

- [ ] **Step 2: Verify file creation**

Run: `ls -la docs/ai/workflows.md`
Expected: File exists and has size > 1500 bytes.

- [ ] **Step 3: Commit**

```bash
git add docs/ai/workflows.md
git commit -m "docs(ai): create workflows.md"
```

---

### Task 4: Create `docs/ai/bulk-cdk-guide.md` (Kotlin Bulk CDK Guide)

**Files:**
- Create: `docs/ai/bulk-cdk-guide.md`

**Interfaces:**
- Consumes: `connector-writer/destination/` step-by-step guides
- Produces: Core architecture map and testing definitions for Kotlin Bulk CDK.

- [ ] **Step 1: Write the Bulk CDK Guide file**

Write the following content to `docs/ai/bulk-cdk-guide.md`:
```markdown
# Kotlin Bulk CDK (Dataflow CDK) Architecture Guide

This guide condenses the mental model, component patterns, and dependency injection structures of the Kotlin Bulk CDK (located under `airbyte-cdk/bulk/`).

## Architecture & Data Flow

When executing a Destination Connector, the data flows as follows:

```
Platform → stdin → Lifecycle → Writer.setup()
                               → createStreamLoader()
                               → AggregateFactory.create()
                               → InsertBuffer
                               → Database
                               → StreamLoader.close()
                               → STATE → stdout → Platform
```

### Core Components

1. **`SqlGenerator`:**
   - **Role:** Pure functions responsible for translating metadata and data streams into database-specific SQL strings.
   - **Rule:** Keep SQL generation isolated here. Never do network I/O or handle raw connection sessions in the SqlGenerator. This makes it 100% testable via component tests.

2. **`TableOperationsClient`:**
   - **Role:** Low-level database client that physically creates schemas, tables, executes drop operations, and counts records.
   - **Rule:** Uses SQL statements generated by the `SqlGenerator` and wraps database exceptions nicely.

3. **`InsertBuffer`:**
   - **Role:** A memory-efficient, database-specific batching buffer that pools incoming records and flushes them in bulk.

4. **`StreamLoader`:**
   - **Role:** Coordinates table lifecycles (Append, Overwrite, Dedupe). Selects the correct loading pattern (e.g., Temp Table + Swap, Direct Insert, or Merge).

5. **`Writer`:**
   - **Role:** High-level orchestrator injecting and connecting the Client, StreamLoader, and Buffer together.

---

## Micronaut Dependency Injection (DI)

Bulk CDK uses Micronaut for DI. This prevents boilerplate code but requires strict adherence to rules:

### 1. Bean Registration
- Classes should be decorated with `@Singleton` (from `jakarta.inject.Singleton`).
- Interfaces that have database-specific implementations should be marked with `@Requires(property = "airbyte.connector-name", value = "clickhouse")` or similar qualifiers.

### 2. Custom Factory Pattern
- Use factory classes annotated with `@Factory` to instantiate third-party database drivers or complex connection pools.

---

## The Three Testing Contexts

When writing or modifying tests, identify the exact test context to avoid setup confusion:

1. **Component Tests (`test` directory):**
   - Tests individual classes (e.g., `SqlGeneratorTest`, `TableOperationsTest`).
   - Uses localized `Testcontainers` to verify SQL syntax and small table mutations without loading the full CDK machinery.

2. **Integration Tests (`integrationTest` directory):**
   - Verifies dependency injection and initialization flows.
   - Checks that the `Writer` can initialize correctly and stream empty payloads.

3. **Basic Functionality Tests (E2E):**
   - Extends `BasicFunctionalityIntegrationTest` and runs complete sync cycles across all supported modes (Append, Overwrite, Dedupe, Schema Evolution).
```

- [ ] **Step 2: Verify file creation**

Run: `ls -la docs/ai/bulk-cdk-guide.md`
Expected: File exists and has size > 1500 bytes.

- [ ] **Step 3: Commit**

```bash
git add docs/ai/bulk-cdk-guide.md
git commit -m "docs(ai): create bulk-cdk-guide.md"
```

---

### Task 5: Create `docs/ai/standards-and-rules.md` (Standards and Rules)

**Files:**
- Create: `docs/ai/standards-and-rules.md`

**Interfaces:**
- Consumes: None
- Produces: Coding standards, security rules, and PR requirements.

- [ ] **Step 1: Write the standards and rules file**

Write the following content to `docs/ai/standards-and-rules.md`:
```markdown
# Coding Standards & Pull Request Guidelines

This document details the quality gates, exception-handling protocols, and PR procedures.

## Code & Formatting Standards

### 1. Style Rules
- **Kotlin:** Spotless format is mandatory. Always run `./gradlew spotlessApply` before staging edits.
- **Python:** Ruff format is mandatory. Run `poetry run ruff format .` and `poetry run ruff check . --fix`.
- **Comments:** Do not delete existing comments unless they are explicitly obsolete. Preserve all original docstrings.

### 2. Strict Exception Translation
- Raw database connection exceptions (e.g., `SQLException`, `ConnectException`) must be caught and translated into user-friendly `ConfigErrorException` or `StateErrorException`.
- **Reason:** Raw exceptions can leak credentials, hostnames, and internal table definitions to stdout, which is a major security hazard.

---

## Pull Request Requirements

When submitting pull requests to `Gena-AI/airbyte` (or upstream):

1. **Allow Maintainer Edits:**
   - You **MUST** check the "Allow edits from maintainers" checkbox on your pull request. This allows formatting, dependencies, and Spotless fixes to be committed directly by reviewers, speeding up the PR lifecycle.

2. **Fork from Personal Account:**
   - Create the pull request from a fork under a **personal GitHub account**, not an organization account. GitHub's security model blocks maintainers from writing to forks owned by organizations.

---

## Avoid AI Anti-Patterns

- **Anti-pattern 1: Blind CDK upgrades.** Never change dependencies or CDK versions unless instructed. Keep gradle properties pinned.
- **Anti-pattern 2: Manual instantiation in DI.** Avoid instantiating classes annotated with `@Singleton` manually. Use `@Inject` constructor injection.
- **Anti-pattern 3: Large PRs.** Keep PRs bounded to a single connector or single component. Large files lead to merge conflicts.
```

- [ ] **Step 2: Verify file creation**

Run: `ls -la docs/ai/standards-and-rules.md`
Expected: File exists and has size > 1500 bytes.

- [ ] **Step 3: Commit**

```bash
git add docs/ai/standards-and-rules.md
git commit -m "docs(ai): create standards-and-rules.md"
```
