# Configuration & Externalized Settings Inventory

Piranha CMS uses ASP.NET Core's built-in `appsettings.json` / `appsettings.{Environment}.json` configuration system with no external configuration server, secret manager, or feature-flag service; runtime parameters are loaded from JSON files and environment variables via the standard Microsoft.Extensions.Configuration pipeline.

## Configuration Sources

| Source | Type | Path/Location | Notes |
|--------|------|--------------|-------|
| appsettings.json | JSON config file | `examples/MvcWeb/appsettings.json` | Base configuration; connection strings, logging, AllowedHosts |
| appsettings.json | JSON config file | `examples/RazorWeb/appsettings.json` | Identical structure to MvcWeb |
| appsettings.Development.json | JSON config file | `examples/MvcWeb/appsettings.Development.json` | Development log-level overrides only |
| appsettings.Development.json | JSON config file | `examples/RazorWeb/appsettings.Development.json` | Development log-level overrides only |
| launchSettings.json | IDE/launch profile | `examples/RazorWeb/Properties/launchSettings.json` | Sets `ASPNETCORE_ENVIRONMENT=Development`; local dev only, not deployed |
| editorconfig.json | TinyMCE config | `examples/MvcWeb/editorconfig.json`, `examples/RazorWeb/editorconfig.json` | Loaded at runtime by `EditorConfig.FromFile()`; configures TinyMCE plugins and toolbar |
| Piranha Params (DB) | Database-backed params | `Piranha_Params` table | Runtime CMS configuration (cache TTLs, comment settings, manager preferences) stored as key/value pairs in the database |
| Environment Variables | OS/container env | Runtime | `ASPNETCORE_ENVIRONMENT`, `ConnectionStrings__piranha`, `ConnectionStrings__blobstorage` |

No Spring Cloud Config, Azure App Configuration, HashiCorp Vault, Azure KeyVault, AWS Secrets Manager, or other external configuration server is used.

## Build Profiles

| Profile | Activation | Purpose | Key Dependencies/Plugins |
|---------|-----------|---------|--------------------------|
| Debug | Default in IDE / `dotnet build` | Development build; no optimization; debug symbols included | `<GenerateDocumentationFile>` enabled; no AOT |
| Release | `-c Release` / CI pipeline | Production build; optimized; documentation XML generated | `<ContinuousIntegrationBuild>true` enabled on GitHub Actions (`GITHUB_ACTIONS=true`) |
| net8.0 TFM | `<TargetFrameworks>net8.0` | .NET 8.0 LTS target; selects net8.0-versioned NuGet package variants | EFCore 8.0.x packages, Extensions 8.0.x |
| net9.0 TFM | `<TargetFrameworks>net9.0` | .NET 9.0 current target; selects net9.0-versioned NuGet package variants | EFCore 9.0.x packages, Extensions 9.0.x |

## Runtime Profiles

| Profile | Activation Method | Config Files Loaded | Key Overrides |
|---------|-----------------|---------------------|--------------|
| Development | `ASPNETCORE_ENVIRONMENT=Development` (via launchSettings.json or env var) | `appsettings.json` → `appsettings.Development.json` | Log level `Default=Information`, `Microsoft=Warning` (same as base; no functional difference) |
| Production | `ASPNETCORE_ENVIRONMENT=Production` (default when not set) | `appsettings.json` only (no `appsettings.Production.json` present) | Same settings as base; connection strings must be overridden via environment variables |
| Custom (any) | Set `ASPNETCORE_ENVIRONMENT=<name>` | `appsettings.json` → `appsettings.<name>.json` (if present) | Standard ASP.NET Core layered config merging |

> Note: No `appsettings.Production.json` or `appsettings.Staging.json` files exist in the repository. Production deployments must override `ConnectionStrings:piranha` and any secrets via environment variables or a secrets manager configured by the host.

## Properties Inventory

### MvcWeb / RazorWeb (Example Applications)

| Property Key | Default Value | Profile | Source |
|-------------|--------------|---------|--------|
| `Logging:LogLevel:Default` | `Information` | All | appsettings.json |
| `Logging:LogLevel:Microsoft` | `Warning` | All | appsettings.json |
| `Logging:LogLevel:Microsoft.Hosting.Lifetime` | `Information` | All | appsettings.json |
| `AllowedHosts` | `*` | All | appsettings.json |
| `ConnectionStrings:piranha` | `Filename=./piranha.db` | All | appsettings.json / env var override |
| `ConnectionStrings:blobstorage` | `DefaultEndpointsProtocol=https;AccountName=;AccountKey=;EndpointSuffix=` | All | appsettings.json / env var override |

### Piranha Runtime Parameters (Database-Backed, `Piranha_Params` Table)

