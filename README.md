graph TB
    %% Presentation Layer Package
    subgraph Presentation_Layer ["Package: Presentation Layer (UI / API)"]
        direction LR
        API[API Endpoints / Routers] --> Services[Request Services]
    end

    %% Business Logic Layer Package
    subgraph Business_Logic_Layer ["Package: Business Logic Layer (Core Domain)"]
        direction TB
        Facade[HBnB Application Facade]
        
        subgraph Domain_Models ["Sub-Package: Core Models"]
            M1[User Model]
            M2[Place Model]
            M3[Review Model]
            M4[Amenity Model]
        end
        
        Facade --> Domain_Models
    end

    %% Persistence Layer Package
    subgraph Persistence_Layer ["Package: Persistence Layer (Data Access)"]
        direction LR
        Repo[Data Repositories / DAOs] --> DB[(Database / In-Memory Storage)]
    end

    %% Inter-Layer Communication via Facade
    Services -->|1. Invokes Unified Interface| Facade
    Domain_Models -->|2. Persists / Fetches Data| Repo

    %% Styling for Professional Look
    style Presentation_Layer fill:#f9f0ff,stroke:#d3adf7,stroke-width:2px
    style Business_Logic_Layer fill:#e6f7ff,stroke:#91d5ff,stroke-width:2px
    style Persistence_Layer fill:#f6ffed,stroke:#b7eb8f,stroke-width:2px
    style Facade fill:#fffbe6,stroke:#ffe58f,stroke-width:2px,font-weight:bold
