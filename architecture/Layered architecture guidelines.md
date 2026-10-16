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
        Service--delegates database calls to-->Repository
        Service--delegates domain mapping to-->Mapper
        Service--delegates REST calls-->REST(Rest Client)
        Service--delegates WEB calls-->WEB(WEB Client)
        Service--send messages-->MQ(Message Queue)
        Service--receive messages-->MQ(Message Queue)
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
