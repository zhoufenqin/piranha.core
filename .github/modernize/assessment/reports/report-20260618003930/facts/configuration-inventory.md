# Configuration & Externalized Settings Inventory

Piranha.Core has a relatively small but clear configuration footprint centered on .NET build properties, example host `appsettings` files, launch profiles, and startup extension methods. Configuration is mostly local to the host application, with secrets supplied through connection strings and optional Azure Blob Storage settings rather than a separate remote configuration service.

## Configuration Sources

| Source | Type | Path/Location | Notes |
|---|---|---|---|
| `Directory.Build.props` | MSBuild properties | `D:\a\piranha.core\piranha.core\Directory.Build.props` | Shared target frameworks, package metadata, documentation, and CI build settings |
| `Directory.Build.targets` | MSBuild targets | `D:\a\piranha.core\piranha.core\Directory.Build.targets` | Shared solution-level build customizations |
| `appsettings.json` | Runtime config | `D:\a\piranha.core\piranha.core\examples\MvcWeb\appsettings.json` | Logging, allowed hosts, and connection strings |
| `appsettings.Development.json` | Runtime override | `D:\a\piranha.core\piranha.core\examples\MvcWeb\appsettings.Development.json` | Development logging overrides |
| `appsettings.json` | Runtime config | `D:\a\piranha.core\piranha.core\examples\RazorWeb\appsettings.json` | Logging, allowed hosts, and connection strings |
| `appsettings.Development.json` | Runtime override | `D:\a\piranha.core\piranha.core\examples\RazorWeb\appsettings.Development.json` | Development logging overrides |
| `launchSettings.json` | Launch profile | `D:\a\piranha.core\piranha.core\examples\MvcWeb\Properties\launchSettings.json` | HTTP, HTTPS, IIS Express, and `ASPNETCORE_ENVIRONMENT` |
| `launchSettings.json` | Launch profile | `D:\a\piranha.core\piranha.core\examples\RazorWeb\Properties\launchSettings.json` | HTTP, HTTPS, IIS Express, and `ASPNETCORE_ENVIRONMENT` |
| Startup extensions in `Program.cs` | Code-based config | `D:\a\piranha.core\piranha.core\examples\MvcWeb\Program.cs` and `examples\RazorWeb\Program.cs` | Enables manager, file storage, TinyMCE, memory cache, EF, identity, and security |

## Build Profiles

| Profile | Activation | Purpose | Key Dependencies/Plugins |
|---|---|---|---|
| `Debug` | Default local build configuration | Local development and testing | Standard project references and symbols |
| `Release` | Explicit build configuration | Packaging and release builds | Standard project references with optimized build output |
| `net8.0` target | Multi-target compilation from `Directory.Build.props` | Produce packages for .NET 8 consumers | 8.0.x EF Core, Identity, and ASP.NET package variants |
| `net9.0` target | Multi-target compilation from `Directory.Build.props` | Produce packages for .NET 9 consumers | 9.0.x EF Core, Identity, and ASP.NET package variants |
| GitHub Actions CI build | `GITHUB_ACTIONS=true` | Enable CI-friendly metadata and deterministic packaging | Continuous integration MSBuild properties |

## Runtime Profiles

| Profile | Activation Method | Config Files | Key Overrides |
|---|---|---|---|
| `Development` | `ASPNETCORE_ENVIRONMENT=Development` via launch settings | `appsettings.json`, `appsettings.Development.json` | More verbose logging and local debug defaults |
| Default host runtime | No explicit environment variable | `appsettings.json` | Base logging, `AllowedHosts`, and connection strings |

## Properties Inventory

| Property Key | Default | Profiles | Source |
|---|---|---|---|
| `Logging:LogLevel:Default` | `Information` | Default, Development override possible | Example `appsettings.json` |
| `Logging:LogLevel:Microsoft` | `Warning` | Default, Development override possible | Example `appsettings.json` |
| `AllowedHosts` | `*` | Default | Example `appsettings.json` |
| `ConnectionStrings:piranha` | SQLite file path | Default | Example `appsettings.json` |
| `ConnectionStrings:blobstorage` | Present in examples | Default | Example `appsettings.json` |
| `ASPNETCORE_ENVIRONMENT` | `Development` in launch profiles | Development | `launchSettings.json` |
| `TargetFrameworks` | `net8.0;net9.0` | Build-wide | `Directory.Build.props` |
| `Version` | `12.1.0` | Build-wide | `Directory.Build.props` |

## Startup Parameters & Resource Requirements

| Service | JVM/Runtime Options | Memory | Instance Count |
|---|---|---|---|
| `MvcWeb` | Standard ASP.NET Core process options from launch settings | Not explicitly configured | 1 in example setup |
| `RazorWeb` | Standard ASP.NET Core process options from launch settings | Not explicitly configured | 1 in example setup |
| Library projects | Not directly executable | Not applicable | Not applicable |

## Startup Dependency Chain

1. Host app loads `appsettings` and launch profile environment.
2. Host app calls `AddPiranha` and startup extensions to register EF, identity, cache, storage, manager UI, and TinyMCE.
3. Host app builds the ASP.NET Core pipeline and calls `UsePiranha`.
4. `UsePiranha` initializes the `IApi` scope and makes the CMS runtime, manager routes, and identity integration available.

## Secrets & Sensitive Configuration

| Secret Reference | Type | Storage |
|---|---|---|
| `ConnectionStrings:piranha` | Database connection string | Local config file in examples, masked at deployment time |
| `ConnectionStrings:blobstorage` | Cloud storage connection string | Local config file in examples, masked at deployment time |

### Secrets Provisioning Workflow

The repository examples keep secrets in local configuration files for development convenience, but production deployment is expected to inject database and storage credentials through standard ASP.NET Core configuration sources. No dedicated Key Vault, Vault, or remote secrets provider integration is declared in source, so the effective workflow is host configuration source to ASP.NET Core configuration binding to Piranha startup extensions and EF or storage registrations.

## Feature Flags

| Flag Name | Default | Controlled By |
|---|---|---|
| Razor runtime compilation | Disabled unless enabled by startup | `PiranhaServiceBuilder.AddRazorRuntimeCompilation` |
| Security extension permissions | Off until configured | `UseSecurity` startup configuration |
| Cache backend selection | Memory cache in examples | Startup extension choice such as `UseMemoryCache` or distributed cache registration |
| Storage backend selection | Local file storage in examples | Startup extension choice such as `UseFileStorage` or `UseBlobStorage` |

## Framework & Runtime Versions

| Component | Version | Source |
|---|---:|---|
| .NET target frameworks | net8.0, net9.0 | `Directory.Build.props` |
| Piranha package version | 12.1.0 | `Directory.Build.props` |
| ASP.NET Core shared framework | .NET 8 and 9 line | Framework references in host and library projects |
| Entity Framework Core providers | 8.0.0, 8.0.11, 9.0.0, 9.0.4 | Provider-specific `.csproj` files |
| ASP.NET Core Identity EF | 8.0.0, 9.0.0 | Identity `.csproj` files |
| Azure Storage Blobs | 12.18.0 | `Piranha.Azure.BlobStorage.csproj` |
| ImageSharp | 2.1.13 | `Piranha.ImageSharp.csproj` |
| Markdig | 0.40.0 | `Piranha.csproj` |
| Newtonsoft.Json | 13.0.3 | `Piranha.csproj` |
