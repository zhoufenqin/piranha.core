# Assessment Overview

This directory contains supplementary analysis documents generated during the application assessment of **Piranha CMS v12.1.0** (solution: `Piranha.sln`). Each document provides a different architectural and operational perspective on the codebase.

## Supplementary Documents

| Document | Description |
|----------|-------------|
| [Architecture Diagram](./architecture-diagram.md) | Two-layer visual architecture showing the application layer structure (core, data, identity, manager, web API, examples) and component relationships including service dependencies and middleware pipeline. |
| [Dependency Map](./dependency-map.md) | NuGet package dependency map covering 17 external packages across 6 functional categories (ORM/database, media processing, cloud storage, identity, serialization, UI/framework) and 5 test-scoped packages. |
| [API & Service Contracts](./api-service-contracts.md) | Inventory of ~60+ HTTP endpoints across two API surfaces — the Manager back-office API (`/manager/api/`) and the Public Headless Web API (`/api/`) — with request/response formats and sequence diagram. |
| [Data Architecture](./data-architecture.md) | Entity-relationship diagram covering 35+ EF Core entities, repository query patterns, pluggable database backend design (SQLite, SQL Server, PostgreSQL, MySQL), caching strategy, and data classification (PII). |
| [Configuration Inventory](./configuration-inventory.md) | Comprehensive inventory of all configuration sources (appsettings.json, launchSettings.json, database-backed Params), build and runtime profiles, feature flags, secrets workflow, and framework/runtime versions. |
| [Business Workflows](./business-workflows.md) | End-to-end documentation of core business processes: content creation/publishing lifecycle, media upload and processing, URL alias management, comment moderation, and application startup/content-type registration. Includes Mermaid sequence diagram. |

## Key Findings Summary

- **Framework**: ASP.NET Core targeting **net8.0** (LTS) and **net9.0** (current); Piranha CMS v12.1.0
- **Architecture**: Single-process monolith with pluggable storage backends; no microservices or message queues
- **AppCAT Assessment**: 0 issues found — the project has no detected cloud-readiness concerns
- **API Surfaces**: Manager API (authenticated, XSRF-protected) + Public Headless REST API (optional anonymous access)
- **Data layer**: EF Core with 4 pluggable DB backends; IMemoryCache or IDistributedCache depending on deployment
- **Security**: ASP.NET Core Identity for authentication; granular policy-based authorization on all Manager endpoints
- **Upgrade opportunity**: Currently targets net8.0/net9.0; see the .NET upgrade assessment for net10.0 upgrade analysis
