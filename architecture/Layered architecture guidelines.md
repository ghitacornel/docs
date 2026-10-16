Layered Architecture
```mermaid
graph v
    subgraph Database Layer
        DB(Database)
    end
    subgraph Persistence Layer
        subgraph Data Model
            Projection--derived from-->Entity
        end
        Entity--maps-->DB
        Repository--manages-->Entity
        Repository--uses-->Projection
    end
    subgraph Business Layer
        Service--uses-->Entity
        Service--delegates database calls to-->Repository
        Service--delegates domain mapping to-->Mapper
        Mapper--maps-->Entity
    end
    subgraph Presentation Layer
        subgraph Data Model
            Request
            Response
        end
        Controller--receives-->Request
        Controller--returns-->Response
        Controller--delegates to-->Service
        Request--sent to-->Service
        Response--built by-->Service
    end
```
---