| Param Key | Default Value | Type | Purpose |
|-----------|-------------|------|---------|
| `ArchivePageSize` | `0` (unlimited) | int | Number of posts per archive page |
| `CacheExpiresPages` | `0` (no expiry) | int | Page cache TTL in minutes |
| `CacheExpiresPosts` | `0` (no expiry) | int | Post cache TTL in minutes |
| `CommentsApprove` | `true` | bool | Auto-approve submitted comments |
| `CommentsPageSize` | `0` | int | Comments per page |
| `CommentsPostsEnabled` | `true` | bool | Enable comments on posts |
| `CommentsPagesEnabled` | `false` | bool | Enable comments on pages |
| `CommentsCloseAfterDays` | `0` (never) | int | Days after publish before comments close |
| `HtmlExcerpt` | `false` | bool | Render excerpts as HTML |
| `MediaCdnUrl` | `""` | string | CDN base URL for media assets |
| `ManagerExpandedSitemapLevels` | `0` | int | Manager sitemap auto-expand depth |
| `ManagerPageSize` | `0` | int | Manager list pagination size |
| `ManagerDefaultCollapsedBlocks` | `false` | bool | Collapse content blocks by default |
| `ManagerDefaultCollapsedBlockGroupHeaders` | `false` | bool | Collapse block group headers by default |
| `ManagerOutlined` | `false` | bool | Enable outlined manager UI style |
| `ManagerXhrTimeout` | `0` | int | XHR timeout in ms for manager API calls |
| `HierarchicalPageSlugs` | `true` | bool | Include parent slug in child page URL |
| `PageRevisions` | `0` (unlimited) | int | Max page revision history depth |
| `PostRevisions` | `0` (unlimited) | int | Max post revision history depth |

### Piranha Manager Options (Code-Configured)

| Option | Default Value | Configured In |
|--------|-------------|--------------|
| `XsrfCookieName` | `XSRF-REQUEST-TOKEN` | `ManagerOptions` class |
| `XsrfHeaderName` | `X-XSRF-TOKEN` | `ManagerOptions` class |
| `JsonOptions` | null | `ManagerOptions` class; override via `AddPiranha` |

### Piranha Routing Options (Code-Configured)

| Option | Default Value | Configured In |
|--------|-------------|--------------|
| `UseAliasRouting` | `true` | `RoutingOptions` class |
| `UseArchiveRouting` | `true` | `RoutingOptions` class |
| `UsePageRouting` | `true` | `RoutingOptions` class |
| `UsePostRouting` | `true` | `RoutingOptions` class |
| `UseSiteRouting` | `true` | `RoutingOptions` class |
| `UseSitemapRouting` | `true` | `RoutingOptions` class |
| `UseStartpageRouting` | `true` | `RoutingOptions` class |

### Piranha Web API Options (Code-Configured)

| Option | Default Value | Configured In |
|--------|-------------|--------------|
| `AllowAnonymousAccess` | `false` | `WebApiOptions` class |

## Startup Parameters & Resource Requirements

| Service | Runtime Options | Memory | Instance Count |
|---------|----------------|--------|---------------|
| MvcWeb (example) | `ASPNETCORE_ENVIRONMENT=Development` (dev) | Not specified | 1 (single-process) |
| RazorWeb (example) | `ASPNETCORE_ENVIRONMENT=Development` (dev); listens on `https://localhost:5001;http://localhost:5000` | Not specified | 1 (single-process) |
| Library packages (Piranha.*) | No startup params; embedded in host | Not applicable | N/A |

No JVM heap settings, Docker `mem_limit`, Kubernetes `resources.requests/limits`, or instance scaling configurations are defined in the repository. These must be set by the consuming host application or deployment pipeline.

## Startup Dependency Chain

Piranha CMS is a **single-process** library framework — all components start within one ASP.NET Core application startup sequence:

1. **`builder.AddPiranha()`** — registers all Piranha services into the DI container (services, repositories, EF Core DbContext)
2. **DbContext constructor** — on first request to the DbContext, `Database.Migrate()` is called (guarded by a static mutex). This blocks startup until all EF Core migrations complete
3. **`Seed()`** — runs immediately after migrations to seed default Language and Param records
4. **`app.UsePiranha()`** — configures middleware pipeline, initializes `App.Init(api)` to load content types and app configuration from the database
5. **`ContentTypeBuilder.Build()`** — scans host assembly for `[PageType]`/`[PostType]` attributes and registers them with the CMS API

There are no inter-service TCP wait mechanisms, health check probes, `dockerize` patterns, or Kubernetes readiness probes defined in the framework itself. The host application is responsible for configuring health checks if needed.

## Secrets & Sensitive Configuration

| Secret Reference | Type | Storage |
|----------------|------|---------|
| `ConnectionStrings:piranha` | Database connection string | appsettings.json (plaintext for dev SQLite); **must be overridden** via environment variable (`ConnectionStrings__piranha`) or secrets manager in production |
| `ConnectionStrings:blobstorage` | Azure Blob Storage connection string (AccountKey) | appsettings.json — **currently empty/placeholder**; must be populated via env var or secrets manager |
| ASP.NET Core Identity password hash | PBKDF2 password hash | Stored in `AspNetUsers.PasswordHash` column — never in config files |

### Secrets Provisioning Workflow

Piranha CMS does not include a built-in secrets management integration. The expected provisioning workflow for production deployments is:

