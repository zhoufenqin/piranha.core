# MvcWeb

## Summary

| Metric | Value |
|--------|-------|
| Total Issues | 6 |
| Mandatory Blockers | 1 |
| Potential Issues | 3 |

## Component Information

| Property | Value |
|----------|-------|
| Language | C# |
| Frameworks | net8.0, net9.0 |
| Build tools | MSBuild |

## DotNET Upgrade Issues [View Details](scenarios/dotnet-version-upgrade/assessment.md)

| Issue Category | Criticality | Story Points | Occurrences |
|----------------|-------------|--------------|-------------|
| Project's target framework(s) needs to be changed | Mandatory | 1 | [26](#Project_s_target_framework_s_needs_to_be_changed) |
| Behavioral change in selected .NET version | Potential | 1 | [11](#Behavioral_change_in_selected_NET_version) |
| Source incompatible for selected .NET version | Potential | 1 | [6](#Source_incompatible_for_selected_NET_version) |
| NuGet package upgrade is recommended | Potential | 1 | [1](#NuGet_package_upgrade_is_recommended) |
| NuGet package is deprecated | Optional | 1 | [2](#NuGet_package_is_deprecated) |
| NuGet package contains security vulnerability | Optional | 1 | [1](#NuGet_package_contains_security_vulnerability) |

### Issue Details

<details id="Project_s_target_framework_s_needs_to_be_changed">
<summary><b>Project's target framework(s) needs to be changed</b> — affected files</summary>

- `examples\MvcWeb\MvcWeb.csproj`
- `core\Piranha.AspNetCore\Piranha.AspNetCore.csproj`
- `core\Piranha.AspNetCore.Hosting\Piranha.AspNetCore.Hosting.csproj`
- `identity\Piranha.AspNetCore.Identity\Piranha.AspNetCore.Identity.csproj`
- `identity\Piranha.AspNetCore.Identity.MySQL\Piranha.AspNetCore.Identity.MySQL.csproj`
- `identity\Piranha.AspNetCore.Identity.PostgreSQL\Piranha.AspNetCore.Identity.PostgreSQL.csproj`
- `identity\Piranha.AspNetCore.Identity.SQLite\Piranha.AspNetCore.Identity.SQLite.csproj`
- `identity\Piranha.AspNetCore.Identity.SQLServer\Piranha.AspNetCore.Identity.SQLServer.csproj`
- `core\Piranha.AttributeBuilder\Piranha.AttributeBuilder.csproj`
- `core\Piranha.Azure.BlobStorage\Piranha.Azure.BlobStorage.csproj`
- `core\Piranha\Piranha.csproj`
- `data\Piranha.Data.EF\Piranha.Data.EF.csproj`
- `data\Piranha.Data.EF.MySql\Piranha.Data.EF.MySql.csproj`
- `data\Piranha.Data.EF.PostgreSql\Piranha.Data.EF.PostgreSql.csproj`
- `data\Piranha.Data.EF.SQLite\Piranha.Data.EF.SQLite.csproj`
- `data\Piranha.Data.EF.SQLServer\Piranha.Data.EF.SQLServer.csproj`
- `core\Piranha.ImageSharp\Piranha.ImageSharp.csproj`
- `core\Piranha.Local.FileStorage\Piranha.Local.FileStorage.csproj`
- `core\Piranha.Manager\Piranha.Manager.csproj`
- `core\Piranha.Manager.LocalAuth\Piranha.Manager.LocalAuth.csproj`
- `core\Piranha.Manager.Localization\Piranha.Manager.Localization.csproj`
- `test\Piranha.Manager.Tests\Piranha.Manager.Tests.csproj`
- `core\Piranha.Manager.TinyMCE\Piranha.Manager.TinyMCE.csproj`
- `test\Piranha.Tests\Piranha.Tests.csproj`
- `core\Piranha.WebApi\Piranha.WebApi.csproj`
- `examples\RazorWeb\RazorWeb.csproj`

</details>

<details id="Behavioral_change_in_selected_NET_version">
<summary><b>Behavioral change in selected .NET version</b> — affected files</summary>

- `core\Piranha.AspNetCore\Http\SitemapMiddleware.cs (line 118, col 20)`
- `core\Piranha.AspNetCore\Http\SitemapMiddleware.cs (line 103, col 12)`
- `core\Piranha.Azure.BlobStorage\BlobStorage.cs (line 138, col 8)`
- `core\Piranha.Azure.BlobStorage\BlobStorage.cs (line 79, col 8)`
- `core\Piranha.Azure.BlobStorage\BlobStorage.cs (line 39, col 4)`
- `core\Piranha.Azure.BlobStorage\Extensions\BlobStorageExtensions.cs (line 74, col 4)`
- `core\Piranha.Azure.BlobStorage\Extensions\BlobStorageExtensions.cs (line 29, col 4)`
- `core\Piranha\Extend\Fields\SelectField.cs (line 86, col 8)`

</details>

<details id="Source_incompatible_for_selected_NET_version">
<summary><b>Source incompatible for selected .NET version</b> — affected files</summary>

- `core\Piranha.AspNetCore\Http\RoutingMiddleware.cs (line 496, col 12)`
- `core\Piranha.AspNetCore\Extensions\PiranhaStartupExtensions.cs (line 36, col 12)`
- `identity\Piranha.AspNetCore.Identity\Extensions\IdentityModuleExtensions.cs (line 200, col 8)`
- `identity\Piranha.AspNetCore.Identity\Extensions\IdentityModuleExtensions.cs (line 185, col 8)`
- `identity\Piranha.AspNetCore.Identity\Extensions\IdentityModuleExtensions.cs (line 120, col 8)`

</details>

<details id="NuGet_package_upgrade_is_recommended">
<summary><b>NuGet package upgrade is recommended</b> — affected files</summary>

- `core\Piranha\Piranha.csproj`

</details>

<details id="NuGet_package_is_deprecated">
<summary><b>NuGet package is deprecated</b> — affected files</summary>

- `test\Piranha.Manager.Tests\Piranha.Manager.Tests.csproj`
- `test\Piranha.Tests\Piranha.Tests.csproj`

</details>

<details id="NuGet_package_contains_security_vulnerability">
<summary><b>NuGet package contains security vulnerability</b> — affected files</summary>

- `data\Piranha.Data.EF\Piranha.Data.EF.csproj`

</details>

---

## Codebase Insights

> **Note:** These documents are generated by AI and may contain inaccuracies or incomplete information. Please review carefully.

1. **[Architecture Diagram](facts/architecture-diagram.md)** — Understand the big picture: system layers and component relationships
2. **[Dependency Map](facts/dependency-map.md)** — Know what the project depends on and where the risks are
3. **[API & Service Contracts](facts/api-service-contracts.md)** — See how services communicate and what contracts they expose
4. **[Data Architecture](facts/data-architecture.md)** — Explore data models, storage, and data flow patterns
5. **[Configuration Inventory](facts/configuration-inventory.md)** — Review how the application is configured across environments
6. **[Business Workflows](facts/business-workflows.md)** — Trace end-to-end business processes and domain logic

[Share feedback](https://aka.ms/ghcp-appmod/feedback)
