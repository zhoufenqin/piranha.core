# Architecture Diagram

Piranha.Core is a modular .NET CMS composed of reusable class libraries, data-provider packages, identity integrations, and sample host applications. The solution separates presentation, application services, persistence, and infrastructure so the same core can be hosted with different UI, storage, and database combinations.

## Application Architecture

```mermaid
flowchart TD
    subgraph Client["Client Layer"]
        Browser["Browser and CMS users"]
        ApiClients["Headless API clients"]
    end
    subgraph Presentation["Presentation Layer - ASP.NET Core"]
        Mvc["MvcWeb and RazorWeb hosts"]
        Manager["Piranha.Manager admin UI"]
        WebApi["Piranha.WebApi controllers"]
        SignalR["PreviewHub realtime preview"]
    end
    subgraph App["Application Layer - Piranha Core"]
        Api["IApi facade"]
        Services["Content, Page, Post, Media, Site services"]
        Types["AttributeBuilder and content type runtime"]
    end
    subgraph Data["Data Layer - EF Core"]
        Repos["Repository interfaces and EF repositories"]
        Db["Provider specific DbContext implementations"]
        Sqlite[("SQLite")]
        SqlServer[("SQL Server")]
        Postgres[("PostgreSQL")]
        Mysql[("MySQL")]
    end
    subgraph Infra["Infrastructure Layer"]
        Cache["Memory or distributed cache"]
        Files["Local file storage"]
        Blob["Azure Blob storage"]
        Images["ImageSharp processor"]
        Identity["ASP.NET Core Identity"]
    end

    Browser -->|"authoring and site requests"| Mvc
    Browser -->|"admin requests"| Manager
    ApiClients -->|"REST calls"| WebApi
    Manager -->|"preview updates"| SignalR
    Mvc -->|"content rendering"| Api
    Manager -->|"CRUD operations"| Api
    WebApi -->|"read operations"| Api
    Api -->|"business orchestration"| Services
    Services -->|"schema and block metadata"| Types
    Services -->|"queries and persistence"| Repos
    Repos -->|"EF Core access"| Db
    Db -->|"provider connections"| Sqlite
    Db -->|"provider connections"| SqlServer
    Db -->|"provider connections"| Postgres
    Db -->|"provider connections"| Mysql
    Services -->|"cache lookups"| Cache
    Services -->|"media storage"| Files
    Services -->|"cloud media storage"| Blob
    Services -->|"image transformations"| Images
    Manager -->|"admin authentication"| Identity
    Mvc -->|"front end auth integration"| Identity
```

### Technology Stack Summary

| Layer | Technology | Version | Purpose |
|---|---|---:|---|
| Presentation | ASP.NET Core MVC and Razor | net8.0, net9.0 | Hosts example sites, admin UI, and API endpoints |
| Application | Piranha core services via `IApi` | 12.1.0 | Central facade for content, site, page, post, media, and taxonomy workflows |
| Data | Entity Framework Core providers | 8.0.x, 9.0.x | Database access through provider-specific packages |
| Identity | ASP.NET Core Identity | 8.0.x, 9.0.x | Manager and application authentication integration |
| Storage | Local filesystem and Azure Blob Storage | Azure.Storage.Blobs 12.18.0 | Media persistence backends |
| Media | SixLabors ImageSharp | 2.1.13 | Image resizing and transformation |

### Data Storage & External Services

The core runtime persists CMS data through Entity Framework Core with interchangeable SQLite, SQL Server, PostgreSQL, and MySQL providers. Media can be stored on the local filesystem or Azure Blob Storage, while the admin experience also uses SignalR for preview notifications and ASP.NET Core Identity for authenticated management flows.

### Key Architectural Decisions

- Uses a central `IApi` facade over internal services and repositories so host applications and the manager UI share the same content workflows.
- Keeps the persistence layer provider-agnostic by placing EF Core implementations and database providers in separate projects from the core domain libraries.
- Treats infrastructure concerns such as storage, caching, image processing, and identity as pluggable modules that can be enabled by startup extensions in the host application.

## Component Relationships

```mermaid
flowchart LR
    subgraph Presentation["Presentation"]
        Hosts["MvcWeb and RazorWeb"]
        Admin["Manager controllers"]
        PublicApi["WebApi controllers"]
    end
    subgraph Business["Business Logic"]
        Facade["Api facade"]
        CoreSvc["Internal content services"]
        Builder["Content type builder"]
    end
    subgraph DataAccess["Data Access"]
        RepoIf["Repository interfaces"]
        RepoImpl["EF repositories"]
        DbCtx["DbContext providers"]
    end
    subgraph Infra["Infrastructure"]
        Preview["PreviewHub"]
        CacheComp["Memory or distributed cache"]
        StorageComp["Storage adapters"]
        ImageComp["Image processor"]
        IdentityComp["Identity providers"]
    end

    Hosts -->|"renders and edits content through"| Facade
    Admin -->|"delegates CRUD and publish actions"| Facade
    PublicApi -->|"fetches content and media"| Facade
    Admin -->|"pushes preview updates"| Preview
    Facade -->|"coordinates business rules"| CoreSvc
    CoreSvc -->|"loads schema metadata"| Builder
    CoreSvc -->|"uses contracts from"| RepoIf
    RepoIf -->|"implemented by"| RepoImpl
    RepoImpl -->|"persists through"| DbCtx
    CoreSvc -->|"reads and invalidates"| CacheComp
    CoreSvc -->|"stores media via"| StorageComp
    CoreSvc -->|"resizes assets with"| ImageComp
    Admin -.->|"protected by"| IdentityComp
    Hosts -.->|"can enable"| IdentityComp
```

### Component Inventory

| Component | Layer | Type | Responsibility |
|---|---|---|---|
| `MvcWeb` and `RazorWeb` | Presentation | Host applications | Configure Piranha and serve example CMS sites |
| `Piranha.Manager` controllers | Presentation | MVC controllers | Handle admin editing, publishing, media, site, and config operations |
| `Piranha.WebApi` controllers | Presentation | API controllers | Expose headless read-oriented CMS endpoints |
| `Piranha.Api` | Business Logic | Facade service | Aggregates the core service surface behind `IApi` |
| Internal page, post, media, site services | Business Logic | Domain services | Apply CMS business rules and call repositories and infrastructure |
| `ContentTypeBuilder` and runtime type services | Business Logic | Metadata builder | Assemble and manage dynamic content schemas |
| Repository interfaces | Data Access | Abstractions | Define persistence contracts for aliases, pages, posts, media, sites, and taxonomies |
| EF repositories | Data Access | Repository implementations | Translate core persistence contracts to EF Core queries |
| Provider-specific `DbContext` classes | Data Access | DbContext | Connect EF Core to SQLite, SQL Server, PostgreSQL, and MySQL |
| `PreviewHub` | Infrastructure | SignalR hub | Notifies connected clients about live preview updates |
| `ICache` implementations | Infrastructure | Cache adapters | Provide memory and distributed caching options |
| `IStorage` implementations | Infrastructure | Storage adapters | Persist media to local files or Azure Blob Storage |
| `IImageProcessor` implementation | Infrastructure | Media processor | Generates transformed image versions |
| Identity provider projects | Infrastructure | Auth adapters | Integrate ASP.NET Core Identity with provider-specific stores |
