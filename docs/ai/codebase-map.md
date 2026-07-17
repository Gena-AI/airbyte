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
