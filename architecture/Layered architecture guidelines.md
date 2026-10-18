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
        subgraph Business
            Repository
        end
        Entity--maps-->DB
        Repository--manages-->Entity
        Repository--uses-->Projection
    end
    subgraph Business Layer
        MQ(Message Queue)
        REST(Rest Client)
        WEB(WEB Client)
        Service--delegates database calls to-->Repository
        Service--delegates domain mapping to-->Mapper
        Service--delegates REST calls-->REST
        Service--delegates WEB calls-->WEB
        Service--send messages-->MQ
        Service--receive messages-->MQ
        Service--delegates-->Service
    end
    subgraph Presentation Layer
        subgraph Data Model
            Request
            Response
        end
        Controller--receives-->Request
        Controller--returns-->Response
        Controller--delegates-->Service
        Request--sent to-->Service
        Response--built by-->Service
    end
    Client--calls-->Controller
```
---
