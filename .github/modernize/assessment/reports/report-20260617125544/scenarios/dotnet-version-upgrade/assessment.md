# Projects and dependencies analysis

This document provides a comprehensive overview of the projects and their dependencies in the context of upgrading to .NETCoreApp,Version=v10.0.

## Table of Contents

- [Executive Summary](#executive-Summary)
  - [Highlevel Metrics](#highlevel-metrics)
  - [Projects Compatibility](#projects-compatibility)
  - [Package Compatibility](#package-compatibility)
  - [API Compatibility](#api-compatibility)
  - [Binding Redirect Configuration](#binding-redirect-configuration)
- [Aggregate NuGet packages details](#aggregate-nuget-packages-details)
- [Top API Migration Challenges](#top-api-migration-challenges)
  - [Technologies and Features](#technologies-and-features)
  - [Most Frequent API Issues](#most-frequent-api-issues)
- [Projects Relationship Graph](#projects-relationship-graph)
- [Project Details](#project-details)

  - [core\Piranha.AspNetCore.Hosting\Piranha.AspNetCore.Hosting.csproj](#corepiranhaaspnetcorehostingpiranhaaspnetcorehostingcsproj)
  - [core\Piranha.AspNetCore\Piranha.AspNetCore.csproj](#corepiranhaaspnetcorepiranhaaspnetcorecsproj)
  - [core\Piranha.AttributeBuilder\Piranha.AttributeBuilder.csproj](#corepiranhaattributebuilderpiranhaattributebuildercsproj)
  - [core\Piranha.Azure.BlobStorage\Piranha.Azure.BlobStorage.csproj](#corepiranhaazureblobstoragepiranhaazureblobstoragecsproj)
  - [core\Piranha.ImageSharp\Piranha.ImageSharp.csproj](#corepiranhaimagesharppiranhaimagesharpcsproj)
  - [core\Piranha.Local.FileStorage\Piranha.Local.FileStorage.csproj](#corepiranhalocalfilestoragepiranhalocalfilestoragecsproj)
  - [core\Piranha.Manager.LocalAuth\Piranha.Manager.LocalAuth.csproj](#corepiranhamanagerlocalauthpiranhamanagerlocalauthcsproj)
  - [core\Piranha.Manager.Localization\Piranha.Manager.Localization.csproj](#corepiranhamanagerlocalizationpiranhamanagerlocalizationcsproj)
  - [core\Piranha.Manager.TinyMCE\Piranha.Manager.TinyMCE.csproj](#corepiranhamanagertinymcepiranhamanagertinymcecsproj)
  - [core\Piranha.Manager\Piranha.Manager.csproj](#corepiranhamanagerpiranhamanagercsproj)
  - [core\Piranha.WebApi\Piranha.WebApi.csproj](#corepiranhawebapipiranhawebapicsproj)
  - [core\Piranha\Piranha.csproj](#corepiranhapiranhacsproj)
  - [data\Piranha.Data.EF.MySql\Piranha.Data.EF.MySql.csproj](#datapiranhadataefmysqlpiranhadataefmysqlcsproj)
  - [data\Piranha.Data.EF.PostgreSql\Piranha.Data.EF.PostgreSql.csproj](#datapiranhadataefpostgresqlpiranhadataefpostgresqlcsproj)
  - [data\Piranha.Data.EF.SQLite\Piranha.Data.EF.SQLite.csproj](#datapiranhadataefsqlitepiranhadataefsqlitecsproj)
  - [data\Piranha.Data.EF.SQLServer\Piranha.Data.EF.SQLServer.csproj](#datapiranhadataefsqlserverpiranhadataefsqlservercsproj)
  - [data\Piranha.Data.EF\Piranha.Data.EF.csproj](#datapiranhadataefpiranhadataefcsproj)
  - [examples\MvcWeb\MvcWeb.csproj](#examplesmvcwebmvcwebcsproj)
  - [examples\RazorWeb\RazorWeb.csproj](#examplesrazorwebrazorwebcsproj)
  - [identity\Piranha.AspNetCore.Identity.MySQL\Piranha.AspNetCore.Identity.MySQL.csproj](#identitypiranhaaspnetcoreidentitymysqlpiranhaaspnetcoreidentitymysqlcsproj)
  - [identity\Piranha.AspNetCore.Identity.PostgreSQL\Piranha.AspNetCore.Identity.PostgreSQL.csproj](#identitypiranhaaspnetcoreidentitypostgresqlpiranhaaspnetcoreidentitypostgresqlcsproj)
  - [identity\Piranha.AspNetCore.Identity.SQLite\Piranha.AspNetCore.Identity.SQLite.csproj](#identitypiranhaaspnetcoreidentitysqlitepiranhaaspnetcoreidentitysqlitecsproj)
  - [identity\Piranha.AspNetCore.Identity.SQLServer\Piranha.AspNetCore.Identity.SQLServer.csproj](#identitypiranhaaspnetcoreidentitysqlserverpiranhaaspnetcoreidentitysqlservercsproj)
  - [identity\Piranha.AspNetCore.Identity\Piranha.AspNetCore.Identity.csproj](#identitypiranhaaspnetcoreidentitypiranhaaspnetcoreidentitycsproj)
  - [test\Piranha.Manager.Tests\Piranha.Manager.Tests.csproj](#testpiranhamanagertestspiranhamanagertestscsproj)
  - [test\Piranha.Tests\Piranha.Tests.csproj](#testpiranhatestspiranhatestscsproj)


## Executive Summary

### Highlevel Metrics

| Metric | Count | Status |
| :--- | :---: | :--- |
| Total Projects | 26 | All require upgrade |
| Total NuGet Packages | 12 | 3 need upgrade |
| Total Code Files | 0 |  |
| Total Code Files with Incidents | 33 |  |
| Total Lines of Code | 0 |  |
| Total Number of Issues | 47 |  |
| Estimated LOC to modify | 17+ | at least 0.0% of codebase |

### Projects Compatibility

| Project | Target Framework | Difficulty | Package Issues | API Issues | Binding Issues | Est. LOC Impact | Description |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: | :--- |
| [core\Piranha.AspNetCore.Hosting\Piranha.AspNetCore.Hosting.csproj](#corepiranhaaspnetcorehostingpiranhaaspnetcorehostingcsproj) | net8.0;net9.0 | 🟢 Low | 0 | 0 | 0 |  | ClassLibrary, Sdk Style = True |
| [core\Piranha.AspNetCore\Piranha.AspNetCore.csproj](#corepiranhaaspnetcorepiranhaaspnetcorecsproj) | net8.0;net9.0 | 🟢 Low | 0 | 4 | 0 | 4+ | ClassLibrary, Sdk Style = True |
| [core\Piranha.AttributeBuilder\Piranha.AttributeBuilder.csproj](#corepiranhaattributebuilderpiranhaattributebuildercsproj) | net8.0;net9.0 | 🟢 Low | 0 | 0 | 0 |  | ClassLibrary, Sdk Style = True |
| [core\Piranha.Azure.BlobStorage\Piranha.Azure.BlobStorage.csproj](#corepiranhaazureblobstoragepiranhaazureblobstoragecsproj) | net8.0;net9.0 | 🟢 Low | 0 | 8 | 0 | 8+ | ClassLibrary, Sdk Style = True |
| [core\Piranha.ImageSharp\Piranha.ImageSharp.csproj](#corepiranhaimagesharppiranhaimagesharpcsproj) | net8.0;net9.0 | 🟢 Low | 0 | 0 | 0 |  | ClassLibrary, Sdk Style = True |
| [core\Piranha.Local.FileStorage\Piranha.Local.FileStorage.csproj](#corepiranhalocalfilestoragepiranhalocalfilestoragecsproj) | net8.0;net9.0 | 🟢 Low | 0 | 0 | 0 |  | ClassLibrary, Sdk Style = True |
| [core\Piranha.Manager.LocalAuth\Piranha.Manager.LocalAuth.csproj](#corepiranhamanagerlocalauthpiranhamanagerlocalauthcsproj) | net8.0;net9.0 | 🟢 Low | 0 | 0 | 0 |  | ClassLibrary, Sdk Style = True |
| [core\Piranha.Manager.Localization\Piranha.Manager.Localization.csproj](#corepiranhamanagerlocalizationpiranhamanagerlocalizationcsproj) | net8.0;net9.0 | 🟢 Low | 0 | 0 | 0 |  | ClassLibrary, Sdk Style = True |
| [core\Piranha.Manager.TinyMCE\Piranha.Manager.TinyMCE.csproj](#corepiranhamanagertinymcepiranhamanagertinymcecsproj) | net8.0;net9.0 | 🟢 Low | 0 | 0 | 0 |  | ClassLibrary, Sdk Style = True |
| [core\Piranha.Manager\Piranha.Manager.csproj](#corepiranhamanagerpiranhamanagercsproj) | net8.0;net9.0 | 🟢 Low | 0 | 0 | 0 |  | ClassLibrary, Sdk Style = True |
| [core\Piranha.WebApi\Piranha.WebApi.csproj](#corepiranhawebapipiranhawebapicsproj) | net8.0;net9.0 | 🟢 Low | 0 | 0 | 0 |  | ClassLibrary, Sdk Style = True |
| [core\Piranha\Piranha.csproj](#corepiranhapiranhacsproj) | net8.0;net9.0 | 🟢 Low | 1 | 1 | 0 | 1+ | ClassLibrary, Sdk Style = True |
| [data\Piranha.Data.EF.MySql\Piranha.Data.EF.MySql.csproj](#datapiranhadataefmysqlpiranhadataefmysqlcsproj) | net8.0;net9.0 | 🟢 Low | 0 | 0 | 0 |  | ClassLibrary, Sdk Style = True |
| [data\Piranha.Data.EF.PostgreSql\Piranha.Data.EF.PostgreSql.csproj](#datapiranhadataefpostgresqlpiranhadataefpostgresqlcsproj) | net8.0;net9.0 | 🟢 Low | 0 | 0 | 0 |  | ClassLibrary, Sdk Style = True |
| [data\Piranha.Data.EF.SQLite\Piranha.Data.EF.SQLite.csproj](#datapiranhadataefsqlitepiranhadataefsqlitecsproj) | net8.0;net9.0 | 🟢 Low | 0 | 0 | 0 |  | ClassLibrary, Sdk Style = True |
| [data\Piranha.Data.EF.SQLServer\Piranha.Data.EF.SQLServer.csproj](#datapiranhadataefsqlserverpiranhadataefsqlservercsproj) | net8.0;net9.0 | 🟢 Low | 0 | 0 | 0 |  | ClassLibrary, Sdk Style = True |
| [data\Piranha.Data.EF\Piranha.Data.EF.csproj](#datapiranhadataefpiranhadataefcsproj) | net8.0;net9.0 | 🟢 Low | 1 | 0 | 0 |  | ClassLibrary, Sdk Style = True |
| [examples\MvcWeb\MvcWeb.csproj](#examplesmvcwebmvcwebcsproj) | net8.0;net9.0 | 🟢 Low | 0 | 0 | 0 |  | AspNetCore, Sdk Style = True |
| [examples\RazorWeb\RazorWeb.csproj](#examplesrazorwebrazorwebcsproj) | net8.0;net9.0 | 🟢 Low | 0 | 0 | 0 |  | AspNetCore, Sdk Style = True |
| [identity\Piranha.AspNetCore.Identity.MySQL\Piranha.AspNetCore.Identity.MySQL.csproj](#identitypiranhaaspnetcoreidentitymysqlpiranhaaspnetcoreidentitymysqlcsproj) | net8.0;net9.0 | 🟢 Low | 0 | 0 | 0 |  | ClassLibrary, Sdk Style = True |
| [identity\Piranha.AspNetCore.Identity.PostgreSQL\Piranha.AspNetCore.Identity.PostgreSQL.csproj](#identitypiranhaaspnetcoreidentitypostgresqlpiranhaaspnetcoreidentitypostgresqlcsproj) | net8.0;net9.0 | 🟢 Low | 0 | 0 | 0 |  | ClassLibrary, Sdk Style = True |
| [identity\Piranha.AspNetCore.Identity.SQLite\Piranha.AspNetCore.Identity.SQLite.csproj](#identitypiranhaaspnetcoreidentitysqlitepiranhaaspnetcoreidentitysqlitecsproj) | net8.0;net9.0 | 🟢 Low | 0 | 0 | 0 |  | ClassLibrary, Sdk Style = True |
| [identity\Piranha.AspNetCore.Identity.SQLServer\Piranha.AspNetCore.Identity.SQLServer.csproj](#identitypiranhaaspnetcoreidentitysqlserverpiranhaaspnetcoreidentitysqlservercsproj) | net8.0;net9.0 | 🟢 Low | 0 | 0 | 0 |  | ClassLibrary, Sdk Style = True |
| [identity\Piranha.AspNetCore.Identity\Piranha.AspNetCore.Identity.csproj](#identitypiranhaaspnetcoreidentitypiranhaaspnetcoreidentitycsproj) | net8.0;net9.0 | 🟢 Low | 0 | 4 | 0 | 4+ | ClassLibrary, Sdk Style = True |
| [test\Piranha.Manager.Tests\Piranha.Manager.Tests.csproj](#testpiranhamanagertestspiranhamanagertestscsproj) | net8.0;net9.0 | 🟢 Low | 1 | 0 | 0 |  | DotNetCoreApp, Sdk Style = True |
| [test\Piranha.Tests\Piranha.Tests.csproj](#testpiranhatestspiranhatestscsproj) | net8.0;net9.0 | 🟢 Low | 1 | 0 | 0 |  | DotNetCoreApp, Sdk Style = True |

### Package Compatibility

| Status | Count | Percentage |
| :--- | :---: | :---: |
| ✅ Compatible | 9 | 75.0% |
| ⚠️ Incompatible | 1 | 8.3% |
| 🔄 Upgrade Recommended | 2 | 16.7% |
| ***Total NuGet Packages*** | ***12*** | ***100%*** |

### API Compatibility

| Category | Count | Impact |
| :--- | :---: | :--- |
| 🔴 Binary Incompatible | 0 | High - Require code changes |
| 🟡 Source Incompatible | 6 | Medium - Needs re-compilation and potential conflicting API error fixing |
| 🔵 Behavioral change | 11 | Low - Behavioral changes that may require testing at runtime |
| ✅ Compatible | 188466 |  |
| ***Total APIs Analyzed*** | ***188483*** |  |

## Aggregate NuGet packages details

| Package | Current Version | Suggested Version | Projects | Description |
| :--- | :---: | :---: | :--- | :--- |
| AutoMapper | 12.0.1 | 16.1.1 | [Piranha.Data.EF.csproj](#datapiranhadataefpiranhadataefcsproj) | NuGet package contains security vulnerability |
| Azure.Storage.Blobs | 12.18.0 |  | [Piranha.Azure.BlobStorage.csproj](#corepiranhaazureblobstoragepiranhaazureblobstoragecsproj) | ✅Compatible |
| coverlet.collector | 6.0.2 |  | [Piranha.Manager.Tests.csproj](#testpiranhamanagertestspiranhamanagertestscsproj)<br/>[Piranha.Tests.csproj](#testpiranhatestspiranhatestscsproj) | ✅Compatible |
| coverlet.msbuild | 6.0.2 |  | [Piranha.Manager.Tests.csproj](#testpiranhamanagertestspiranhamanagertestscsproj)<br/>[Piranha.Tests.csproj](#testpiranhatestspiranhatestscsproj) | ✅Compatible |
| Markdig | 0.40.0 |  | [Piranha.csproj](#corepiranhapiranhacsproj) | ✅Compatible |
| Microsoft.NET.Test.Sdk | 17.9.0 |  | [Piranha.Manager.Tests.csproj](#testpiranhamanagertestspiranhamanagertestscsproj)<br/>[Piranha.Tests.csproj](#testpiranhatestspiranhatestscsproj) | ✅Compatible |
| Microsoft.SourceLink.GitHub | 1.1.1 |  | [MvcWeb.csproj](#examplesmvcwebmvcwebcsproj)<br/>[Piranha.AspNetCore.csproj](#corepiranhaaspnetcorepiranhaaspnetcorecsproj)<br/>[Piranha.AspNetCore.Hosting.csproj](#corepiranhaaspnetcorehostingpiranhaaspnetcorehostingcsproj)<br/>[Piranha.AspNetCore.Identity.csproj](#identitypiranhaaspnetcoreidentitypiranhaaspnetcoreidentitycsproj)<br/>[Piranha.AspNetCore.Identity.MySQL.csproj](#identitypiranhaaspnetcoreidentitymysqlpiranhaaspnetcoreidentitymysqlcsproj)<br/>[Piranha.AspNetCore.Identity.PostgreSQL.csproj](#identitypiranhaaspnetcoreidentitypostgresqlpiranhaaspnetcoreidentitypostgresqlcsproj)<br/>[Piranha.AspNetCore.Identity.SQLite.csproj](#identitypiranhaaspnetcoreidentitysqlitepiranhaaspnetcoreidentitysqlitecsproj)<br/>[Piranha.AspNetCore.Identity.SQLServer.csproj](#identitypiranhaaspnetcoreidentitysqlserverpiranhaaspnetcoreidentitysqlservercsproj)<br/>[Piranha.AttributeBuilder.csproj](#corepiranhaattributebuilderpiranhaattributebuildercsproj)<br/>[Piranha.Azure.BlobStorage.csproj](#corepiranhaazureblobstoragepiranhaazureblobstoragecsproj)<br/>[Piranha.csproj](#corepiranhapiranhacsproj)<br/>[Piranha.Data.EF.csproj](#datapiranhadataefpiranhadataefcsproj)<br/>[Piranha.Data.EF.MySql.csproj](#datapiranhadataefmysqlpiranhadataefmysqlcsproj)<br/>[Piranha.Data.EF.PostgreSql.csproj](#datapiranhadataefpostgresqlpiranhadataefpostgresqlcsproj)<br/>[Piranha.Data.EF.SQLite.csproj](#datapiranhadataefsqlitepiranhadataefsqlitecsproj)<br/>[Piranha.Data.EF.SQLServer.csproj](#datapiranhadataefsqlserverpiranhadataefsqlservercsproj)<br/>[Piranha.ImageSharp.csproj](#corepiranhaimagesharppiranhaimagesharpcsproj)<br/>[Piranha.Local.FileStorage.csproj](#corepiranhalocalfilestoragepiranhalocalfilestoragecsproj)<br/>[Piranha.Manager.csproj](#corepiranhamanagerpiranhamanagercsproj)<br/>[Piranha.Manager.LocalAuth.csproj](#corepiranhamanagerlocalauthpiranhamanagerlocalauthcsproj)<br/>[Piranha.Manager.Localization.csproj](#corepiranhamanagerlocalizationpiranhamanagerlocalizationcsproj)<br/>[Piranha.Manager.Tests.csproj](#testpiranhamanagertestspiranhamanagertestscsproj)<br/>[Piranha.Manager.TinyMCE.csproj](#corepiranhamanagertinymcepiranhamanagertinymcecsproj)<br/>[Piranha.Tests.csproj](#testpiranhatestspiranhatestscsproj)<br/>[Piranha.WebApi.csproj](#corepiranhawebapipiranhawebapicsproj)<br/>[RazorWeb.csproj](#examplesrazorwebrazorwebcsproj) | ✅Compatible |
| Newtonsoft.Json | 13.0.3 | 13.0.4 | [Piranha.csproj](#corepiranhapiranhacsproj) | NuGet package upgrade is recommended |
| SixLabors.ImageSharp | 2.1.13 |  | [Piranha.ImageSharp.csproj](#corepiranhaimagesharppiranhaimagesharpcsproj) | ✅Compatible |
| X.Web.Sitemap | 2.10.1 |  | [Piranha.AspNetCore.csproj](#corepiranhaaspnetcorepiranhaaspnetcorecsproj) | ✅Compatible |
| xunit | 2.7.0 |  | [Piranha.Manager.Tests.csproj](#testpiranhamanagertestspiranhamanagertestscsproj)<br/>[Piranha.Tests.csproj](#testpiranhatestspiranhatestscsproj) | ⚠️NuGet package is deprecated |
| xunit.runner.visualstudio | 2.5.7 |  | [Piranha.Manager.Tests.csproj](#testpiranhamanagertestspiranhamanagertestscsproj)<br/>[Piranha.Tests.csproj](#testpiranhatestspiranhatestscsproj) | ✅Compatible |

## Top API Migration Challenges

### Technologies and Features

| Technology | Issues | Percentage | Migration Path |
| :--- | :---: | :---: | :--- |

### Most Frequent API Issues

| API | Count | Percentage | Category |
| :--- | :---: | :---: | :--- |
| T:System.Uri | 8 | 47.1% | Behavioral Change |
| M:System.TimeSpan.FromMinutes(System.Double) | 3 | 17.6% | Source Incompatible |
| P:System.Uri.AbsoluteUri | 2 | 11.8% | Behavioral Change |
| M:Microsoft.Extensions.DependencyInjection.RazorRuntimeCompilationMvcBuilderExtensions.AddRazorRuntimeCompilation(Microsoft.Extensions.DependencyInjection.IMvcBuilder) | 1 | 5.9% | Source Incompatible |
| T:Microsoft.Extensions.DependencyInjection.IdentityEntityFrameworkBuilderExtensions | 1 | 5.9% | Source Incompatible |
| M:Microsoft.Extensions.DependencyInjection.IdentityEntityFrameworkBuilderExtensions.AddEntityFrameworkStores''1(Microsoft.AspNetCore.Identity.IdentityBuilder) | 1 | 5.9% | Source Incompatible |
| M:System.ValueType.GetHashCode | 1 | 5.9% | Behavioral Change |

## Projects Relationship Graph

Legend:
📦 SDK-style project
⚙️ Classic project

```mermaid
flowchart LR
    P1["<b>📦&nbsp;Piranha.csproj</b><br/><small>net8.0;net9.0</small>"]
    P2["<b>📦&nbsp;Piranha.AspNetCore.csproj</b><br/><small>net8.0;net9.0</small>"]
    P3["<b>📦&nbsp;Piranha.AttributeBuilder.csproj</b><br/><small>net8.0;net9.0</small>"]
    P4["<b>📦&nbsp;Piranha.Tests.csproj</b><br/><small>net8.0;net9.0</small>"]
    P5["<b>📦&nbsp;Piranha.Local.FileStorage.csproj</b><br/><small>net8.0;net9.0</small>"]
    P6["<b>📦&nbsp;Piranha.Azure.BlobStorage.csproj</b><br/><small>net8.0;net9.0</small>"]
    P7["<b>📦&nbsp;Piranha.ImageSharp.csproj</b><br/><small>net8.0;net9.0</small>"]
    P8["<b>📦&nbsp;Piranha.AspNetCore.Identity.csproj</b><br/><small>net8.0;net9.0</small>"]
    P9["<b>📦&nbsp;Piranha.AspNetCore.Identity.SQLite.csproj</b><br/><small>net8.0;net9.0</small>"]
    P10["<b>📦&nbsp;Piranha.AspNetCore.Identity.SQLServer.csproj</b><br/><small>net8.0;net9.0</small>"]
    P11["<b>📦&nbsp;MvcWeb.csproj</b><br/><small>net8.0;net9.0</small>"]
    P12["<b>📦&nbsp;Piranha.Data.EF.csproj</b><br/><small>net8.0;net9.0</small>"]
    P13["<b>📦&nbsp;Piranha.Manager.csproj</b><br/><small>net8.0;net9.0</small>"]
    P14["<b>📦&nbsp;Piranha.Manager.Localization.csproj</b><br/><small>net8.0;net9.0</small>"]
    P15["<b>📦&nbsp;Piranha.WebApi.csproj</b><br/><small>net8.0;net9.0</small>"]
    P16["<b>📦&nbsp;RazorWeb.csproj</b><br/><small>net8.0;net9.0</small>"]
    P17["<b>📦&nbsp;Piranha.Manager.TinyMCE.csproj</b><br/><small>net8.0;net9.0</small>"]
    P18["<b>📦&nbsp;Piranha.Manager.Tests.csproj</b><br/><small>net8.0;net9.0</small>"]
    P19["<b>📦&nbsp;Piranha.Data.EF.SQLite.csproj</b><br/><small>net8.0;net9.0</small>"]
    P20["<b>📦&nbsp;Piranha.Data.EF.SQLServer.csproj</b><br/><small>net8.0;net9.0</small>"]
    P21["<b>📦&nbsp;Piranha.Data.EF.MySql.csproj</b><br/><small>net8.0;net9.0</small>"]
    P22["<b>📦&nbsp;Piranha.Data.EF.PostgreSql.csproj</b><br/><small>net8.0;net9.0</small>"]
    P23["<b>📦&nbsp;Piranha.AspNetCore.Identity.MySQL.csproj</b><br/><small>net8.0;net9.0</small>"]
    P24["<b>📦&nbsp;Piranha.AspNetCore.Identity.PostgreSQL.csproj</b><br/><small>net8.0;net9.0</small>"]
    P25["<b>📦&nbsp;Piranha.Manager.LocalAuth.csproj</b><br/><small>net8.0;net9.0</small>"]
    P26["<b>📦&nbsp;Piranha.AspNetCore.Hosting.csproj</b><br/><small>net8.0;net9.0</small>"]
    P2 --> P1
    P2 --> P26
    P2 --> P1
    P2 --> P26
    P3 --> P1
    P3 --> P1
    P4 --> P1
    P4 --> P3
    P4 --> P7
    P4 --> P5
    P4 --> P12
    P4 --> P19
    P4 --> P1
    P4 --> P3
    P4 --> P7
    P4 --> P5
    P4 --> P12
    P4 --> P19
    P5 --> P1
    P5 --> P1
    P6 --> P1
    P6 --> P1
    P7 --> P1
    P7 --> P1
    P8 --> P1
    P8 --> P13
    P8 --> P25
    P8 --> P14
    P8 --> P26
    P8 --> P1
    P8 --> P13
    P8 --> P25
    P8 --> P14
    P8 --> P26
    P9 --> P8
    P9 --> P1
    P9 --> P26
    P9 --> P13
    P9 --> P25
    P9 --> P14
    P9 --> P8
    P9 --> P1
    P9 --> P26
    P9 --> P13
    P9 --> P25
    P9 --> P14
    P10 --> P8
    P10 --> P1
    P10 --> P26
    P10 --> P13
    P10 --> P25
    P10 --> P14
    P10 --> P8
    P10 --> P1
    P10 --> P26
    P10 --> P13
    P10 --> P25
    P10 --> P14
    P11 --> P1
    P11 --> P2
    P11 --> P3
    P11 --> P7
    P11 --> P5
    P11 --> P13
    P11 --> P25
    P11 --> P17
    P11 --> P19
    P11 --> P9
    P11 --> P26
    P11 --> P8
    P11 --> P12
    P11 --> P14
    P11 --> P1
    P11 --> P2
    P11 --> P3
    P11 --> P7
    P11 --> P5
    P11 --> P13
    P11 --> P25
    P11 --> P17
    P11 --> P19
    P11 --> P9
    P11 --> P26
    P11 --> P8
    P11 --> P12
    P11 --> P14
    P12 --> P1
    P12 --> P1
    P13 --> P1
    P13 --> P26
    P13 --> P14
    P13 --> P1
    P13 --> P26
    P13 --> P14
    P15 --> P1
    P15 --> P1
    P16 --> P1
    P16 --> P2
    P16 --> P3
    P16 --> P7
    P16 --> P5
    P16 --> P13
    P16 --> P25
    P16 --> P17
    P16 --> P19
    P16 --> P20
    P16 --> P21
    P16 --> P22
    P16 --> P9
    P16 --> P26
    P16 --> P8
    P16 --> P12
    P16 --> P14
    P16 --> P1
    P16 --> P2
    P16 --> P3
    P16 --> P7
    P16 --> P5
    P16 --> P13
    P16 --> P25
    P16 --> P17
    P16 --> P19
    P16 --> P20
    P16 --> P21
    P16 --> P22
    P16 --> P9
    P16 --> P26
    P16 --> P8
    P16 --> P12
    P16 --> P14
    P17 --> P13
    P17 --> P1
    P17 --> P26
    P17 --> P14
    P17 --> P13
    P17 --> P1
    P17 --> P26
    P17 --> P14
    P18 --> P13
    P18 --> P1
    P18 --> P26
    P18 --> P14
    P18 --> P13
    P18 --> P1
    P18 --> P26
    P18 --> P14
    P19 --> P12
    P19 --> P1
    P19 --> P12
    P19 --> P1
    P20 --> P12
    P20 --> P1
    P20 --> P12
    P20 --> P1
    P21 --> P12
    P21 --> P1
    P21 --> P12
    P21 --> P1
    P22 --> P12
    P22 --> P1
    P22 --> P12
    P22 --> P1
    P23 --> P8
    P23 --> P1
    P23 --> P26
    P23 --> P13
    P23 --> P25
    P23 --> P14
    P23 --> P8
    P23 --> P1
    P23 --> P26
    P23 --> P13
    P23 --> P25
    P23 --> P14
    P24 --> P8
    P24 --> P1
    P24 --> P26
    P24 --> P13
    P24 --> P25
    P24 --> P14
    P24 --> P8
    P24 --> P1
    P24 --> P26
    P24 --> P13
    P24 --> P25
    P24 --> P14
    P25 --> P1
    P25 --> P13
    P25 --> P26
    P25 --> P14
    P25 --> P1
    P25 --> P13
    P25 --> P26
    P25 --> P14
    P26 --> P1
    P26 --> P1
    click P1 "#corepiranhapiranhacsproj"
    click P2 "#corepiranhaaspnetcorepiranhaaspnetcorecsproj"
    click P3 "#corepiranhaattributebuilderpiranhaattributebuildercsproj"
    click P4 "#testpiranhatestspiranhatestscsproj"
    click P5 "#corepiranhalocalfilestoragepiranhalocalfilestoragecsproj"
    click P6 "#corepiranhaazureblobstoragepiranhaazureblobstoragecsproj"
    click P7 "#corepiranhaimagesharppiranhaimagesharpcsproj"
    click P8 "#identitypiranhaaspnetcoreidentitypiranhaaspnetcoreidentitycsproj"
    click P9 "#identitypiranhaaspnetcoreidentitysqlitepiranhaaspnetcoreidentitysqlitecsproj"
    click P10 "#identitypiranhaaspnetcoreidentitysqlserverpiranhaaspnetcoreidentitysqlservercsproj"
    click P11 "#examplesmvcwebmvcwebcsproj"
    click P12 "#datapiranhadataefpiranhadataefcsproj"
    click P13 "#corepiranhamanagerpiranhamanagercsproj"
    click P14 "#corepiranhamanagerlocalizationpiranhamanagerlocalizationcsproj"
    click P15 "#corepiranhawebapipiranhawebapicsproj"
    click P16 "#examplesrazorwebrazorwebcsproj"
    click P17 "#corepiranhamanagertinymcepiranhamanagertinymcecsproj"
    click P18 "#testpiranhamanagertestspiranhamanagertestscsproj"
    click P19 "#datapiranhadataefsqlitepiranhadataefsqlitecsproj"
    click P20 "#datapiranhadataefsqlserverpiranhadataefsqlservercsproj"
    click P21 "#datapiranhadataefmysqlpiranhadataefmysqlcsproj"
    click P22 "#datapiranhadataefpostgresqlpiranhadataefpostgresqlcsproj"
    click P23 "#identitypiranhaaspnetcoreidentitymysqlpiranhaaspnetcoreidentitymysqlcsproj"
    click P24 "#identitypiranhaaspnetcoreidentitypostgresqlpiranhaaspnetcoreidentitypostgresqlcsproj"
    click P25 "#corepiranhamanagerlocalauthpiranhamanagerlocalauthcsproj"
    click P26 "#corepiranhaaspnetcorehostingpiranhaaspnetcorehostingcsproj"

```

## Project Details

<a id="corepiranhaaspnetcorehostingpiranhaaspnetcorehostingcsproj"></a>
### core\Piranha.AspNetCore.Hosting\Piranha.AspNetCore.Hosting.csproj

#### Project Info

- **Current Target Framework:** net8.0;net9.0
- **Proposed Target Framework:** net8.0;net9.0;net10.0
- **SDK-style**: True
- **Project Kind:** ClassLibrary
- **Dependencies**: 2
- **Dependants**: 12
- **Number of Files**: 0
- **Number of Files with Incidents**: 1
- **Lines of Code**: 0
- **Estimated LOC to modify**: 0+ (at least 0.0% of the project)

#### Dependency Graph

Legend:
📦 SDK-style project
⚙️ Classic project

```mermaid
flowchart TB
    subgraph upstream["Dependants (12)"]
        P2["<b>📦&nbsp;Piranha.AspNetCore.csproj</b><br/><small>net8.0;net9.0</small>"]
        P8["<b>📦&nbsp;Piranha.AspNetCore.Identity.csproj</b><br/><small>net8.0;net9.0</small>"]
        P9["<b>📦&nbsp;Piranha.AspNetCore.Identity.SQLite.csproj</b><br/><small>net8.0;net9.0</small>"]
        P10["<b>📦&nbsp;Piranha.AspNetCore.Identity.SQLServer.csproj</b><br/><small>net8.0;net9.0</small>"]
        P11["<b>📦&nbsp;MvcWeb.csproj</b><br/><small>net8.0;net9.0</small>"]
        P13["<b>📦&nbsp;Piranha.Manager.csproj</b><br/><small>net8.0;net9.0</small>"]
        P16["<b>📦&nbsp;RazorWeb.csproj</b><br/><small>net8.0;net9.0</small>"]
        P17["<b>📦&nbsp;Piranha.Manager.TinyMCE.csproj</b><br/><small>net8.0;net9.0</small>"]
        P18["<b>📦&nbsp;Piranha.Manager.Tests.csproj</b><br/><small>net8.0;net9.0</small>"]
        P23["<b>📦&nbsp;Piranha.AspNetCore.Identity.MySQL.csproj</b><br/><small>net8.0;net9.0</small>"]
        P24["<b>📦&nbsp;Piranha.AspNetCore.Identity.PostgreSQL.csproj</b><br/><small>net8.0;net9.0</small>"]
        P25["<b>📦&nbsp;Piranha.Manager.LocalAuth.csproj</b><br/><small>net8.0;net9.0</small>"]
        click P2 "#corepiranhaaspnetcorepiranhaaspnetcorecsproj"
        click P8 "#identitypiranhaaspnetcoreidentitypiranhaaspnetcoreidentitycsproj"
        click P9 "#identitypiranhaaspnetcoreidentitysqlitepiranhaaspnetcoreidentitysqlitecsproj"
        click P10 "#identitypiranhaaspnetcoreidentitysqlserverpiranhaaspnetcoreidentitysqlservercsproj"
        click P11 "#examplesmvcwebmvcwebcsproj"
        click P13 "#corepiranhamanagerpiranhamanagercsproj"
        click P16 "#examplesrazorwebrazorwebcsproj"
        click P17 "#corepiranhamanagertinymcepiranhamanagertinymcecsproj"
        click P18 "#testpiranhamanagertestspiranhamanagertestscsproj"
        click P23 "#identitypiranhaaspnetcoreidentitymysqlpiranhaaspnetcoreidentitymysqlcsproj"
        click P24 "#identitypiranhaaspnetcoreidentitypostgresqlpiranhaaspnetcoreidentitypostgresqlcsproj"
        click P25 "#corepiranhamanagerlocalauthpiranhamanagerlocalauthcsproj"
    end
    subgraph current["Piranha.AspNetCore.Hosting.csproj"]
        MAIN["<b>📦&nbsp;Piranha.AspNetCore.Hosting.csproj</b><br/><small>net8.0;net9.0</small>"]
        click MAIN "#corepiranhaaspnetcorehostingpiranhaaspnetcorehostingcsproj"
    end
    subgraph downstream["Dependencies (2"]
        P1["<b>📦&nbsp;Piranha.csproj</b><br/><small>net8.0;net9.0</small>"]
        P1["<b>📦&nbsp;Piranha.csproj</b><br/><small>net8.0;net9.0</small>"]
        click P1 "#corepiranhapiranhacsproj"
        click P1 "#corepiranhapiranhacsproj"
    end
    P2 --> MAIN
    P8 --> MAIN
    P9 --> MAIN
    P10 --> MAIN
    P11 --> MAIN
    P13 --> MAIN
    P16 --> MAIN
    P17 --> MAIN
    P18 --> MAIN
    P23 --> MAIN
    P24 --> MAIN
    P25 --> MAIN
    MAIN --> P1
    MAIN --> P1

```

### API Compatibility

| Category | Count | Impact |
| :--- | :---: | :--- |
| 🔴 Binary Incompatible | 0 | High - Require code changes |
| 🟡 Source Incompatible | 0 | Medium - Needs re-compilation and potential conflicting API error fixing |
| 🔵 Behavioral change | 0 | Low - Behavioral changes that may require testing at runtime |
| ✅ Compatible | 125 |  |
| ***Total APIs Analyzed*** | ***125*** |  |

<a id="corepiranhaaspnetcorepiranhaaspnetcorecsproj"></a>
### core\Piranha.AspNetCore\Piranha.AspNetCore.csproj

#### Project Info

- **Current Target Framework:** net8.0;net9.0
- **Proposed Target Framework:** net8.0;net9.0;net10.0
- **SDK-style**: True
- **Project Kind:** ClassLibrary
- **Dependencies**: 4
- **Dependants**: 2
- **Number of Files**: 0
- **Number of Files with Incidents**: 4
- **Lines of Code**: 0
- **Estimated LOC to modify**: 4+ (at least 0.0% of the project)

#### Dependency Graph

Legend:
📦 SDK-style project
⚙️ Classic project

```mermaid
flowchart TB
    subgraph upstream["Dependants (2)"]
        P11["<b>📦&nbsp;MvcWeb.csproj</b><br/><small>net8.0;net9.0</small>"]
        P16["<b>📦&nbsp;RazorWeb.csproj</b><br/><small>net8.0;net9.0</small>"]
        click P11 "#examplesmvcwebmvcwebcsproj"
        click P16 "#examplesrazorwebrazorwebcsproj"
    end
    subgraph current["Piranha.AspNetCore.csproj"]
        MAIN["<b>📦&nbsp;Piranha.AspNetCore.csproj</b><br/><small>net8.0;net9.0</small>"]
        click MAIN "#corepiranhaaspnetcorepiranhaaspnetcorecsproj"
    end
    subgraph downstream["Dependencies (4"]
        P1["<b>📦&nbsp;Piranha.csproj</b><br/><small>net8.0;net9.0</small>"]
        P26["<b>📦&nbsp;Piranha.AspNetCore.Hosting.csproj</b><br/><small>net8.0;net9.0</small>"]
        P1["<b>📦&nbsp;Piranha.csproj</b><br/><small>net8.0;net9.0</small>"]
        P26["<b>📦&nbsp;Piranha.AspNetCore.Hosting.csproj</b><br/><small>net8.0;net9.0</small>"]
        click P1 "#corepiranhapiranhacsproj"
        click P26 "#corepiranhaaspnetcorehostingpiranhaaspnetcorehostingcsproj"
        click P1 "#corepiranhapiranhacsproj"
        click P26 "#corepiranhaaspnetcorehostingpiranhaaspnetcorehostingcsproj"
    end
    P11 --> MAIN
    P16 --> MAIN
    MAIN --> P1
    MAIN --> P26
    MAIN --> P1
    MAIN --> P26

```

### API Compatibility

| Category | Count | Impact |
| :--- | :---: | :--- |
| 🔴 Binary Incompatible | 0 | High - Require code changes |
| 🟡 Source Incompatible | 2 | Medium - Needs re-compilation and potential conflicting API error fixing |
| 🔵 Behavioral change | 2 | Low - Behavioral changes that may require testing at runtime |
| ✅ Compatible | 1824 |  |
| ***Total APIs Analyzed*** | ***1828*** |  |

<a id="corepiranhaattributebuilderpiranhaattributebuildercsproj"></a>
### core\Piranha.AttributeBuilder\Piranha.AttributeBuilder.csproj

#### Project Info

- **Current Target Framework:** net8.0;net9.0
- **Proposed Target Framework:** net8.0;net9.0;net10.0
- **SDK-style**: True
- **Project Kind:** ClassLibrary
- **Dependencies**: 2
- **Dependants**: 3
- **Number of Files**: 0
- **Number of Files with Incidents**: 1
- **Lines of Code**: 0
- **Estimated LOC to modify**: 0+ (at least 0.0% of the project)

#### Dependency Graph

Legend:
📦 SDK-style project
⚙️ Classic project

```mermaid
flowchart TB
    subgraph upstream["Dependants (3)"]
        P4["<b>📦&nbsp;Piranha.Tests.csproj</b><br/><small>net8.0;net9.0</small>"]
        P11["<b>📦&nbsp;MvcWeb.csproj</b><br/><small>net8.0;net9.0</small>"]
        P16["<b>📦&nbsp;RazorWeb.csproj</b><br/><small>net8.0;net9.0</small>"]
        click P4 "#testpiranhatestspiranhatestscsproj"
        click P11 "#examplesmvcwebmvcwebcsproj"
        click P16 "#examplesrazorwebrazorwebcsproj"
    end
    subgraph current["Piranha.AttributeBuilder.csproj"]
        MAIN["<b>📦&nbsp;Piranha.AttributeBuilder.csproj</b><br/><small>net8.0;net9.0</small>"]
        click MAIN "#corepiranhaattributebuilderpiranhaattributebuildercsproj"
    end
    subgraph downstream["Dependencies (2"]
        P1["<b>📦&nbsp;Piranha.csproj</b><br/><small>net8.0;net9.0</small>"]
        P1["<b>📦&nbsp;Piranha.csproj</b><br/><small>net8.0;net9.0</small>"]
        click P1 "#corepiranhapiranhacsproj"
        click P1 "#corepiranhapiranhacsproj"
    end
    P4 --> MAIN
    P11 --> MAIN
    P16 --> MAIN
    MAIN --> P1
    MAIN --> P1

```

### API Compatibility

| Category | Count | Impact |
| :--- | :---: | :--- |
| 🔴 Binary Incompatible | 0 | High - Require code changes |
| 🟡 Source Incompatible | 0 | Medium - Needs re-compilation and potential conflicting API error fixing |
| 🔵 Behavioral change | 0 | Low - Behavioral changes that may require testing at runtime |
| ✅ Compatible | 758 |  |
| ***Total APIs Analyzed*** | ***758*** |  |

<a id="corepiranhaazureblobstoragepiranhaazureblobstoragecsproj"></a>
### core\Piranha.Azure.BlobStorage\Piranha.Azure.BlobStorage.csproj

#### Project Info

- **Current Target Framework:** net8.0;net9.0
- **Proposed Target Framework:** net8.0;net9.0;net10.0
- **SDK-style**: True
- **Project Kind:** ClassLibrary
- **Dependencies**: 2
- **Dependants**: 0
- **Number of Files**: 0
- **Number of Files with Incidents**: 3
- **Lines of Code**: 0
- **Estimated LOC to modify**: 8+ (at least 0.0% of the project)

#### Dependency Graph

Legend:
📦 SDK-style project
⚙️ Classic project

```mermaid
flowchart TB
    subgraph current["Piranha.Azure.BlobStorage.csproj"]
        MAIN["<b>📦&nbsp;Piranha.Azure.BlobStorage.csproj</b><br/><small>net8.0;net9.0</small>"]
        click MAIN "#corepiranhaazureblobstoragepiranhaazureblobstoragecsproj"
    end
    subgraph downstream["Dependencies (2"]
        P1["<b>📦&nbsp;Piranha.csproj</b><br/><small>net8.0;net9.0</small>"]
        P1["<b>📦&nbsp;Piranha.csproj</b><br/><small>net8.0;net9.0</small>"]
        click P1 "#corepiranhapiranhacsproj"
        click P1 "#corepiranhapiranhacsproj"
    end
    MAIN --> P1
    MAIN --> P1

```

### API Compatibility

| Category | Count | Impact |
| :--- | :---: | :--- |
| 🔴 Binary Incompatible | 0 | High - Require code changes |
| 🟡 Source Incompatible | 0 | Medium - Needs re-compilation and potential conflicting API error fixing |
| 🔵 Behavioral change | 8 | Low - Behavioral changes that may require testing at runtime |
| ✅ Compatible | 166 |  |
| ***Total APIs Analyzed*** | ***174*** |  |

<a id="corepiranhaimagesharppiranhaimagesharpcsproj"></a>
### core\Piranha.ImageSharp\Piranha.ImageSharp.csproj

#### Project Info

- **Current Target Framework:** net8.0;net9.0
- **Proposed Target Framework:** net8.0;net9.0;net10.0
- **SDK-style**: True
- **Project Kind:** ClassLibrary
- **Dependencies**: 2
- **Dependants**: 3
- **Number of Files**: 0
- **Number of Files with Incidents**: 1
- **Lines of Code**: 0
- **Estimated LOC to modify**: 0+ (at least 0.0% of the project)

#### Dependency Graph

Legend:
📦 SDK-style project
⚙️ Classic project

```mermaid
flowchart TB
    subgraph upstream["Dependants (3)"]
        P4["<b>📦&nbsp;Piranha.Tests.csproj</b><br/><small>net8.0;net9.0</small>"]
        P11["<b>📦&nbsp;MvcWeb.csproj</b><br/><small>net8.0;net9.0</small>"]
        P16["<b>📦&nbsp;RazorWeb.csproj</b><br/><small>net8.0;net9.0</small>"]
        click P4 "#testpiranhatestspiranhatestscsproj"
        click P11 "#examplesmvcwebmvcwebcsproj"
        click P16 "#examplesrazorwebrazorwebcsproj"
    end
    subgraph current["Piranha.ImageSharp.csproj"]
        MAIN["<b>📦&nbsp;Piranha.ImageSharp.csproj</b><br/><small>net8.0;net9.0</small>"]
        click MAIN "#corepiranhaimagesharppiranhaimagesharpcsproj"
    end
    subgraph downstream["Dependencies (2"]
        P1["<b>📦&nbsp;Piranha.csproj</b><br/><small>net8.0;net9.0</small>"]
        P1["<b>📦&nbsp;Piranha.csproj</b><br/><small>net8.0;net9.0</small>"]
        click P1 "#corepiranhapiranhacsproj"
        click P1 "#corepiranhapiranhacsproj"
    end
    P4 --> MAIN
    P11 --> MAIN
    P16 --> MAIN
    MAIN --> P1
    MAIN --> P1

```

### API Compatibility

| Category | Count | Impact |
| :--- | :---: | :--- |
| 🔴 Binary Incompatible | 0 | High - Require code changes |
| 🟡 Source Incompatible | 0 | Medium - Needs re-compilation and potential conflicting API error fixing |
| 🔵 Behavioral change | 0 | Low - Behavioral changes that may require testing at runtime |
| ✅ Compatible | 189 |  |
| ***Total APIs Analyzed*** | ***189*** |  |

<a id="corepiranhalocalfilestoragepiranhalocalfilestoragecsproj"></a>
### core\Piranha.Local.FileStorage\Piranha.Local.FileStorage.csproj

#### Project Info

- **Current Target Framework:** net8.0;net9.0
- **Proposed Target Framework:** net8.0;net9.0;net10.0
- **SDK-style**: True
- **Project Kind:** ClassLibrary
- **Dependencies**: 2
- **Dependants**: 3
- **Number of Files**: 0
- **Number of Files with Incidents**: 1
- **Lines of Code**: 0
- **Estimated LOC to modify**: 0+ (at least 0.0% of the project)

#### Dependency Graph

Legend:
📦 SDK-style project
⚙️ Classic project

```mermaid
flowchart TB
    subgraph upstream["Dependants (3)"]
        P4["<b>📦&nbsp;Piranha.Tests.csproj</b><br/><small>net8.0;net9.0</small>"]
        P11["<b>📦&nbsp;MvcWeb.csproj</b><br/><small>net8.0;net9.0</small>"]
        P16["<b>📦&nbsp;RazorWeb.csproj</b><br/><small>net8.0;net9.0</small>"]
        click P4 "#testpiranhatestspiranhatestscsproj"
        click P11 "#examplesmvcwebmvcwebcsproj"
        click P16 "#examplesrazorwebrazorwebcsproj"
    end
    subgraph current["Piranha.Local.FileStorage.csproj"]
        MAIN["<b>📦&nbsp;Piranha.Local.FileStorage.csproj</b><br/><small>net8.0;net9.0</small>"]
        click MAIN "#corepiranhalocalfilestoragepiranhalocalfilestoragecsproj"
    end
    subgraph downstream["Dependencies (2"]
        P1["<b>📦&nbsp;Piranha.csproj</b><br/><small>net8.0;net9.0</small>"]
        P1["<b>📦&nbsp;Piranha.csproj</b><br/><small>net8.0;net9.0</small>"]
        click P1 "#corepiranhapiranhacsproj"
        click P1 "#corepiranhapiranhacsproj"
    end
    P4 --> MAIN
    P11 --> MAIN
    P16 --> MAIN
    MAIN --> P1
    MAIN --> P1

```

### API Compatibility

| Category | Count | Impact |
| :--- | :---: | :--- |
| 🔴 Binary Incompatible | 0 | High - Require code changes |
| 🟡 Source Incompatible | 0 | Medium - Needs re-compilation and potential conflicting API error fixing |
| 🔵 Behavioral change | 0 | Low - Behavioral changes that may require testing at runtime |
| ✅ Compatible | 226 |  |
| ***Total APIs Analyzed*** | ***226*** |  |

<a id="corepiranhamanagerlocalauthpiranhamanagerlocalauthcsproj"></a>
### core\Piranha.Manager.LocalAuth\Piranha.Manager.LocalAuth.csproj

#### Project Info

- **Current Target Framework:** net8.0;net9.0
- **Proposed Target Framework:** net8.0;net9.0;net10.0
- **SDK-style**: True
- **Project Kind:** ClassLibrary
- **Dependencies**: 8
- **Dependants**: 7
- **Number of Files**: 0
- **Number of Files with Incidents**: 1
- **Lines of Code**: 0
- **Estimated LOC to modify**: 0+ (at least 0.0% of the project)

#### Dependency Graph

Legend:
📦 SDK-style project
⚙️ Classic project

```mermaid
flowchart TB
    subgraph upstream["Dependants (7)"]
        P8["<b>📦&nbsp;Piranha.AspNetCore.Identity.csproj</b><br/><small>net8.0;net9.0</small>"]
        P9["<b>📦&nbsp;Piranha.AspNetCore.Identity.SQLite.csproj</b><br/><small>net8.0;net9.0</small>"]
        P10["<b>📦&nbsp;Piranha.AspNetCore.Identity.SQLServer.csproj</b><br/><small>net8.0;net9.0</small>"]
        P11["<b>📦&nbsp;MvcWeb.csproj</b><br/><small>net8.0;net9.0</small>"]
        P16["<b>📦&nbsp;RazorWeb.csproj</b><br/><small>net8.0;net9.0</small>"]
        P23["<b>📦&nbsp;Piranha.AspNetCore.Identity.MySQL.csproj</b><br/><small>net8.0;net9.0</small>"]
        P24["<b>📦&nbsp;Piranha.AspNetCore.Identity.PostgreSQL.csproj</b><br/><small>net8.0;net9.0</small>"]
        click P8 "#identitypiranhaaspnetcoreidentitypiranhaaspnetcoreidentitycsproj"
        click P9 "#identitypiranhaaspnetcoreidentitysqlitepiranhaaspnetcoreidentitysqlitecsproj"
        click P10 "#identitypiranhaaspnetcoreidentitysqlserverpiranhaaspnetcoreidentitysqlservercsproj"
        click P11 "#examplesmvcwebmvcwebcsproj"
        click P16 "#examplesrazorwebrazorwebcsproj"
        click P23 "#identitypiranhaaspnetcoreidentitymysqlpiranhaaspnetcoreidentitymysqlcsproj"
        click P24 "#identitypiranhaaspnetcoreidentitypostgresqlpiranhaaspnetcoreidentitypostgresqlcsproj"
    end
    subgraph current["Piranha.Manager.LocalAuth.csproj"]
        MAIN["<b>📦&nbsp;Piranha.Manager.LocalAuth.csproj</b><br/><small>net8.0;net9.0</small>"]
        click MAIN "#corepiranhamanagerlocalauthpiranhamanagerlocalauthcsproj"
    end
    subgraph downstream["Dependencies (8"]
        P1["<b>📦&nbsp;Piranha.csproj</b><br/><small>net8.0;net9.0</small>"]
        P13["<b>📦&nbsp;Piranha.Manager.csproj</b><br/><small>net8.0;net9.0</small>"]
        P26["<b>📦&nbsp;Piranha.AspNetCore.Hosting.csproj</b><br/><small>net8.0;net9.0</small>"]
        P14["<b>📦&nbsp;Piranha.Manager.Localization.csproj</b><br/><small>net8.0;net9.0</small>"]
        P1["<b>📦&nbsp;Piranha.csproj</b><br/><small>net8.0;net9.0</small>"]
        P13["<b>📦&nbsp;Piranha.Manager.csproj</b><br/><small>net8.0;net9.0</small>"]
        P26["<b>📦&nbsp;Piranha.AspNetCore.Hosting.csproj</b><br/><small>net8.0;net9.0</small>"]
        P14["<b>📦&nbsp;Piranha.Manager.Localization.csproj</b><br/><small>net8.0;net9.0</small>"]
        click P1 "#corepiranhapiranhacsproj"
        click P13 "#corepiranhamanagerpiranhamanagercsproj"
        click P26 "#corepiranhaaspnetcorehostingpiranhaaspnetcorehostingcsproj"
        click P14 "#corepiranhamanagerlocalizationpiranhamanagerlocalizationcsproj"
        click P1 "#corepiranhapiranhacsproj"
        click P13 "#corepiranhamanagerpiranhamanagercsproj"
        click P26 "#corepiranhaaspnetcorehostingpiranhaaspnetcorehostingcsproj"
        click P14 "#corepiranhamanagerlocalizationpiranhamanagerlocalizationcsproj"
    end
    P8 --> MAIN
    P9 --> MAIN
    P10 --> MAIN
    P11 --> MAIN
    P16 --> MAIN
    P23 --> MAIN
    P24 --> MAIN
    MAIN --> P1
    MAIN --> P13
    MAIN --> P26
    MAIN --> P14
    MAIN --> P1
    MAIN --> P13
    MAIN --> P26
    MAIN --> P14

```

### API Compatibility

| Category | Count | Impact |
| :--- | :---: | :--- |
| 🔴 Binary Incompatible | 0 | High - Require code changes |
| 🟡 Source Incompatible | 0 | Medium - Needs re-compilation and potential conflicting API error fixing |
| 🔵 Behavioral change | 0 | Low - Behavioral changes that may require testing at runtime |
| ✅ Compatible | 100 |  |
| ***Total APIs Analyzed*** | ***100*** |  |

<a id="corepiranhamanagerlocalizationpiranhamanagerlocalizationcsproj"></a>
### core\Piranha.Manager.Localization\Piranha.Manager.Localization.csproj

#### Project Info

- **Current Target Framework:** net8.0;net9.0
- **Proposed Target Framework:** net8.0;net9.0;net10.0
- **SDK-style**: True
- **Project Kind:** ClassLibrary
- **Dependencies**: 0
- **Dependants**: 11
- **Number of Files**: 0
- **Number of Files with Incidents**: 1
- **Lines of Code**: 0
- **Estimated LOC to modify**: 0+ (at least 0.0% of the project)

#### Dependency Graph

Legend:
📦 SDK-style project
⚙️ Classic project

```mermaid
flowchart TB
    subgraph upstream["Dependants (11)"]
        P8["<b>📦&nbsp;Piranha.AspNetCore.Identity.csproj</b><br/><small>net8.0;net9.0</small>"]
        P9["<b>📦&nbsp;Piranha.AspNetCore.Identity.SQLite.csproj</b><br/><small>net8.0;net9.0</small>"]
        P10["<b>📦&nbsp;Piranha.AspNetCore.Identity.SQLServer.csproj</b><br/><small>net8.0;net9.0</small>"]
        P11["<b>📦&nbsp;MvcWeb.csproj</b><br/><small>net8.0;net9.0</small>"]
        P13["<b>📦&nbsp;Piranha.Manager.csproj</b><br/><small>net8.0;net9.0</small>"]
        P16["<b>📦&nbsp;RazorWeb.csproj</b><br/><small>net8.0;net9.0</small>"]
        P17["<b>📦&nbsp;Piranha.Manager.TinyMCE.csproj</b><br/><small>net8.0;net9.0</small>"]
        P18["<b>📦&nbsp;Piranha.Manager.Tests.csproj</b><br/><small>net8.0;net9.0</small>"]
        P23["<b>📦&nbsp;Piranha.AspNetCore.Identity.MySQL.csproj</b><br/><small>net8.0;net9.0</small>"]
        P24["<b>📦&nbsp;Piranha.AspNetCore.Identity.PostgreSQL.csproj</b><br/><small>net8.0;net9.0</small>"]
        P25["<b>📦&nbsp;Piranha.Manager.LocalAuth.csproj</b><br/><small>net8.0;net9.0</small>"]
        click P8 "#identitypiranhaaspnetcoreidentitypiranhaaspnetcoreidentitycsproj"
        click P9 "#identitypiranhaaspnetcoreidentitysqlitepiranhaaspnetcoreidentitysqlitecsproj"
        click P10 "#identitypiranhaaspnetcoreidentitysqlserverpiranhaaspnetcoreidentitysqlservercsproj"
        click P11 "#examplesmvcwebmvcwebcsproj"
        click P13 "#corepiranhamanagerpiranhamanagercsproj"
        click P16 "#examplesrazorwebrazorwebcsproj"
        click P17 "#corepiranhamanagertinymcepiranhamanagertinymcecsproj"
        click P18 "#testpiranhamanagertestspiranhamanagertestscsproj"
        click P23 "#identitypiranhaaspnetcoreidentitymysqlpiranhaaspnetcoreidentitymysqlcsproj"
        click P24 "#identitypiranhaaspnetcoreidentitypostgresqlpiranhaaspnetcoreidentitypostgresqlcsproj"
        click P25 "#corepiranhamanagerlocalauthpiranhamanagerlocalauthcsproj"
    end
    subgraph current["Piranha.Manager.Localization.csproj"]
        MAIN["<b>📦&nbsp;Piranha.Manager.Localization.csproj</b><br/><small>net8.0;net9.0</small>"]
        click MAIN "#corepiranhamanagerlocalizationpiranhamanagerlocalizationcsproj"
    end
    P8 --> MAIN
    P9 --> MAIN
    P10 --> MAIN
    P11 --> MAIN
    P13 --> MAIN
    P16 --> MAIN
    P17 --> MAIN
    P18 --> MAIN
    P23 --> MAIN
    P24 --> MAIN
    P25 --> MAIN

```

### API Compatibility

| Category | Count | Impact |
| :--- | :---: | :--- |
| 🔴 Binary Incompatible | 0 | High - Require code changes |
| 🟡 Source Incompatible | 0 | Medium - Needs re-compilation and potential conflicting API error fixing |
| 🔵 Behavioral change | 0 | Low - Behavioral changes that may require testing at runtime |
| ✅ Compatible | 110 |  |
| ***Total APIs Analyzed*** | ***110*** |  |

<a id="corepiranhamanagertinymcepiranhamanagertinymcecsproj"></a>
### core\Piranha.Manager.TinyMCE\Piranha.Manager.TinyMCE.csproj

#### Project Info

- **Current Target Framework:** net8.0;net9.0
- **Proposed Target Framework:** net8.0;net9.0;net10.0
- **SDK-style**: True
- **Project Kind:** ClassLibrary
- **Dependencies**: 8
- **Dependants**: 2
- **Number of Files**: 76
- **Number of Files with Incidents**: 1
- **Lines of Code**: 0
- **Estimated LOC to modify**: 0+ (at least 0.0% of the project)

#### Dependency Graph

Legend:
📦 SDK-style project
⚙️ Classic project

```mermaid
flowchart TB
    subgraph upstream["Dependants (2)"]
        P11["<b>📦&nbsp;MvcWeb.csproj</b><br/><small>net8.0;net9.0</small>"]
        P16["<b>📦&nbsp;RazorWeb.csproj</b><br/><small>net8.0;net9.0</small>"]
        click P11 "#examplesmvcwebmvcwebcsproj"
        click P16 "#examplesrazorwebrazorwebcsproj"
    end
    subgraph current["Piranha.Manager.TinyMCE.csproj"]
        MAIN["<b>📦&nbsp;Piranha.Manager.TinyMCE.csproj</b><br/><small>net8.0;net9.0</small>"]
        click MAIN "#corepiranhamanagertinymcepiranhamanagertinymcecsproj"
    end
    subgraph downstream["Dependencies (8"]
        P13["<b>📦&nbsp;Piranha.Manager.csproj</b><br/><small>net8.0;net9.0</small>"]
        P1["<b>📦&nbsp;Piranha.csproj</b><br/><small>net8.0;net9.0</small>"]
        P26["<b>📦&nbsp;Piranha.AspNetCore.Hosting.csproj</b><br/><small>net8.0;net9.0</small>"]
        P14["<b>📦&nbsp;Piranha.Manager.Localization.csproj</b><br/><small>net8.0;net9.0</small>"]
        P13["<b>📦&nbsp;Piranha.Manager.csproj</b><br/><small>net8.0;net9.0</small>"]
        P1["<b>📦&nbsp;Piranha.csproj</b><br/><small>net8.0;net9.0</small>"]
        P26["<b>📦&nbsp;Piranha.AspNetCore.Hosting.csproj</b><br/><small>net8.0;net9.0</small>"]
        P14["<b>📦&nbsp;Piranha.Manager.Localization.csproj</b><br/><small>net8.0;net9.0</small>"]
        click P13 "#corepiranhamanagerpiranhamanagercsproj"
        click P1 "#corepiranhapiranhacsproj"
        click P26 "#corepiranhaaspnetcorehostingpiranhaaspnetcorehostingcsproj"
        click P14 "#corepiranhamanagerlocalizationpiranhamanagerlocalizationcsproj"
        click P13 "#corepiranhamanagerpiranhamanagercsproj"
        click P1 "#corepiranhapiranhacsproj"
        click P26 "#corepiranhaaspnetcorehostingpiranhaaspnetcorehostingcsproj"
        click P14 "#corepiranhamanagerlocalizationpiranhamanagerlocalizationcsproj"
    end
    P11 --> MAIN
    P16 --> MAIN
    MAIN --> P13
    MAIN --> P1
    MAIN --> P26
    MAIN --> P14
    MAIN --> P13
    MAIN --> P1
    MAIN --> P26
    MAIN --> P14

```

### API Compatibility

| Category | Count | Impact |
| :--- | :---: | :--- |
| 🔴 Binary Incompatible | 0 | High - Require code changes |
| 🟡 Source Incompatible | 0 | Medium - Needs re-compilation and potential conflicting API error fixing |
| 🔵 Behavioral change | 0 | Low - Behavioral changes that may require testing at runtime |
| ✅ Compatible | 70 |  |
| ***Total APIs Analyzed*** | ***70*** |  |

<a id="corepiranhamanagerpiranhamanagercsproj"></a>
### core\Piranha.Manager\Piranha.Manager.csproj

#### Project Info

- **Current Target Framework:** net8.0;net9.0
- **Proposed Target Framework:** net8.0;net9.0;net10.0
- **SDK-style**: True
- **Project Kind:** ClassLibrary
- **Dependencies**: 6
- **Dependants**: 10
- **Number of Files**: 81
- **Number of Files with Incidents**: 1
- **Lines of Code**: 0
- **Estimated LOC to modify**: 0+ (at least 0.0% of the project)

#### Dependency Graph

Legend:
📦 SDK-style project
⚙️ Classic project

```mermaid
flowchart TB
    subgraph upstream["Dependants (10)"]
        P8["<b>📦&nbsp;Piranha.AspNetCore.Identity.csproj</b><br/><small>net8.0;net9.0</small>"]
        P9["<b>📦&nbsp;Piranha.AspNetCore.Identity.SQLite.csproj</b><br/><small>net8.0;net9.0</small>"]
        P10["<b>📦&nbsp;Piranha.AspNetCore.Identity.SQLServer.csproj</b><br/><small>net8.0;net9.0</small>"]
        P11["<b>📦&nbsp;MvcWeb.csproj</b><br/><small>net8.0;net9.0</small>"]
        P16["<b>📦&nbsp;RazorWeb.csproj</b><br/><small>net8.0;net9.0</small>"]
        P17["<b>📦&nbsp;Piranha.Manager.TinyMCE.csproj</b><br/><small>net8.0;net9.0</small>"]
        P18["<b>📦&nbsp;Piranha.Manager.Tests.csproj</b><br/><small>net8.0;net9.0</small>"]
        P23["<b>📦&nbsp;Piranha.AspNetCore.Identity.MySQL.csproj</b><br/><small>net8.0;net9.0</small>"]
        P24["<b>📦&nbsp;Piranha.AspNetCore.Identity.PostgreSQL.csproj</b><br/><small>net8.0;net9.0</small>"]
        P25["<b>📦&nbsp;Piranha.Manager.LocalAuth.csproj</b><br/><small>net8.0;net9.0</small>"]
        click P8 "#identitypiranhaaspnetcoreidentitypiranhaaspnetcoreidentitycsproj"
        click P9 "#identitypiranhaaspnetcoreidentitysqlitepiranhaaspnetcoreidentitysqlitecsproj"
        click P10 "#identitypiranhaaspnetcoreidentitysqlserverpiranhaaspnetcoreidentitysqlservercsproj"
        click P11 "#examplesmvcwebmvcwebcsproj"
        click P16 "#examplesrazorwebrazorwebcsproj"
        click P17 "#corepiranhamanagertinymcepiranhamanagertinymcecsproj"
        click P18 "#testpiranhamanagertestspiranhamanagertestscsproj"
        click P23 "#identitypiranhaaspnetcoreidentitymysqlpiranhaaspnetcoreidentitymysqlcsproj"
        click P24 "#identitypiranhaaspnetcoreidentitypostgresqlpiranhaaspnetcoreidentitypostgresqlcsproj"
        click P25 "#corepiranhamanagerlocalauthpiranhamanagerlocalauthcsproj"
    end
    subgraph current["Piranha.Manager.csproj"]
        MAIN["<b>📦&nbsp;Piranha.Manager.csproj</b><br/><small>net8.0;net9.0</small>"]
        click MAIN "#corepiranhamanagerpiranhamanagercsproj"
    end
    subgraph downstream["Dependencies (6"]
        P1["<b>📦&nbsp;Piranha.csproj</b><br/><small>net8.0;net9.0</small>"]
        P26["<b>📦&nbsp;Piranha.AspNetCore.Hosting.csproj</b><br/><small>net8.0;net9.0</small>"]
        P14["<b>📦&nbsp;Piranha.Manager.Localization.csproj</b><br/><small>net8.0;net9.0</small>"]
        P1["<b>📦&nbsp;Piranha.csproj</b><br/><small>net8.0;net9.0</small>"]
        P26["<b>📦&nbsp;Piranha.AspNetCore.Hosting.csproj</b><br/><small>net8.0;net9.0</small>"]
        P14["<b>📦&nbsp;Piranha.Manager.Localization.csproj</b><br/><small>net8.0;net9.0</small>"]
        click P1 "#corepiranhapiranhacsproj"
        click P26 "#corepiranhaaspnetcorehostingpiranhaaspnetcorehostingcsproj"
        click P14 "#corepiranhamanagerlocalizationpiranhamanagerlocalizationcsproj"
        click P1 "#corepiranhapiranhacsproj"
        click P26 "#corepiranhaaspnetcorehostingpiranhaaspnetcorehostingcsproj"
        click P14 "#corepiranhamanagerlocalizationpiranhamanagerlocalizationcsproj"
    end
    P8 --> MAIN
    P9 --> MAIN
    P10 --> MAIN
    P11 --> MAIN
    P16 --> MAIN
    P17 --> MAIN
    P18 --> MAIN
    P23 --> MAIN
    P24 --> MAIN
    P25 --> MAIN
    MAIN --> P1
    MAIN --> P26
    MAIN --> P14
    MAIN --> P1
    MAIN --> P26
    MAIN --> P14

```

### API Compatibility

| Category | Count | Impact |
| :--- | :---: | :--- |
| 🔴 Binary Incompatible | 0 | High - Require code changes |
| 🟡 Source Incompatible | 0 | Medium - Needs re-compilation and potential conflicting API error fixing |
| 🔵 Behavioral change | 0 | Low - Behavioral changes that may require testing at runtime |
| ✅ Compatible | 7096 |  |
| ***Total APIs Analyzed*** | ***7096*** |  |

<a id="corepiranhawebapipiranhawebapicsproj"></a>
### core\Piranha.WebApi\Piranha.WebApi.csproj

#### Project Info

- **Current Target Framework:** net8.0;net9.0
- **Proposed Target Framework:** net8.0;net9.0;net10.0
- **SDK-style**: True
- **Project Kind:** ClassLibrary
- **Dependencies**: 2
- **Dependants**: 0
- **Number of Files**: 0
- **Number of Files with Incidents**: 1
- **Lines of Code**: 0
- **Estimated LOC to modify**: 0+ (at least 0.0% of the project)

#### Dependency Graph

Legend:
📦 SDK-style project
⚙️ Classic project

```mermaid
flowchart TB
    subgraph current["Piranha.WebApi.csproj"]
        MAIN["<b>📦&nbsp;Piranha.WebApi.csproj</b><br/><small>net8.0;net9.0</small>"]
        click MAIN "#corepiranhawebapipiranhawebapicsproj"
    end
    subgraph downstream["Dependencies (2"]
        P1["<b>📦&nbsp;Piranha.csproj</b><br/><small>net8.0;net9.0</small>"]
        P1["<b>📦&nbsp;Piranha.csproj</b><br/><small>net8.0;net9.0</small>"]
        click P1 "#corepiranhapiranhacsproj"
        click P1 "#corepiranhapiranhacsproj"
    end
    MAIN --> P1
    MAIN --> P1

```

### API Compatibility

| Category | Count | Impact |
| :--- | :---: | :--- |
| 🔴 Binary Incompatible | 0 | High - Require code changes |
| 🟡 Source Incompatible | 0 | Medium - Needs re-compilation and potential conflicting API error fixing |
| 🔵 Behavioral change | 0 | Low - Behavioral changes that may require testing at runtime |
| ✅ Compatible | 470 |  |
| ***Total APIs Analyzed*** | ***470*** |  |

<a id="corepiranhapiranhacsproj"></a>
### core\Piranha\Piranha.csproj

#### Project Info

- **Current Target Framework:** net8.0;net9.0
- **Proposed Target Framework:** net8.0;net9.0;net10.0
- **SDK-style**: True
- **Project Kind:** ClassLibrary
- **Dependencies**: 0
- **Dependants**: 24
- **Number of Files**: 0
- **Number of Files with Incidents**: 2
- **Lines of Code**: 0
- **Estimated LOC to modify**: 1+ (at least 0.0% of the project)

#### Dependency Graph

Legend:
📦 SDK-style project
⚙️ Classic project

```mermaid
flowchart TB
    subgraph upstream["Dependants (24)"]
        P2["<b>📦&nbsp;Piranha.AspNetCore.csproj</b><br/><small>net8.0;net9.0</small>"]
        P3["<b>📦&nbsp;Piranha.AttributeBuilder.csproj</b><br/><small>net8.0;net9.0</small>"]
        P4["<b>📦&nbsp;Piranha.Tests.csproj</b><br/><small>net8.0;net9.0</small>"]
        P5["<b>📦&nbsp;Piranha.Local.FileStorage.csproj</b><br/><small>net8.0;net9.0</small>"]
        P6["<b>📦&nbsp;Piranha.Azure.BlobStorage.csproj</b><br/><small>net8.0;net9.0</small>"]
        P7["<b>📦&nbsp;Piranha.ImageSharp.csproj</b><br/><small>net8.0;net9.0</small>"]
        P8["<b>📦&nbsp;Piranha.AspNetCore.Identity.csproj</b><br/><small>net8.0;net9.0</small>"]
        P9["<b>📦&nbsp;Piranha.AspNetCore.Identity.SQLite.csproj</b><br/><small>net8.0;net9.0</small>"]
        P10["<b>📦&nbsp;Piranha.AspNetCore.Identity.SQLServer.csproj</b><br/><small>net8.0;net9.0</small>"]
        P11["<b>📦&nbsp;MvcWeb.csproj</b><br/><small>net8.0;net9.0</small>"]
        P12["<b>📦&nbsp;Piranha.Data.EF.csproj</b><br/><small>net8.0;net9.0</small>"]
        P13["<b>📦&nbsp;Piranha.Manager.csproj</b><br/><small>net8.0;net9.0</small>"]
        P15["<b>📦&nbsp;Piranha.WebApi.csproj</b><br/><small>net8.0;net9.0</small>"]
        P16["<b>📦&nbsp;RazorWeb.csproj</b><br/><small>net8.0;net9.0</small>"]
        P17["<b>📦&nbsp;Piranha.Manager.TinyMCE.csproj</b><br/><small>net8.0;net9.0</small>"]
        P18["<b>📦&nbsp;Piranha.Manager.Tests.csproj</b><br/><small>net8.0;net9.0</small>"]
        P19["<b>📦&nbsp;Piranha.Data.EF.SQLite.csproj</b><br/><small>net8.0;net9.0</small>"]
        P20["<b>📦&nbsp;Piranha.Data.EF.SQLServer.csproj</b><br/><small>net8.0;net9.0</small>"]
        P21["<b>📦&nbsp;Piranha.Data.EF.MySql.csproj</b><br/><small>net8.0;net9.0</small>"]
        P22["<b>📦&nbsp;Piranha.Data.EF.PostgreSql.csproj</b><br/><small>net8.0;net9.0</small>"]
        P23["<b>📦&nbsp;Piranha.AspNetCore.Identity.MySQL.csproj</b><br/><small>net8.0;net9.0</small>"]
        P24["<b>📦&nbsp;Piranha.AspNetCore.Identity.PostgreSQL.csproj</b><br/><small>net8.0;net9.0</small>"]
        P25["<b>📦&nbsp;Piranha.Manager.LocalAuth.csproj</b><br/><small>net8.0;net9.0</small>"]
        P26["<b>📦&nbsp;Piranha.AspNetCore.Hosting.csproj</b><br/><small>net8.0;net9.0</small>"]
        click P2 "#corepiranhaaspnetcorepiranhaaspnetcorecsproj"
        click P3 "#corepiranhaattributebuilderpiranhaattributebuildercsproj"
        click P4 "#testpiranhatestspiranhatestscsproj"
        click P5 "#corepiranhalocalfilestoragepiranhalocalfilestoragecsproj"
        click P6 "#corepiranhaazureblobstoragepiranhaazureblobstoragecsproj"
        click P7 "#corepiranhaimagesharppiranhaimagesharpcsproj"
        click P8 "#identitypiranhaaspnetcoreidentitypiranhaaspnetcoreidentitycsproj"
        click P9 "#identitypiranhaaspnetcoreidentitysqlitepiranhaaspnetcoreidentitysqlitecsproj"
        click P10 "#identitypiranhaaspnetcoreidentitysqlserverpiranhaaspnetcoreidentitysqlservercsproj"
        click P11 "#examplesmvcwebmvcwebcsproj"
        click P12 "#datapiranhadataefpiranhadataefcsproj"
        click P13 "#corepiranhamanagerpiranhamanagercsproj"
        click P15 "#corepiranhawebapipiranhawebapicsproj"
        click P16 "#examplesrazorwebrazorwebcsproj"
        click P17 "#corepiranhamanagertinymcepiranhamanagertinymcecsproj"
        click P18 "#testpiranhamanagertestspiranhamanagertestscsproj"
        click P19 "#datapiranhadataefsqlitepiranhadataefsqlitecsproj"
        click P20 "#datapiranhadataefsqlserverpiranhadataefsqlservercsproj"
        click P21 "#datapiranhadataefmysqlpiranhadataefmysqlcsproj"
        click P22 "#datapiranhadataefpostgresqlpiranhadataefpostgresqlcsproj"
        click P23 "#identitypiranhaaspnetcoreidentitymysqlpiranhaaspnetcoreidentitymysqlcsproj"
        click P24 "#identitypiranhaaspnetcoreidentitypostgresqlpiranhaaspnetcoreidentitypostgresqlcsproj"
        click P25 "#corepiranhamanagerlocalauthpiranhamanagerlocalauthcsproj"
        click P26 "#corepiranhaaspnetcorehostingpiranhaaspnetcorehostingcsproj"
    end
    subgraph current["Piranha.csproj"]
        MAIN["<b>📦&nbsp;Piranha.csproj</b><br/><small>net8.0;net9.0</small>"]
        click MAIN "#corepiranhapiranhacsproj"
    end
    P2 --> MAIN
    P3 --> MAIN
    P4 --> MAIN
    P5 --> MAIN
    P6 --> MAIN
    P7 --> MAIN
    P8 --> MAIN
    P9 --> MAIN
    P10 --> MAIN
    P11 --> MAIN
    P12 --> MAIN
    P13 --> MAIN
    P15 --> MAIN
    P16 --> MAIN
    P17 --> MAIN
    P18 --> MAIN
    P19 --> MAIN
    P20 --> MAIN
    P21 --> MAIN
    P22 --> MAIN
    P23 --> MAIN
    P24 --> MAIN
    P25 --> MAIN
    P26 --> MAIN

```

### API Compatibility

| Category | Count | Impact |
| :--- | :---: | :--- |
| 🔴 Binary Incompatible | 0 | High - Require code changes |
| 🟡 Source Incompatible | 0 | Medium - Needs re-compilation and potential conflicting API error fixing |
| 🔵 Behavioral change | 1 | Low - Behavioral changes that may require testing at runtime |
| ✅ Compatible | 9651 |  |
| ***Total APIs Analyzed*** | ***9652*** |  |

<a id="datapiranhadataefmysqlpiranhadataefmysqlcsproj"></a>
### data\Piranha.Data.EF.MySql\Piranha.Data.EF.MySql.csproj

#### Project Info

- **Current Target Framework:** net8.0;net9.0
- **Proposed Target Framework:** net8.0;net9.0;net10.0
- **SDK-style**: True
- **Project Kind:** ClassLibrary
- **Dependencies**: 4
- **Dependants**: 1
- **Number of Files**: 0
- **Number of Files with Incidents**: 1
- **Lines of Code**: 0
- **Estimated LOC to modify**: 0+ (at least 0.0% of the project)

#### Dependency Graph

Legend:
📦 SDK-style project
⚙️ Classic project

```mermaid
flowchart TB
    subgraph upstream["Dependants (1)"]
        P16["<b>📦&nbsp;RazorWeb.csproj</b><br/><small>net8.0;net9.0</small>"]
        click P16 "#examplesrazorwebrazorwebcsproj"
    end
    subgraph current["Piranha.Data.EF.MySql.csproj"]
        MAIN["<b>📦&nbsp;Piranha.Data.EF.MySql.csproj</b><br/><small>net8.0;net9.0</small>"]
        click MAIN "#datapiranhadataefmysqlpiranhadataefmysqlcsproj"
    end
    subgraph downstream["Dependencies (4"]
        P12["<b>📦&nbsp;Piranha.Data.EF.csproj</b><br/><small>net8.0;net9.0</small>"]
        P1["<b>📦&nbsp;Piranha.csproj</b><br/><small>net8.0;net9.0</small>"]
        P12["<b>📦&nbsp;Piranha.Data.EF.csproj</b><br/><small>net8.0;net9.0</small>"]
        P1["<b>📦&nbsp;Piranha.csproj</b><br/><small>net8.0;net9.0</small>"]
        click P12 "#datapiranhadataefpiranhadataefcsproj"
        click P1 "#corepiranhapiranhacsproj"
        click P12 "#datapiranhadataefpiranhadataefcsproj"
        click P1 "#corepiranhapiranhacsproj"
    end
    P16 --> MAIN
    MAIN --> P12
    MAIN --> P1
    MAIN --> P12
    MAIN --> P1

```

### API Compatibility

| Category | Count | Impact |
| :--- | :---: | :--- |
| 🔴 Binary Incompatible | 0 | High - Require code changes |
| 🟡 Source Incompatible | 0 | Medium - Needs re-compilation and potential conflicting API error fixing |
| 🔵 Behavioral change | 0 | Low - Behavioral changes that may require testing at runtime |
| ✅ Compatible | 35744 |  |
| ***Total APIs Analyzed*** | ***35744*** |  |

<a id="datapiranhadataefpostgresqlpiranhadataefpostgresqlcsproj"></a>
### data\Piranha.Data.EF.PostgreSql\Piranha.Data.EF.PostgreSql.csproj

#### Project Info

- **Current Target Framework:** net8.0;net9.0
- **Proposed Target Framework:** net8.0;net9.0;net10.0
- **SDK-style**: True
- **Project Kind:** ClassLibrary
- **Dependencies**: 4
- **Dependants**: 1
- **Number of Files**: 0
- **Number of Files with Incidents**: 1
- **Lines of Code**: 0
- **Estimated LOC to modify**: 0+ (at least 0.0% of the project)

#### Dependency Graph

Legend:
📦 SDK-style project
⚙️ Classic project

```mermaid
flowchart TB
    subgraph upstream["Dependants (1)"]
        P16["<b>📦&nbsp;RazorWeb.csproj</b><br/><small>net8.0;net9.0</small>"]
        click P16 "#examplesrazorwebrazorwebcsproj"
    end
    subgraph current["Piranha.Data.EF.PostgreSql.csproj"]
        MAIN["<b>📦&nbsp;Piranha.Data.EF.PostgreSql.csproj</b><br/><small>net8.0;net9.0</small>"]
        click MAIN "#datapiranhadataefpostgresqlpiranhadataefpostgresqlcsproj"
    end
    subgraph downstream["Dependencies (4"]
        P12["<b>📦&nbsp;Piranha.Data.EF.csproj</b><br/><small>net8.0;net9.0</small>"]
        P1["<b>📦&nbsp;Piranha.csproj</b><br/><small>net8.0;net9.0</small>"]
        P12["<b>📦&nbsp;Piranha.Data.EF.csproj</b><br/><small>net8.0;net9.0</small>"]
        P1["<b>📦&nbsp;Piranha.csproj</b><br/><small>net8.0;net9.0</small>"]
        click P12 "#datapiranhadataefpiranhadataefcsproj"
        click P1 "#corepiranhapiranhacsproj"
        click P12 "#datapiranhadataefpiranhadataefcsproj"
        click P1 "#corepiranhapiranhacsproj"
    end
    P16 --> MAIN
    MAIN --> P12
    MAIN --> P1
    MAIN --> P12
    MAIN --> P1

```

### API Compatibility

| Category | Count | Impact |
| :--- | :---: | :--- |
| 🔴 Binary Incompatible | 0 | High - Require code changes |
| 🟡 Source Incompatible | 0 | Medium - Needs re-compilation and potential conflicting API error fixing |
| 🔵 Behavioral change | 0 | Low - Behavioral changes that may require testing at runtime |
| ✅ Compatible | 35784 |  |
| ***Total APIs Analyzed*** | ***35784*** |  |

<a id="datapiranhadataefsqlitepiranhadataefsqlitecsproj"></a>
### data\Piranha.Data.EF.SQLite\Piranha.Data.EF.SQLite.csproj

#### Project Info

- **Current Target Framework:** net8.0;net9.0
- **Proposed Target Framework:** net8.0;net9.0;net10.0
- **SDK-style**: True
- **Project Kind:** ClassLibrary
- **Dependencies**: 4
- **Dependants**: 3
- **Number of Files**: 0
- **Number of Files with Incidents**: 1
- **Lines of Code**: 0
- **Estimated LOC to modify**: 0+ (at least 0.0% of the project)

#### Dependency Graph

Legend:
📦 SDK-style project
⚙️ Classic project

```mermaid
flowchart TB
    subgraph upstream["Dependants (3)"]
        P4["<b>📦&nbsp;Piranha.Tests.csproj</b><br/><small>net8.0;net9.0</small>"]
        P11["<b>📦&nbsp;MvcWeb.csproj</b><br/><small>net8.0;net9.0</small>"]
        P16["<b>📦&nbsp;RazorWeb.csproj</b><br/><small>net8.0;net9.0</small>"]
        click P4 "#testpiranhatestspiranhatestscsproj"
        click P11 "#examplesmvcwebmvcwebcsproj"
        click P16 "#examplesrazorwebrazorwebcsproj"
    end
    subgraph current["Piranha.Data.EF.SQLite.csproj"]
        MAIN["<b>📦&nbsp;Piranha.Data.EF.SQLite.csproj</b><br/><small>net8.0;net9.0</small>"]
        click MAIN "#datapiranhadataefsqlitepiranhadataefsqlitecsproj"
    end
    subgraph downstream["Dependencies (4"]
        P12["<b>📦&nbsp;Piranha.Data.EF.csproj</b><br/><small>net8.0;net9.0</small>"]
        P1["<b>📦&nbsp;Piranha.csproj</b><br/><small>net8.0;net9.0</small>"]
        P12["<b>📦&nbsp;Piranha.Data.EF.csproj</b><br/><small>net8.0;net9.0</small>"]
        P1["<b>📦&nbsp;Piranha.csproj</b><br/><small>net8.0;net9.0</small>"]
        click P12 "#datapiranhadataefpiranhadataefcsproj"
        click P1 "#corepiranhapiranhacsproj"
        click P12 "#datapiranhadataefpiranhadataefcsproj"
        click P1 "#corepiranhapiranhacsproj"
    end
    P4 --> MAIN
    P11 --> MAIN
    P16 --> MAIN
    MAIN --> P12
    MAIN --> P1
    MAIN --> P12
    MAIN --> P1

```

### API Compatibility

| Category | Count | Impact |
| :--- | :---: | :--- |
| 🔴 Binary Incompatible | 0 | High - Require code changes |
| 🟡 Source Incompatible | 0 | Medium - Needs re-compilation and potential conflicting API error fixing |
| 🔵 Behavioral change | 0 | Low - Behavioral changes that may require testing at runtime |
| ✅ Compatible | 35719 |  |
| ***Total APIs Analyzed*** | ***35719*** |  |

<a id="datapiranhadataefsqlserverpiranhadataefsqlservercsproj"></a>
### data\Piranha.Data.EF.SQLServer\Piranha.Data.EF.SQLServer.csproj

#### Project Info

- **Current Target Framework:** net8.0;net9.0
- **Proposed Target Framework:** net8.0;net9.0;net10.0
- **SDK-style**: True
- **Project Kind:** ClassLibrary
- **Dependencies**: 4
- **Dependants**: 1
- **Number of Files**: 0
- **Number of Files with Incidents**: 1
- **Lines of Code**: 0
- **Estimated LOC to modify**: 0+ (at least 0.0% of the project)

#### Dependency Graph

Legend:
📦 SDK-style project
⚙️ Classic project

```mermaid
flowchart TB
    subgraph upstream["Dependants (1)"]
        P16["<b>📦&nbsp;RazorWeb.csproj</b><br/><small>net8.0;net9.0</small>"]
        click P16 "#examplesrazorwebrazorwebcsproj"
    end
    subgraph current["Piranha.Data.EF.SQLServer.csproj"]
        MAIN["<b>📦&nbsp;Piranha.Data.EF.SQLServer.csproj</b><br/><small>net8.0;net9.0</small>"]
        click MAIN "#datapiranhadataefsqlserverpiranhadataefsqlservercsproj"
    end
    subgraph downstream["Dependencies (4"]
        P12["<b>📦&nbsp;Piranha.Data.EF.csproj</b><br/><small>net8.0;net9.0</small>"]
        P1["<b>📦&nbsp;Piranha.csproj</b><br/><small>net8.0;net9.0</small>"]
        P12["<b>📦&nbsp;Piranha.Data.EF.csproj</b><br/><small>net8.0;net9.0</small>"]
        P1["<b>📦&nbsp;Piranha.csproj</b><br/><small>net8.0;net9.0</small>"]
        click P12 "#datapiranhadataefpiranhadataefcsproj"
        click P1 "#corepiranhapiranhacsproj"
        click P12 "#datapiranhadataefpiranhadataefcsproj"
        click P1 "#corepiranhapiranhacsproj"
    end
    P16 --> MAIN
    MAIN --> P12
    MAIN --> P1
    MAIN --> P12
    MAIN --> P1

```

### API Compatibility

| Category | Count | Impact |
| :--- | :---: | :--- |
| 🔴 Binary Incompatible | 0 | High - Require code changes |
| 🟡 Source Incompatible | 0 | Medium - Needs re-compilation and potential conflicting API error fixing |
| 🔵 Behavioral change | 0 | Low - Behavioral changes that may require testing at runtime |
| ✅ Compatible | 35799 |  |
| ***Total APIs Analyzed*** | ***35799*** |  |

<a id="datapiranhadataefpiranhadataefcsproj"></a>
### data\Piranha.Data.EF\Piranha.Data.EF.csproj

#### Project Info

- **Current Target Framework:** net8.0;net9.0
- **Proposed Target Framework:** net8.0;net9.0;net10.0
- **SDK-style**: True
- **Project Kind:** ClassLibrary
- **Dependencies**: 2
- **Dependants**: 7
- **Number of Files**: 0
- **Number of Files with Incidents**: 1
- **Lines of Code**: 0
- **Estimated LOC to modify**: 0+ (at least 0.0% of the project)

#### Dependency Graph

Legend:
📦 SDK-style project
⚙️ Classic project

```mermaid
flowchart TB
    subgraph upstream["Dependants (7)"]
        P4["<b>📦&nbsp;Piranha.Tests.csproj</b><br/><small>net8.0;net9.0</small>"]
        P11["<b>📦&nbsp;MvcWeb.csproj</b><br/><small>net8.0;net9.0</small>"]
        P16["<b>📦&nbsp;RazorWeb.csproj</b><br/><small>net8.0;net9.0</small>"]
        P19["<b>📦&nbsp;Piranha.Data.EF.SQLite.csproj</b><br/><small>net8.0;net9.0</small>"]
        P20["<b>📦&nbsp;Piranha.Data.EF.SQLServer.csproj</b><br/><small>net8.0;net9.0</small>"]
        P21["<b>📦&nbsp;Piranha.Data.EF.MySql.csproj</b><br/><small>net8.0;net9.0</small>"]
        P22["<b>📦&nbsp;Piranha.Data.EF.PostgreSql.csproj</b><br/><small>net8.0;net9.0</small>"]
        click P4 "#testpiranhatestspiranhatestscsproj"
        click P11 "#examplesmvcwebmvcwebcsproj"
        click P16 "#examplesrazorwebrazorwebcsproj"
        click P19 "#datapiranhadataefsqlitepiranhadataefsqlitecsproj"
        click P20 "#datapiranhadataefsqlserverpiranhadataefsqlservercsproj"
        click P21 "#datapiranhadataefmysqlpiranhadataefmysqlcsproj"
        click P22 "#datapiranhadataefpostgresqlpiranhadataefpostgresqlcsproj"
    end
    subgraph current["Piranha.Data.EF.csproj"]
        MAIN["<b>📦&nbsp;Piranha.Data.EF.csproj</b><br/><small>net8.0;net9.0</small>"]
        click MAIN "#datapiranhadataefpiranhadataefcsproj"
    end
    subgraph downstream["Dependencies (2"]
        P1["<b>📦&nbsp;Piranha.csproj</b><br/><small>net8.0;net9.0</small>"]
        P1["<b>📦&nbsp;Piranha.csproj</b><br/><small>net8.0;net9.0</small>"]
        click P1 "#corepiranhapiranhacsproj"
        click P1 "#corepiranhapiranhacsproj"
    end
    P4 --> MAIN
    P11 --> MAIN
    P16 --> MAIN
    P19 --> MAIN
    P20 --> MAIN
    P21 --> MAIN
    P22 --> MAIN
    MAIN --> P1
    MAIN --> P1

```

### API Compatibility

| Category | Count | Impact |
| :--- | :---: | :--- |
| 🔴 Binary Incompatible | 0 | High - Require code changes |
| 🟡 Source Incompatible | 0 | Medium - Needs re-compilation and potential conflicting API error fixing |
| 🔵 Behavioral change | 0 | Low - Behavioral changes that may require testing at runtime |
| ✅ Compatible | 10058 |  |
| ***Total APIs Analyzed*** | ***10058*** |  |

<a id="examplesmvcwebmvcwebcsproj"></a>
### examples\MvcWeb\MvcWeb.csproj

#### Project Info

- **Current Target Framework:** net8.0;net9.0
- **Proposed Target Framework:** net8.0;net9.0;net10.0
- **SDK-style**: True
- **Project Kind:** AspNetCore
- **Dependencies**: 28
- **Dependants**: 0
- **Number of Files**: 0
- **Number of Files with Incidents**: 1
- **Lines of Code**: 0
- **Estimated LOC to modify**: 0+ (at least 0.0% of the project)

#### Dependency Graph

Legend:
📦 SDK-style project
⚙️ Classic project

```mermaid
flowchart TB
    subgraph current["MvcWeb.csproj"]
        MAIN["<b>📦&nbsp;MvcWeb.csproj</b><br/><small>net8.0;net9.0</small>"]
        click MAIN "#examplesmvcwebmvcwebcsproj"
    end
    subgraph downstream["Dependencies (28"]
        P1["<b>📦&nbsp;Piranha.csproj</b><br/><small>net8.0;net9.0</small>"]
        P2["<b>📦&nbsp;Piranha.AspNetCore.csproj</b><br/><small>net8.0;net9.0</small>"]
        P3["<b>📦&nbsp;Piranha.AttributeBuilder.csproj</b><br/><small>net8.0;net9.0</small>"]
        P7["<b>📦&nbsp;Piranha.ImageSharp.csproj</b><br/><small>net8.0;net9.0</small>"]
        P5["<b>📦&nbsp;Piranha.Local.FileStorage.csproj</b><br/><small>net8.0;net9.0</small>"]
        P13["<b>📦&nbsp;Piranha.Manager.csproj</b><br/><small>net8.0;net9.0</small>"]
        P25["<b>📦&nbsp;Piranha.Manager.LocalAuth.csproj</b><br/><small>net8.0;net9.0</small>"]
        P17["<b>📦&nbsp;Piranha.Manager.TinyMCE.csproj</b><br/><small>net8.0;net9.0</small>"]
        P19["<b>📦&nbsp;Piranha.Data.EF.SQLite.csproj</b><br/><small>net8.0;net9.0</small>"]
        P9["<b>📦&nbsp;Piranha.AspNetCore.Identity.SQLite.csproj</b><br/><small>net8.0;net9.0</small>"]
        P26["<b>📦&nbsp;Piranha.AspNetCore.Hosting.csproj</b><br/><small>net8.0;net9.0</small>"]
        P8["<b>📦&nbsp;Piranha.AspNetCore.Identity.csproj</b><br/><small>net8.0;net9.0</small>"]
        P12["<b>📦&nbsp;Piranha.Data.EF.csproj</b><br/><small>net8.0;net9.0</small>"]
        P14["<b>📦&nbsp;Piranha.Manager.Localization.csproj</b><br/><small>net8.0;net9.0</small>"]
        P1["<b>📦&nbsp;Piranha.csproj</b><br/><small>net8.0;net9.0</small>"]
        P2["<b>📦&nbsp;Piranha.AspNetCore.csproj</b><br/><small>net8.0;net9.0</small>"]
        P3["<b>📦&nbsp;Piranha.AttributeBuilder.csproj</b><br/><small>net8.0;net9.0</small>"]
        P7["<b>📦&nbsp;Piranha.ImageSharp.csproj</b><br/><small>net8.0;net9.0</small>"]
        P5["<b>📦&nbsp;Piranha.Local.FileStorage.csproj</b><br/><small>net8.0;net9.0</small>"]
        P13["<b>📦&nbsp;Piranha.Manager.csproj</b><br/><small>net8.0;net9.0</small>"]
        P25["<b>📦&nbsp;Piranha.Manager.LocalAuth.csproj</b><br/><small>net8.0;net9.0</small>"]
        P17["<b>📦&nbsp;Piranha.Manager.TinyMCE.csproj</b><br/><small>net8.0;net9.0</small>"]
        P19["<b>📦&nbsp;Piranha.Data.EF.SQLite.csproj</b><br/><small>net8.0;net9.0</small>"]
        P9["<b>📦&nbsp;Piranha.AspNetCore.Identity.SQLite.csproj</b><br/><small>net8.0;net9.0</small>"]
        P26["<b>📦&nbsp;Piranha.AspNetCore.Hosting.csproj</b><br/><small>net8.0;net9.0</small>"]
        P8["<b>📦&nbsp;Piranha.AspNetCore.Identity.csproj</b><br/><small>net8.0;net9.0</small>"]
        P12["<b>📦&nbsp;Piranha.Data.EF.csproj</b><br/><small>net8.0;net9.0</small>"]
        P14["<b>📦&nbsp;Piranha.Manager.Localization.csproj</b><br/><small>net8.0;net9.0</small>"]
        click P1 "#corepiranhapiranhacsproj"
        click P2 "#corepiranhaaspnetcorepiranhaaspnetcorecsproj"
        click P3 "#corepiranhaattributebuilderpiranhaattributebuildercsproj"
        click P7 "#corepiranhaimagesharppiranhaimagesharpcsproj"
        click P5 "#corepiranhalocalfilestoragepiranhalocalfilestoragecsproj"
        click P13 "#corepiranhamanagerpiranhamanagercsproj"
        click P25 "#corepiranhamanagerlocalauthpiranhamanagerlocalauthcsproj"
        click P17 "#corepiranhamanagertinymcepiranhamanagertinymcecsproj"
        click P19 "#datapiranhadataefsqlitepiranhadataefsqlitecsproj"
        click P9 "#identitypiranhaaspnetcoreidentitysqlitepiranhaaspnetcoreidentitysqlitecsproj"
        click P26 "#corepiranhaaspnetcorehostingpiranhaaspnetcorehostingcsproj"
        click P8 "#identitypiranhaaspnetcoreidentitypiranhaaspnetcoreidentitycsproj"
        click P12 "#datapiranhadataefpiranhadataefcsproj"
        click P14 "#corepiranhamanagerlocalizationpiranhamanagerlocalizationcsproj"
        click P1 "#corepiranhapiranhacsproj"
        click P2 "#corepiranhaaspnetcorepiranhaaspnetcorecsproj"
        click P3 "#corepiranhaattributebuilderpiranhaattributebuildercsproj"
        click P7 "#corepiranhaimagesharppiranhaimagesharpcsproj"
        click P5 "#corepiranhalocalfilestoragepiranhalocalfilestoragecsproj"
        click P13 "#corepiranhamanagerpiranhamanagercsproj"
        click P25 "#corepiranhamanagerlocalauthpiranhamanagerlocalauthcsproj"
        click P17 "#corepiranhamanagertinymcepiranhamanagertinymcecsproj"
        click P19 "#datapiranhadataefsqlitepiranhadataefsqlitecsproj"
        click P9 "#identitypiranhaaspnetcoreidentitysqlitepiranhaaspnetcoreidentitysqlitecsproj"
        click P26 "#corepiranhaaspnetcorehostingpiranhaaspnetcorehostingcsproj"
        click P8 "#identitypiranhaaspnetcoreidentitypiranhaaspnetcoreidentitycsproj"
        click P12 "#datapiranhadataefpiranhadataefcsproj"
        click P14 "#corepiranhamanagerlocalizationpiranhamanagerlocalizationcsproj"
    end
    MAIN --> P1
    MAIN --> P2
    MAIN --> P3
    MAIN --> P7
    MAIN --> P5
    MAIN --> P13
    MAIN --> P25
    MAIN --> P17
    MAIN --> P19
    MAIN --> P9
    MAIN --> P26
    MAIN --> P8
    MAIN --> P12
    MAIN --> P14
    MAIN --> P1
    MAIN --> P2
    MAIN --> P3
    MAIN --> P7
    MAIN --> P5
    MAIN --> P13
    MAIN --> P25
    MAIN --> P17
    MAIN --> P19
    MAIN --> P9
    MAIN --> P26
    MAIN --> P8
    MAIN --> P12
    MAIN --> P14

```

### API Compatibility

| Category | Count | Impact |
| :--- | :---: | :--- |
| 🔴 Binary Incompatible | 0 | High - Require code changes |
| 🟡 Source Incompatible | 0 | Medium - Needs re-compilation and potential conflicting API error fixing |
| 🔵 Behavioral change | 0 | Low - Behavioral changes that may require testing at runtime |
| ✅ Compatible | 402 |  |
| ***Total APIs Analyzed*** | ***402*** |  |

<a id="examplesrazorwebrazorwebcsproj"></a>
### examples\RazorWeb\RazorWeb.csproj

#### Project Info

- **Current Target Framework:** net8.0;net9.0
- **Proposed Target Framework:** net8.0;net9.0;net10.0
- **SDK-style**: True
- **Project Kind:** AspNetCore
- **Dependencies**: 34
- **Dependants**: 0
- **Number of Files**: 0
- **Number of Files with Incidents**: 1
- **Lines of Code**: 0
- **Estimated LOC to modify**: 0+ (at least 0.0% of the project)

#### Dependency Graph

Legend:
📦 SDK-style project
⚙️ Classic project

```mermaid
flowchart TB
    subgraph current["RazorWeb.csproj"]
        MAIN["<b>📦&nbsp;RazorWeb.csproj</b><br/><small>net8.0;net9.0</small>"]
        click MAIN "#examplesrazorwebrazorwebcsproj"
    end
    subgraph downstream["Dependencies (34"]
        P1["<b>📦&nbsp;Piranha.csproj</b><br/><small>net8.0;net9.0</small>"]
        P2["<b>📦&nbsp;Piranha.AspNetCore.csproj</b><br/><small>net8.0;net9.0</small>"]
        P3["<b>📦&nbsp;Piranha.AttributeBuilder.csproj</b><br/><small>net8.0;net9.0</small>"]
        P7["<b>📦&nbsp;Piranha.ImageSharp.csproj</b><br/><small>net8.0;net9.0</small>"]
        P5["<b>📦&nbsp;Piranha.Local.FileStorage.csproj</b><br/><small>net8.0;net9.0</small>"]
        P13["<b>📦&nbsp;Piranha.Manager.csproj</b><br/><small>net8.0;net9.0</small>"]
        P25["<b>📦&nbsp;Piranha.Manager.LocalAuth.csproj</b><br/><small>net8.0;net9.0</small>"]
        P17["<b>📦&nbsp;Piranha.Manager.TinyMCE.csproj</b><br/><small>net8.0;net9.0</small>"]
        P19["<b>📦&nbsp;Piranha.Data.EF.SQLite.csproj</b><br/><small>net8.0;net9.0</small>"]
        P20["<b>📦&nbsp;Piranha.Data.EF.SQLServer.csproj</b><br/><small>net8.0;net9.0</small>"]
        P21["<b>📦&nbsp;Piranha.Data.EF.MySql.csproj</b><br/><small>net8.0;net9.0</small>"]
        P22["<b>📦&nbsp;Piranha.Data.EF.PostgreSql.csproj</b><br/><small>net8.0;net9.0</small>"]
        P9["<b>📦&nbsp;Piranha.AspNetCore.Identity.SQLite.csproj</b><br/><small>net8.0;net9.0</small>"]
        P26["<b>📦&nbsp;Piranha.AspNetCore.Hosting.csproj</b><br/><small>net8.0;net9.0</small>"]
        P8["<b>📦&nbsp;Piranha.AspNetCore.Identity.csproj</b><br/><small>net8.0;net9.0</small>"]
        P12["<b>📦&nbsp;Piranha.Data.EF.csproj</b><br/><small>net8.0;net9.0</small>"]
        P14["<b>📦&nbsp;Piranha.Manager.Localization.csproj</b><br/><small>net8.0;net9.0</small>"]
        P1["<b>📦&nbsp;Piranha.csproj</b><br/><small>net8.0;net9.0</small>"]
        P2["<b>📦&nbsp;Piranha.AspNetCore.csproj</b><br/><small>net8.0;net9.0</small>"]
        P3["<b>📦&nbsp;Piranha.AttributeBuilder.csproj</b><br/><small>net8.0;net9.0</small>"]
        P7["<b>📦&nbsp;Piranha.ImageSharp.csproj</b><br/><small>net8.0;net9.0</small>"]
        P5["<b>📦&nbsp;Piranha.Local.FileStorage.csproj</b><br/><small>net8.0;net9.0</small>"]
        P13["<b>📦&nbsp;Piranha.Manager.csproj</b><br/><small>net8.0;net9.0</small>"]
        P25["<b>📦&nbsp;Piranha.Manager.LocalAuth.csproj</b><br/><small>net8.0;net9.0</small>"]
        P17["<b>📦&nbsp;Piranha.Manager.TinyMCE.csproj</b><br/><small>net8.0;net9.0</small>"]
        P19["<b>📦&nbsp;Piranha.Data.EF.SQLite.csproj</b><br/><small>net8.0;net9.0</small>"]
        P20["<b>📦&nbsp;Piranha.Data.EF.SQLServer.csproj</b><br/><small>net8.0;net9.0</small>"]
        P21["<b>📦&nbsp;Piranha.Data.EF.MySql.csproj</b><br/><small>net8.0;net9.0</small>"]
        P22["<b>📦&nbsp;Piranha.Data.EF.PostgreSql.csproj</b><br/><small>net8.0;net9.0</small>"]
        P9["<b>📦&nbsp;Piranha.AspNetCore.Identity.SQLite.csproj</b><br/><small>net8.0;net9.0</small>"]
        P26["<b>📦&nbsp;Piranha.AspNetCore.Hosting.csproj</b><br/><small>net8.0;net9.0</small>"]
        P8["<b>📦&nbsp;Piranha.AspNetCore.Identity.csproj</b><br/><small>net8.0;net9.0</small>"]
        P12["<b>📦&nbsp;Piranha.Data.EF.csproj</b><br/><small>net8.0;net9.0</small>"]
        P14["<b>📦&nbsp;Piranha.Manager.Localization.csproj</b><br/><small>net8.0;net9.0</small>"]
        click P1 "#corepiranhapiranhacsproj"
        click P2 "#corepiranhaaspnetcorepiranhaaspnetcorecsproj"
        click P3 "#corepiranhaattributebuilderpiranhaattributebuildercsproj"
        click P7 "#corepiranhaimagesharppiranhaimagesharpcsproj"
        click P5 "#corepiranhalocalfilestoragepiranhalocalfilestoragecsproj"
        click P13 "#corepiranhamanagerpiranhamanagercsproj"
        click P25 "#corepiranhamanagerlocalauthpiranhamanagerlocalauthcsproj"
        click P17 "#corepiranhamanagertinymcepiranhamanagertinymcecsproj"
        click P19 "#datapiranhadataefsqlitepiranhadataefsqlitecsproj"
        click P20 "#datapiranhadataefsqlserverpiranhadataefsqlservercsproj"
        click P21 "#datapiranhadataefmysqlpiranhadataefmysqlcsproj"
        click P22 "#datapiranhadataefpostgresqlpiranhadataefpostgresqlcsproj"
        click P9 "#identitypiranhaaspnetcoreidentitysqlitepiranhaaspnetcoreidentitysqlitecsproj"
        click P26 "#corepiranhaaspnetcorehostingpiranhaaspnetcorehostingcsproj"
        click P8 "#identitypiranhaaspnetcoreidentitypiranhaaspnetcoreidentitycsproj"
        click P12 "#datapiranhadataefpiranhadataefcsproj"
        click P14 "#corepiranhamanagerlocalizationpiranhamanagerlocalizationcsproj"
        click P1 "#corepiranhapiranhacsproj"
        click P2 "#corepiranhaaspnetcorepiranhaaspnetcorecsproj"
        click P3 "#corepiranhaattributebuilderpiranhaattributebuildercsproj"
        click P7 "#corepiranhaimagesharppiranhaimagesharpcsproj"
        click P5 "#corepiranhalocalfilestoragepiranhalocalfilestoragecsproj"
        click P13 "#corepiranhamanagerpiranhamanagercsproj"
        click P25 "#corepiranhamanagerlocalauthpiranhamanagerlocalauthcsproj"
        click P17 "#corepiranhamanagertinymcepiranhamanagertinymcecsproj"
        click P19 "#datapiranhadataefsqlitepiranhadataefsqlitecsproj"
        click P20 "#datapiranhadataefsqlserverpiranhadataefsqlservercsproj"
        click P21 "#datapiranhadataefmysqlpiranhadataefmysqlcsproj"
        click P22 "#datapiranhadataefpostgresqlpiranhadataefpostgresqlcsproj"
        click P9 "#identitypiranhaaspnetcoreidentitysqlitepiranhaaspnetcoreidentitysqlitecsproj"
        click P26 "#corepiranhaaspnetcorehostingpiranhaaspnetcorehostingcsproj"
        click P8 "#identitypiranhaaspnetcoreidentitypiranhaaspnetcoreidentitycsproj"
        click P12 "#datapiranhadataefpiranhadataefcsproj"
        click P14 "#corepiranhamanagerlocalizationpiranhamanagerlocalizationcsproj"
    end
    MAIN --> P1
    MAIN --> P2
    MAIN --> P3
    MAIN --> P7
    MAIN --> P5
    MAIN --> P13
    MAIN --> P25
    MAIN --> P17
    MAIN --> P19
    MAIN --> P20
    MAIN --> P21
    MAIN --> P22
    MAIN --> P9
    MAIN --> P26
    MAIN --> P8
    MAIN --> P12
    MAIN --> P14
    MAIN --> P1
    MAIN --> P2
    MAIN --> P3
    MAIN --> P7
    MAIN --> P5
    MAIN --> P13
    MAIN --> P25
    MAIN --> P17
    MAIN --> P19
    MAIN --> P20
    MAIN --> P21
    MAIN --> P22
    MAIN --> P9
    MAIN --> P26
    MAIN --> P8
    MAIN --> P12
    MAIN --> P14

```

### API Compatibility

| Category | Count | Impact |
| :--- | :---: | :--- |
| 🔴 Binary Incompatible | 0 | High - Require code changes |
| 🟡 Source Incompatible | 0 | Medium - Needs re-compilation and potential conflicting API error fixing |
| 🔵 Behavioral change | 0 | Low - Behavioral changes that may require testing at runtime |
| ✅ Compatible | 496 |  |
| ***Total APIs Analyzed*** | ***496*** |  |

<a id="identitypiranhaaspnetcoreidentitymysqlpiranhaaspnetcoreidentitymysqlcsproj"></a>
### identity\Piranha.AspNetCore.Identity.MySQL\Piranha.AspNetCore.Identity.MySQL.csproj

#### Project Info

- **Current Target Framework:** net8.0;net9.0
- **Proposed Target Framework:** net8.0;net9.0;net10.0
- **SDK-style**: True
- **Project Kind:** ClassLibrary
- **Dependencies**: 12
- **Dependants**: 0
- **Number of Files**: 0
- **Number of Files with Incidents**: 1
- **Lines of Code**: 0
- **Estimated LOC to modify**: 0+ (at least 0.0% of the project)

#### Dependency Graph

Legend:
📦 SDK-style project
⚙️ Classic project

```mermaid
flowchart TB
    subgraph current["Piranha.AspNetCore.Identity.MySQL.csproj"]
        MAIN["<b>📦&nbsp;Piranha.AspNetCore.Identity.MySQL.csproj</b><br/><small>net8.0;net9.0</small>"]
        click MAIN "#identitypiranhaaspnetcoreidentitymysqlpiranhaaspnetcoreidentitymysqlcsproj"
    end
    subgraph downstream["Dependencies (12"]
        P8["<b>📦&nbsp;Piranha.AspNetCore.Identity.csproj</b><br/><small>net8.0;net9.0</small>"]
        P1["<b>📦&nbsp;Piranha.csproj</b><br/><small>net8.0;net9.0</small>"]
        P26["<b>📦&nbsp;Piranha.AspNetCore.Hosting.csproj</b><br/><small>net8.0;net9.0</small>"]
        P13["<b>📦&nbsp;Piranha.Manager.csproj</b><br/><small>net8.0;net9.0</small>"]
        P25["<b>📦&nbsp;Piranha.Manager.LocalAuth.csproj</b><br/><small>net8.0;net9.0</small>"]
        P14["<b>📦&nbsp;Piranha.Manager.Localization.csproj</b><br/><small>net8.0;net9.0</small>"]
        P8["<b>📦&nbsp;Piranha.AspNetCore.Identity.csproj</b><br/><small>net8.0;net9.0</small>"]
        P1["<b>📦&nbsp;Piranha.csproj</b><br/><small>net8.0;net9.0</small>"]
        P26["<b>📦&nbsp;Piranha.AspNetCore.Hosting.csproj</b><br/><small>net8.0;net9.0</small>"]
        P13["<b>📦&nbsp;Piranha.Manager.csproj</b><br/><small>net8.0;net9.0</small>"]
        P25["<b>📦&nbsp;Piranha.Manager.LocalAuth.csproj</b><br/><small>net8.0;net9.0</small>"]
        P14["<b>📦&nbsp;Piranha.Manager.Localization.csproj</b><br/><small>net8.0;net9.0</small>"]
        click P8 "#identitypiranhaaspnetcoreidentitypiranhaaspnetcoreidentitycsproj"
        click P1 "#corepiranhapiranhacsproj"
        click P26 "#corepiranhaaspnetcorehostingpiranhaaspnetcorehostingcsproj"
        click P13 "#corepiranhamanagerpiranhamanagercsproj"
        click P25 "#corepiranhamanagerlocalauthpiranhamanagerlocalauthcsproj"
        click P14 "#corepiranhamanagerlocalizationpiranhamanagerlocalizationcsproj"
        click P8 "#identitypiranhaaspnetcoreidentitypiranhaaspnetcoreidentitycsproj"
        click P1 "#corepiranhapiranhacsproj"
        click P26 "#corepiranhaaspnetcorehostingpiranhaaspnetcorehostingcsproj"
        click P13 "#corepiranhamanagerpiranhamanagercsproj"
        click P25 "#corepiranhamanagerlocalauthpiranhamanagerlocalauthcsproj"
        click P14 "#corepiranhamanagerlocalizationpiranhamanagerlocalizationcsproj"
    end
    MAIN --> P8
    MAIN --> P1
    MAIN --> P26
    MAIN --> P13
    MAIN --> P25
    MAIN --> P14
    MAIN --> P8
    MAIN --> P1
    MAIN --> P26
    MAIN --> P13
    MAIN --> P25
    MAIN --> P14

```

### API Compatibility

| Category | Count | Impact |
| :--- | :---: | :--- |
| 🔴 Binary Incompatible | 0 | High - Require code changes |
| 🟡 Source Incompatible | 0 | Medium - Needs re-compilation and potential conflicting API error fixing |
| 🔵 Behavioral change | 0 | Low - Behavioral changes that may require testing at runtime |
| ✅ Compatible | 785 |  |
| ***Total APIs Analyzed*** | ***785*** |  |

<a id="identitypiranhaaspnetcoreidentitypostgresqlpiranhaaspnetcoreidentitypostgresqlcsproj"></a>
### identity\Piranha.AspNetCore.Identity.PostgreSQL\Piranha.AspNetCore.Identity.PostgreSQL.csproj

#### Project Info

- **Current Target Framework:** net8.0;net9.0
- **Proposed Target Framework:** net8.0;net9.0;net10.0
- **SDK-style**: True
- **Project Kind:** ClassLibrary
- **Dependencies**: 12
- **Dependants**: 0
- **Number of Files**: 0
- **Number of Files with Incidents**: 1
- **Lines of Code**: 0
- **Estimated LOC to modify**: 0+ (at least 0.0% of the project)

#### Dependency Graph

Legend:
📦 SDK-style project
⚙️ Classic project

```mermaid
flowchart TB
    subgraph current["Piranha.AspNetCore.Identity.PostgreSQL.csproj"]
        MAIN["<b>📦&nbsp;Piranha.AspNetCore.Identity.PostgreSQL.csproj</b><br/><small>net8.0;net9.0</small>"]
        click MAIN "#identitypiranhaaspnetcoreidentitypostgresqlpiranhaaspnetcoreidentitypostgresqlcsproj"
    end
    subgraph downstream["Dependencies (12"]
        P8["<b>📦&nbsp;Piranha.AspNetCore.Identity.csproj</b><br/><small>net8.0;net9.0</small>"]
        P1["<b>📦&nbsp;Piranha.csproj</b><br/><small>net8.0;net9.0</small>"]
        P26["<b>📦&nbsp;Piranha.AspNetCore.Hosting.csproj</b><br/><small>net8.0;net9.0</small>"]
        P13["<b>📦&nbsp;Piranha.Manager.csproj</b><br/><small>net8.0;net9.0</small>"]
        P25["<b>📦&nbsp;Piranha.Manager.LocalAuth.csproj</b><br/><small>net8.0;net9.0</small>"]
        P14["<b>📦&nbsp;Piranha.Manager.Localization.csproj</b><br/><small>net8.0;net9.0</small>"]
        P8["<b>📦&nbsp;Piranha.AspNetCore.Identity.csproj</b><br/><small>net8.0;net9.0</small>"]
        P1["<b>📦&nbsp;Piranha.csproj</b><br/><small>net8.0;net9.0</small>"]
        P26["<b>📦&nbsp;Piranha.AspNetCore.Hosting.csproj</b><br/><small>net8.0;net9.0</small>"]
        P13["<b>📦&nbsp;Piranha.Manager.csproj</b><br/><small>net8.0;net9.0</small>"]
        P25["<b>📦&nbsp;Piranha.Manager.LocalAuth.csproj</b><br/><small>net8.0;net9.0</small>"]
        P14["<b>📦&nbsp;Piranha.Manager.Localization.csproj</b><br/><small>net8.0;net9.0</small>"]
        click P8 "#identitypiranhaaspnetcoreidentitypiranhaaspnetcoreidentitycsproj"
        click P1 "#corepiranhapiranhacsproj"
        click P26 "#corepiranhaaspnetcorehostingpiranhaaspnetcorehostingcsproj"
        click P13 "#corepiranhamanagerpiranhamanagercsproj"
        click P25 "#corepiranhamanagerlocalauthpiranhamanagerlocalauthcsproj"
        click P14 "#corepiranhamanagerlocalizationpiranhamanagerlocalizationcsproj"
        click P8 "#identitypiranhaaspnetcoreidentitypiranhaaspnetcoreidentitycsproj"
        click P1 "#corepiranhapiranhacsproj"
        click P26 "#corepiranhaaspnetcorehostingpiranhaaspnetcorehostingcsproj"
        click P13 "#corepiranhamanagerpiranhamanagercsproj"
        click P25 "#corepiranhamanagerlocalauthpiranhamanagerlocalauthcsproj"
        click P14 "#corepiranhamanagerlocalizationpiranhamanagerlocalizationcsproj"
    end
    MAIN --> P8
    MAIN --> P1
    MAIN --> P26
    MAIN --> P13
    MAIN --> P25
    MAIN --> P14
    MAIN --> P8
    MAIN --> P1
    MAIN --> P26
    MAIN --> P13
    MAIN --> P25
    MAIN --> P14

```

### API Compatibility

| Category | Count | Impact |
| :--- | :---: | :--- |
| 🔴 Binary Incompatible | 0 | High - Require code changes |
| 🟡 Source Incompatible | 0 | Medium - Needs re-compilation and potential conflicting API error fixing |
| 🔵 Behavioral change | 0 | Low - Behavioral changes that may require testing at runtime |
| ✅ Compatible | 804 |  |
| ***Total APIs Analyzed*** | ***804*** |  |

<a id="identitypiranhaaspnetcoreidentitysqlitepiranhaaspnetcoreidentitysqlitecsproj"></a>
### identity\Piranha.AspNetCore.Identity.SQLite\Piranha.AspNetCore.Identity.SQLite.csproj

#### Project Info

- **Current Target Framework:** net8.0;net9.0
- **Proposed Target Framework:** net8.0;net9.0;net10.0
- **SDK-style**: True
- **Project Kind:** ClassLibrary
- **Dependencies**: 12
- **Dependants**: 2
- **Number of Files**: 0
- **Number of Files with Incidents**: 1
- **Lines of Code**: 0
- **Estimated LOC to modify**: 0+ (at least 0.0% of the project)

#### Dependency Graph

Legend:
📦 SDK-style project
⚙️ Classic project

```mermaid
flowchart TB
    subgraph upstream["Dependants (2)"]
        P11["<b>📦&nbsp;MvcWeb.csproj</b><br/><small>net8.0;net9.0</small>"]
        P16["<b>📦&nbsp;RazorWeb.csproj</b><br/><small>net8.0;net9.0</small>"]
        click P11 "#examplesmvcwebmvcwebcsproj"
        click P16 "#examplesrazorwebrazorwebcsproj"
    end
    subgraph current["Piranha.AspNetCore.Identity.SQLite.csproj"]
        MAIN["<b>📦&nbsp;Piranha.AspNetCore.Identity.SQLite.csproj</b><br/><small>net8.0;net9.0</small>"]
        click MAIN "#identitypiranhaaspnetcoreidentitysqlitepiranhaaspnetcoreidentitysqlitecsproj"
    end
    subgraph downstream["Dependencies (12"]
        P8["<b>📦&nbsp;Piranha.AspNetCore.Identity.csproj</b><br/><small>net8.0;net9.0</small>"]
        P1["<b>📦&nbsp;Piranha.csproj</b><br/><small>net8.0;net9.0</small>"]
        P26["<b>📦&nbsp;Piranha.AspNetCore.Hosting.csproj</b><br/><small>net8.0;net9.0</small>"]
        P13["<b>📦&nbsp;Piranha.Manager.csproj</b><br/><small>net8.0;net9.0</small>"]
        P25["<b>📦&nbsp;Piranha.Manager.LocalAuth.csproj</b><br/><small>net8.0;net9.0</small>"]
        P14["<b>📦&nbsp;Piranha.Manager.Localization.csproj</b><br/><small>net8.0;net9.0</small>"]
        P8["<b>📦&nbsp;Piranha.AspNetCore.Identity.csproj</b><br/><small>net8.0;net9.0</small>"]
        P1["<b>📦&nbsp;Piranha.csproj</b><br/><small>net8.0;net9.0</small>"]
        P26["<b>📦&nbsp;Piranha.AspNetCore.Hosting.csproj</b><br/><small>net8.0;net9.0</small>"]
        P13["<b>📦&nbsp;Piranha.Manager.csproj</b><br/><small>net8.0;net9.0</small>"]
        P25["<b>📦&nbsp;Piranha.Manager.LocalAuth.csproj</b><br/><small>net8.0;net9.0</small>"]
        P14["<b>📦&nbsp;Piranha.Manager.Localization.csproj</b><br/><small>net8.0;net9.0</small>"]
        click P8 "#identitypiranhaaspnetcoreidentitypiranhaaspnetcoreidentitycsproj"
        click P1 "#corepiranhapiranhacsproj"
        click P26 "#corepiranhaaspnetcorehostingpiranhaaspnetcorehostingcsproj"
        click P13 "#corepiranhamanagerpiranhamanagercsproj"
        click P25 "#corepiranhamanagerlocalauthpiranhamanagerlocalauthcsproj"
        click P14 "#corepiranhamanagerlocalizationpiranhamanagerlocalizationcsproj"
        click P8 "#identitypiranhaaspnetcoreidentitypiranhaaspnetcoreidentitycsproj"
        click P1 "#corepiranhapiranhacsproj"
        click P26 "#corepiranhaaspnetcorehostingpiranhaaspnetcorehostingcsproj"
        click P13 "#corepiranhamanagerpiranhamanagercsproj"
        click P25 "#corepiranhamanagerlocalauthpiranhamanagerlocalauthcsproj"
        click P14 "#corepiranhamanagerlocalizationpiranhamanagerlocalizationcsproj"
    end
    P11 --> MAIN
    P16 --> MAIN
    MAIN --> P8
    MAIN --> P1
    MAIN --> P26
    MAIN --> P13
    MAIN --> P25
    MAIN --> P14
    MAIN --> P8
    MAIN --> P1
    MAIN --> P26
    MAIN --> P13
    MAIN --> P25
    MAIN --> P14

```

### API Compatibility

| Category | Count | Impact |
| :--- | :---: | :--- |
| 🔴 Binary Incompatible | 0 | High - Require code changes |
| 🟡 Source Incompatible | 0 | Medium - Needs re-compilation and potential conflicting API error fixing |
| 🔵 Behavioral change | 0 | Low - Behavioral changes that may require testing at runtime |
| ✅ Compatible | 766 |  |
| ***Total APIs Analyzed*** | ***766*** |  |

<a id="identitypiranhaaspnetcoreidentitysqlserverpiranhaaspnetcoreidentitysqlservercsproj"></a>
### identity\Piranha.AspNetCore.Identity.SQLServer\Piranha.AspNetCore.Identity.SQLServer.csproj

#### Project Info

- **Current Target Framework:** net8.0;net9.0
- **Proposed Target Framework:** net8.0;net9.0;net10.0
- **SDK-style**: True
- **Project Kind:** ClassLibrary
- **Dependencies**: 12
- **Dependants**: 0
- **Number of Files**: 0
- **Number of Files with Incidents**: 1
- **Lines of Code**: 0
- **Estimated LOC to modify**: 0+ (at least 0.0% of the project)

#### Dependency Graph

Legend:
📦 SDK-style project
⚙️ Classic project

```mermaid
flowchart TB
    subgraph current["Piranha.AspNetCore.Identity.SQLServer.csproj"]
        MAIN["<b>📦&nbsp;Piranha.AspNetCore.Identity.SQLServer.csproj</b><br/><small>net8.0;net9.0</small>"]
        click MAIN "#identitypiranhaaspnetcoreidentitysqlserverpiranhaaspnetcoreidentitysqlservercsproj"
    end
    subgraph downstream["Dependencies (12"]
        P8["<b>📦&nbsp;Piranha.AspNetCore.Identity.csproj</b><br/><small>net8.0;net9.0</small>"]
        P1["<b>📦&nbsp;Piranha.csproj</b><br/><small>net8.0;net9.0</small>"]
        P26["<b>📦&nbsp;Piranha.AspNetCore.Hosting.csproj</b><br/><small>net8.0;net9.0</small>"]
        P13["<b>📦&nbsp;Piranha.Manager.csproj</b><br/><small>net8.0;net9.0</small>"]
        P25["<b>📦&nbsp;Piranha.Manager.LocalAuth.csproj</b><br/><small>net8.0;net9.0</small>"]
        P14["<b>📦&nbsp;Piranha.Manager.Localization.csproj</b><br/><small>net8.0;net9.0</small>"]
        P8["<b>📦&nbsp;Piranha.AspNetCore.Identity.csproj</b><br/><small>net8.0;net9.0</small>"]
        P1["<b>📦&nbsp;Piranha.csproj</b><br/><small>net8.0;net9.0</small>"]
        P26["<b>📦&nbsp;Piranha.AspNetCore.Hosting.csproj</b><br/><small>net8.0;net9.0</small>"]
        P13["<b>📦&nbsp;Piranha.Manager.csproj</b><br/><small>net8.0;net9.0</small>"]
        P25["<b>📦&nbsp;Piranha.Manager.LocalAuth.csproj</b><br/><small>net8.0;net9.0</small>"]
        P14["<b>📦&nbsp;Piranha.Manager.Localization.csproj</b><br/><small>net8.0;net9.0</small>"]
        click P8 "#identitypiranhaaspnetcoreidentitypiranhaaspnetcoreidentitycsproj"
        click P1 "#corepiranhapiranhacsproj"
        click P26 "#corepiranhaaspnetcorehostingpiranhaaspnetcorehostingcsproj"
        click P13 "#corepiranhamanagerpiranhamanagercsproj"
        click P25 "#corepiranhamanagerlocalauthpiranhamanagerlocalauthcsproj"
        click P14 "#corepiranhamanagerlocalizationpiranhamanagerlocalizationcsproj"
        click P8 "#identitypiranhaaspnetcoreidentitypiranhaaspnetcoreidentitycsproj"
        click P1 "#corepiranhapiranhacsproj"
        click P26 "#corepiranhaaspnetcorehostingpiranhaaspnetcorehostingcsproj"
        click P13 "#corepiranhamanagerpiranhamanagercsproj"
        click P25 "#corepiranhamanagerlocalauthpiranhamanagerlocalauthcsproj"
        click P14 "#corepiranhamanagerlocalizationpiranhamanagerlocalizationcsproj"
    end
    MAIN --> P8
    MAIN --> P1
    MAIN --> P26
    MAIN --> P13
    MAIN --> P25
    MAIN --> P14
    MAIN --> P8
    MAIN --> P1
    MAIN --> P26
    MAIN --> P13
    MAIN --> P25
    MAIN --> P14

```

### API Compatibility

| Category | Count | Impact |
| :--- | :---: | :--- |
| 🔴 Binary Incompatible | 0 | High - Require code changes |
| 🟡 Source Incompatible | 0 | Medium - Needs re-compilation and potential conflicting API error fixing |
| 🔵 Behavioral change | 0 | Low - Behavioral changes that may require testing at runtime |
| ✅ Compatible | 794 |  |
| ***Total APIs Analyzed*** | ***794*** |  |

<a id="identitypiranhaaspnetcoreidentitypiranhaaspnetcoreidentitycsproj"></a>
### identity\Piranha.AspNetCore.Identity\Piranha.AspNetCore.Identity.csproj

#### Project Info

- **Current Target Framework:** net8.0;net9.0
- **Proposed Target Framework:** net8.0;net9.0;net10.0
- **SDK-style**: True
- **Project Kind:** ClassLibrary
- **Dependencies**: 10
- **Dependants**: 6
- **Number of Files**: 2
- **Number of Files with Incidents**: 2
- **Lines of Code**: 0
- **Estimated LOC to modify**: 4+ (at least 0.0% of the project)

#### Dependency Graph

Legend:
📦 SDK-style project
⚙️ Classic project

```mermaid
flowchart TB
    subgraph upstream["Dependants (6)"]
        P9["<b>📦&nbsp;Piranha.AspNetCore.Identity.SQLite.csproj</b><br/><small>net8.0;net9.0</small>"]
        P10["<b>📦&nbsp;Piranha.AspNetCore.Identity.SQLServer.csproj</b><br/><small>net8.0;net9.0</small>"]
        P11["<b>📦&nbsp;MvcWeb.csproj</b><br/><small>net8.0;net9.0</small>"]
        P16["<b>📦&nbsp;RazorWeb.csproj</b><br/><small>net8.0;net9.0</small>"]
        P23["<b>📦&nbsp;Piranha.AspNetCore.Identity.MySQL.csproj</b><br/><small>net8.0;net9.0</small>"]
        P24["<b>📦&nbsp;Piranha.AspNetCore.Identity.PostgreSQL.csproj</b><br/><small>net8.0;net9.0</small>"]
        click P9 "#identitypiranhaaspnetcoreidentitysqlitepiranhaaspnetcoreidentitysqlitecsproj"
        click P10 "#identitypiranhaaspnetcoreidentitysqlserverpiranhaaspnetcoreidentitysqlservercsproj"
        click P11 "#examplesmvcwebmvcwebcsproj"
        click P16 "#examplesrazorwebrazorwebcsproj"
        click P23 "#identitypiranhaaspnetcoreidentitymysqlpiranhaaspnetcoreidentitymysqlcsproj"
        click P24 "#identitypiranhaaspnetcoreidentitypostgresqlpiranhaaspnetcoreidentitypostgresqlcsproj"
    end
    subgraph current["Piranha.AspNetCore.Identity.csproj"]
        MAIN["<b>📦&nbsp;Piranha.AspNetCore.Identity.csproj</b><br/><small>net8.0;net9.0</small>"]
        click MAIN "#identitypiranhaaspnetcoreidentitypiranhaaspnetcoreidentitycsproj"
    end
    subgraph downstream["Dependencies (10"]
        P1["<b>📦&nbsp;Piranha.csproj</b><br/><small>net8.0;net9.0</small>"]
        P13["<b>📦&nbsp;Piranha.Manager.csproj</b><br/><small>net8.0;net9.0</small>"]
        P25["<b>📦&nbsp;Piranha.Manager.LocalAuth.csproj</b><br/><small>net8.0;net9.0</small>"]
        P14["<b>📦&nbsp;Piranha.Manager.Localization.csproj</b><br/><small>net8.0;net9.0</small>"]
        P26["<b>📦&nbsp;Piranha.AspNetCore.Hosting.csproj</b><br/><small>net8.0;net9.0</small>"]
        P1["<b>📦&nbsp;Piranha.csproj</b><br/><small>net8.0;net9.0</small>"]
        P13["<b>📦&nbsp;Piranha.Manager.csproj</b><br/><small>net8.0;net9.0</small>"]
        P25["<b>📦&nbsp;Piranha.Manager.LocalAuth.csproj</b><br/><small>net8.0;net9.0</small>"]
        P14["<b>📦&nbsp;Piranha.Manager.Localization.csproj</b><br/><small>net8.0;net9.0</small>"]
        P26["<b>📦&nbsp;Piranha.AspNetCore.Hosting.csproj</b><br/><small>net8.0;net9.0</small>"]
        click P1 "#corepiranhapiranhacsproj"
        click P13 "#corepiranhamanagerpiranhamanagercsproj"
        click P25 "#corepiranhamanagerlocalauthpiranhamanagerlocalauthcsproj"
        click P14 "#corepiranhamanagerlocalizationpiranhamanagerlocalizationcsproj"
        click P26 "#corepiranhaaspnetcorehostingpiranhaaspnetcorehostingcsproj"
        click P1 "#corepiranhapiranhacsproj"
        click P13 "#corepiranhamanagerpiranhamanagercsproj"
        click P25 "#corepiranhamanagerlocalauthpiranhamanagerlocalauthcsproj"
        click P14 "#corepiranhamanagerlocalizationpiranhamanagerlocalizationcsproj"
        click P26 "#corepiranhaaspnetcorehostingpiranhaaspnetcorehostingcsproj"
    end
    P9 --> MAIN
    P10 --> MAIN
    P11 --> MAIN
    P16 --> MAIN
    P23 --> MAIN
    P24 --> MAIN
    MAIN --> P1
    MAIN --> P13
    MAIN --> P25
    MAIN --> P14
    MAIN --> P26
    MAIN --> P1
    MAIN --> P13
    MAIN --> P25
    MAIN --> P14
    MAIN --> P26

```

### API Compatibility

| Category | Count | Impact |
| :--- | :---: | :--- |
| 🔴 Binary Incompatible | 0 | High - Require code changes |
| 🟡 Source Incompatible | 4 | Medium - Needs re-compilation and potential conflicting API error fixing |
| 🔵 Behavioral change | 0 | Low - Behavioral changes that may require testing at runtime |
| ✅ Compatible | 1364 |  |
| ***Total APIs Analyzed*** | ***1368*** |  |

<a id="testpiranhamanagertestspiranhamanagertestscsproj"></a>
### test\Piranha.Manager.Tests\Piranha.Manager.Tests.csproj

#### Project Info

- **Current Target Framework:** net8.0;net9.0
- **Proposed Target Framework:** net8.0;net9.0;net10.0
- **SDK-style**: True
- **Project Kind:** DotNetCoreApp
- **Dependencies**: 8
- **Dependants**: 0
- **Number of Files**: 0
- **Number of Files with Incidents**: 1
- **Lines of Code**: 0
- **Estimated LOC to modify**: 0+ (at least 0.0% of the project)

#### Dependency Graph

Legend:
📦 SDK-style project
⚙️ Classic project

```mermaid
flowchart TB
    subgraph current["Piranha.Manager.Tests.csproj"]
        MAIN["<b>📦&nbsp;Piranha.Manager.Tests.csproj</b><br/><small>net8.0;net9.0</small>"]
        click MAIN "#testpiranhamanagertestspiranhamanagertestscsproj"
    end
    subgraph downstream["Dependencies (8"]
        P13["<b>📦&nbsp;Piranha.Manager.csproj</b><br/><small>net8.0;net9.0</small>"]
        P1["<b>📦&nbsp;Piranha.csproj</b><br/><small>net8.0;net9.0</small>"]
        P26["<b>📦&nbsp;Piranha.AspNetCore.Hosting.csproj</b><br/><small>net8.0;net9.0</small>"]
        P14["<b>📦&nbsp;Piranha.Manager.Localization.csproj</b><br/><small>net8.0;net9.0</small>"]
        P13["<b>📦&nbsp;Piranha.Manager.csproj</b><br/><small>net8.0;net9.0</small>"]
        P1["<b>📦&nbsp;Piranha.csproj</b><br/><small>net8.0;net9.0</small>"]
        P26["<b>📦&nbsp;Piranha.AspNetCore.Hosting.csproj</b><br/><small>net8.0;net9.0</small>"]
        P14["<b>📦&nbsp;Piranha.Manager.Localization.csproj</b><br/><small>net8.0;net9.0</small>"]
        click P13 "#corepiranhamanagerpiranhamanagercsproj"
        click P1 "#corepiranhapiranhacsproj"
        click P26 "#corepiranhaaspnetcorehostingpiranhaaspnetcorehostingcsproj"
        click P14 "#corepiranhamanagerlocalizationpiranhamanagerlocalizationcsproj"
        click P13 "#corepiranhamanagerpiranhamanagercsproj"
        click P1 "#corepiranhapiranhacsproj"
        click P26 "#corepiranhaaspnetcorehostingpiranhaaspnetcorehostingcsproj"
        click P14 "#corepiranhamanagerlocalizationpiranhamanagerlocalizationcsproj"
    end
    MAIN --> P13
    MAIN --> P1
    MAIN --> P26
    MAIN --> P14
    MAIN --> P13
    MAIN --> P1
    MAIN --> P26
    MAIN --> P14

```

### API Compatibility

| Category | Count | Impact |
| :--- | :---: | :--- |
| 🔴 Binary Incompatible | 0 | High - Require code changes |
| 🟡 Source Incompatible | 0 | Medium - Needs re-compilation and potential conflicting API error fixing |
| 🔵 Behavioral change | 0 | Low - Behavioral changes that may require testing at runtime |
| ✅ Compatible | 36 |  |
| ***Total APIs Analyzed*** | ***36*** |  |

<a id="testpiranhatestspiranhatestscsproj"></a>
### test\Piranha.Tests\Piranha.Tests.csproj

#### Project Info

- **Current Target Framework:** net8.0;net9.0
- **Proposed Target Framework:** net8.0;net9.0;net10.0
- **SDK-style**: True
- **Project Kind:** DotNetCoreApp
- **Dependencies**: 12
- **Dependants**: 0
- **Number of Files**: 0
- **Number of Files with Incidents**: 1
- **Lines of Code**: 0
- **Estimated LOC to modify**: 0+ (at least 0.0% of the project)

#### Dependency Graph

Legend:
📦 SDK-style project
⚙️ Classic project

```mermaid
flowchart TB
    subgraph current["Piranha.Tests.csproj"]
        MAIN["<b>📦&nbsp;Piranha.Tests.csproj</b><br/><small>net8.0;net9.0</small>"]
        click MAIN "#testpiranhatestspiranhatestscsproj"
    end
    subgraph downstream["Dependencies (12"]
        P1["<b>📦&nbsp;Piranha.csproj</b><br/><small>net8.0;net9.0</small>"]
        P3["<b>📦&nbsp;Piranha.AttributeBuilder.csproj</b><br/><small>net8.0;net9.0</small>"]
        P7["<b>📦&nbsp;Piranha.ImageSharp.csproj</b><br/><small>net8.0;net9.0</small>"]
        P5["<b>📦&nbsp;Piranha.Local.FileStorage.csproj</b><br/><small>net8.0;net9.0</small>"]
        P12["<b>📦&nbsp;Piranha.Data.EF.csproj</b><br/><small>net8.0;net9.0</small>"]
        P19["<b>📦&nbsp;Piranha.Data.EF.SQLite.csproj</b><br/><small>net8.0;net9.0</small>"]
        P1["<b>📦&nbsp;Piranha.csproj</b><br/><small>net8.0;net9.0</small>"]
        P3["<b>📦&nbsp;Piranha.AttributeBuilder.csproj</b><br/><small>net8.0;net9.0</small>"]
        P7["<b>📦&nbsp;Piranha.ImageSharp.csproj</b><br/><small>net8.0;net9.0</small>"]
        P5["<b>📦&nbsp;Piranha.Local.FileStorage.csproj</b><br/><small>net8.0;net9.0</small>"]
        P12["<b>📦&nbsp;Piranha.Data.EF.csproj</b><br/><small>net8.0;net9.0</small>"]
        P19["<b>📦&nbsp;Piranha.Data.EF.SQLite.csproj</b><br/><small>net8.0;net9.0</small>"]
        click P1 "#corepiranhapiranhacsproj"
        click P3 "#corepiranhaattributebuilderpiranhaattributebuildercsproj"
        click P7 "#corepiranhaimagesharppiranhaimagesharpcsproj"
        click P5 "#corepiranhalocalfilestoragepiranhalocalfilestoragecsproj"
        click P12 "#datapiranhadataefpiranhadataefcsproj"
        click P19 "#datapiranhadataefsqlitepiranhadataefsqlitecsproj"
        click P1 "#corepiranhapiranhacsproj"
        click P3 "#corepiranhaattributebuilderpiranhaattributebuildercsproj"
        click P7 "#corepiranhaimagesharppiranhaimagesharpcsproj"
        click P5 "#corepiranhalocalfilestoragepiranhalocalfilestoragecsproj"
        click P12 "#datapiranhadataefpiranhadataefcsproj"
        click P19 "#datapiranhadataefsqlitepiranhadataefsqlitecsproj"
    end
    MAIN --> P1
    MAIN --> P3
    MAIN --> P7
    MAIN --> P5
    MAIN --> P12
    MAIN --> P19
    MAIN --> P1
    MAIN --> P3
    MAIN --> P7
    MAIN --> P5
    MAIN --> P12
    MAIN --> P19

```

### API Compatibility

| Category | Count | Impact |
| :--- | :---: | :--- |
| 🔴 Binary Incompatible | 0 | High - Require code changes |
| 🟡 Source Incompatible | 0 | Medium - Needs re-compilation and potential conflicting API error fixing |
| 🔵 Behavioral change | 0 | Low - Behavioral changes that may require testing at runtime |
| ✅ Compatible | 9130 |  |
| ***Total APIs Analyzed*** | ***9130*** |  |