1. **Development**: Connection strings are stored as plaintext in `appsettings.json` (SQLite file path); no actual credentials needed
2. **Production**: Connection strings must be injected via OS environment variables using ASP.NET Core's double-underscore separator convention (`ConnectionStrings__piranha=Server=...;User=...;****** This overrides the appsettings.json values at runtime
3. **Cloud deployments**: Recommended approach is to use Azure App Service Connection Strings, Azure KeyVault with managed identity, or AWS Secrets Manager — none of which are pre-configured in the repository
4. **No encryption**: No Jasypt, DPAPI protected config, or `dotnet user-secrets` encryption is used in the example projects

The `blobstorage` connection string is a placeholder in `appsettings.json` with empty `AccountName` and `AccountKey` values and **must never be committed with real credentials**.

## Feature Flags

| Flag / Option | Default | Controlled By | Notes |
|--------------|---------|--------------|-------|
| `RoutingOptions.UseAliasRouting` | `true` | Code (`UsePiranha` options lambda) | Disabling skips URL alias resolution middleware |
| `RoutingOptions.UseArchiveRouting` | `true` | Code | Disabling skips post archive routing |
| `RoutingOptions.UsePageRouting` | `true` | Code | Disabling skips page URL resolution |
| `RoutingOptions.UsePostRouting` | `true` | Code | Disabling skips post URL resolution |
| `RoutingOptions.UseSiteRouting` | `true` | Code | Disabling skips multi-site hostname resolution |
| `RoutingOptions.UseSitemapRouting` | `true` | Code | Disabling skips `/sitemap.xml` serving |
| `WebApiOptions.AllowAnonymousAccess` | `false` | Code (`UseWebApi` options lambda) | When `true`, public API endpoints require no authentication |
| `AddRazorRuntimeCompilation` | `false` | `PiranhaServiceBuilder` | Enables hot-reload of `.cshtml` files without restart (dev only) |
| `CommentsApprove` (Param) | `true` | Manager UI / DB | Auto-approve comments without moderation |
| `CommentsPostsEnabled` (Param) | `true` | Manager UI / DB | Enable comment form on posts |
| `CommentsPagesEnabled` (Param) | `false` | Manager UI / DB | Enable comment form on pages |
| `HierarchicalPageSlugs` (Param) | `true` | Manager UI / DB | Include parent page slug in child URL |

No LaunchDarkly, Unleash, `Microsoft.FeatureManagement`, or other feature-flag SDK is used. Feature flags are either code-level options (set at startup) or database-backed `Piranha_Params` entries (configurable via Manager UI at runtime).

## Framework & Runtime Versions

| Component | Version | Source |
|-----------|---------|--------|
| .NET Runtime | 8.0 (LTS) and 9.0 (Current) | `Directory.Build.props` `<TargetFrameworks>net8.0;net9.0</TargetFrameworks>` |
| ASP.NET Core | 8.0 / 9.0 | `<FrameworkReference Include="Microsoft.AspNetCore.App" />` |
| Entity Framework Core | 8.0.0 (net8.0) / 9.0.0 (net9.0) | `*.csproj` EFCore package references |
| EFCore.Sqlite | 8.0.0 / 9.0.0 | `Piranha.Data.EF.SQLite.csproj` |
| EFCore.SqlServer | 8.0.0 / 9.0.0 | `Piranha.Data.EF.SQLServer.csproj` |
| Npgsql.EFCore.PostgreSQL | 8.0.11 / 9.0.4 | `Piranha.Data.EF.PostgreSql.csproj` |
| Pomelo.EFCore.MySql | 8.0.3 / 9.0.0 | `Piranha.Data.EF.MySql.csproj` |
| ASP.NET Core Identity | 8.0.0 / 9.0.0 | `Piranha.AspNetCore.Identity.csproj` |
| AutoMapper | 12.0.1 | `Piranha.Data.EF.csproj` |
| Markdig | 0.40.0 | `Piranha.csproj` |
| Newtonsoft.Json | 13.0.3 | `Piranha.csproj` |
| Mvc.NewtonsoftJson | 8.0.0 / 9.0.2 | `Piranha.Manager.csproj` |
| Mvc.Razor.RuntimeCompilation | 8.0.0 / 9.0.2 | `Piranha.AspNetCore.csproj` |
| SixLabors.ImageSharp | 2.1.13 | `Piranha.ImageSharp.csproj` |
| Azure.Storage.Blobs | 12.18.0 | `Piranha.Azure.BlobStorage.csproj` |
| Microsoft.Extensions.Localization | 8.0.0 / 9.0.2 | `Piranha.Manager.Localization.csproj` |
| X.Web.Sitemap | 2.10.1 | `Piranha.AspNetCore.csproj` |
| xunit | 2.7.0 | Test projects |
| Microsoft.NET.Test.Sdk | 17.9.0 | Test projects |
| coverlet | 6.0.2 | Test projects |
| Piranha CMS (solution) | 12.1.0 | `Directory.Build.props` `<Version>12.1.0</Version>` |
