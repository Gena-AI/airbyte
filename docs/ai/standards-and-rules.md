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
- **Anti-pattern 4: Overcomplicating database writes.** Do not write custom raw JDBC connections or standalone SQL executions inside a connector's ingestion flow. Always use the Bulk CDK-provided `StreamLoader`, `TableOperationsClient`, and `InsertBuffer` interfaces to manage writing lifecycles.
