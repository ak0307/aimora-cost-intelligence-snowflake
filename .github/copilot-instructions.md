# AIMORA repository instructions

You are working in the AIMORA Cost Intelligence monorepo.

## Product context
AIMORA is a Snowflake-first enterprise cost intelligence and optimization platform.
Primary goal: reduce Snowflake spend through telemetry ingestion, attribution, anomaly detection, and actionable recommendations.

## Repository structure
- `snowflake/ddl/` contains all DDL.
- `snowflake/procedures/` contains Snowflake stored procedures.
- `snowflake/tasks/` contains the task DAG.
- `snowflake/seeds/` contains rule seed/config SQL.
- `bootstrap/` contains installation and validation runners.
- `apps/api/` contains the FastAPI backend.
- `apps/web/` contains the Next.js frontend.
- `control_plane/sql/` contains Postgres control-plane schema.
- `scripts/` contains deployment and validation helpers.
- `docs/` contains architecture, runbooks, and install docs.

## Hard rules
- Never rename Snowflake objects unless explicitly asked.
- Never move bootstrap files without updating `bootstrap/run_all.sql`.
- Prefer additive changes over destructive changes.
- Keep all SQL idempotent where possible.
- Use overlap + MERGE for Snowflake raw telemetry loads.
- All Snowflake tasks and procedures must run on `AIMORA_APP_WH`.
- Exclude `AIMORA_APP_WH` and `AIMORA_APP_ROLE` from waste/anomaly rules except app-cost transparency features.
- Keep recommendations explainable and deterministic.
- Do not introduce LLM dependencies into the Snowflake layer.
- Keep environment secrets out of the repo.

## Coding standards
- Python: small service functions, typed responses, explicit error handling.
- SQL: readable CTEs, no implicit business logic hidden in nested subqueries unless necessary.
- TypeScript: strongly type API responses, avoid any.
- Write comments only when they clarify non-obvious logic.
- Preserve API backward compatibility where practical.

## Validation expectations
Before proposing changes, consider:
- Does bootstrap still run in order?
- Does validation still pass?
- Does the task DAG still reflect dependency order?
- Does the change preserve enterprise RBAC semantics?

## Preferred workflow
1. Make minimal code changes.
2. Update docs when behavior changes.
3. Suggest validation steps after major changes.