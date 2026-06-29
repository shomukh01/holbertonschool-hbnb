graph TD
    %% الطبقات الثلاث
    subgraph Presentation ["Presentation Layer (API & Services)"]
        API[API Endpoints] --> Svc[Services]
    end

    subgraph Business ["Business Logic Layer (Models)"]
        Facade[HBnB Facade]
        Models[User, Place, Review, Amenity]
        Facade --> Models
    end

    subgraph Persistence ["Persistence Layer (Storage)"]
        Repo[Repositories / DAOs] --> DB[(Database)]
    end

    %% مسارات التواصل
    Svc -->|Calls| Facade
    Models -->|Queries| Repo
