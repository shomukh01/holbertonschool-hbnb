graph TB
    %% Presentation Layer
    subgraph Presentation_Layer [Presentation Layer]
        A[API Endpoints / Routers] --> B[Services / Controllers]
    end

    %% Business Logic Layer
    subgraph Business_Logic_Layer [Business Logic Layer]
        direction TB
        Facade[HBnB Facade Interface]
        
        subgraph Models [Core Models]
            M1[User]
            M2[Place]
            M3[Review]
            M4[Amenity]
        end
        
        Facade --> Models
    end

    %% Persistence Layer
    subgraph Persistence_Layer [Persistence Layer]
        Repository[Data Repositories / DAOs] --> DB[(Database / Storage)]
    end

    %% Communication Pathways via Facade
    Presentation_Layer -->|Calls Unified Interface| Facade
    Business_Logic_Layer -->|Data Retrieval / Persistence| Persistence_Layer

    %% Styling
    style Presentation_Layer fill:#f9f0ff,stroke:#d3adf7,stroke-width:2px
    style Business_Logic_Layer fill:#e6f7ff,stroke:#91d5ff,stroke-width:2px
    style Persistence_Layer fill:#f6ffed,stroke:#b7eb8f,stroke-width:2px
    style Facade fill:#fffbe6,stroke:#ffe58f,stroke-width:2px,font-weight:bold
2. Explanatory Notes
Layer Responsibilities
Presentation Layer (Services, API): This layer acts as the entry point for all client interactions (e.g., mobile apps, web frontends). It manages HTTP requests, handles API routing, validates incoming payload schemas, and formats JSON responses. It never directly mutates data or queries the database; instead, it delegates tasks down.

Business Logic Layer (Models): The heart of the HBnB application. This layer enforces real-world business constraints (e.g., ensuring a host cannot review their own place, or validating that a price is positive). It houses the core entities—User, Place, Review, and Amenity—and handles the computations, state changes, and workflows between them.

Persistence Layer: This layer is isolated from business definitions and strictly handles data durability. It uses Data Access Objects (DAOs) or the Repository pattern to map in-memory application objects into database records (whether SQL, NoSQL, or an in-memory development dictionary) and abstract away the underlying database syntax.

The Role of the Facade Pattern
In this architecture, the HBnB Facade serves as a structural gateway between the Presentation Layer and the complex inner workings of the Business Logic and Persistence Layers.

Decoupling: The Presentation Layer does not need to know which model is interacting with which repository to fulfill a request. It simply talks to the Facade (e.g., facade.create_user(data)).

Simplification: Instead of the API routers importing and managing connections to four different models and repositories, they consume a single, unified interface.

Maintainability: If the inner logic of how a Place links to an Amenity changes, the API routes remain entirely untouched. Only the implementation behind the Facade changes, ensuring a highly modular and easily testable codebase.
