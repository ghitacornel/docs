Simple test (Input vs Output)
```mermaid
graph v
    subgraph Targeted Method
        Method--receives-->Input
        Method--returns-->Result
    end
    subgraph Test Method
        subgraph Given
            SI(Specific Input)
            ER(Expected Result)
        end
        subgraph When
            MI(Method Invocation)
            Test--builds-->SI
            Test--builds-->ER
            Test--performs-->MI
            MI--invoked with-->SI
            MI--invokes-->Method
        end
        subgraph Then
            AR(Actual Result)
            MI--returns-->AR
            AR--is compared with-->ER
        end
    end
```
---
Simple test (Input vs Exception)
```mermaid
graph v
    subgraph Targeted Method
        Method--receives-->Input
        Method--throws-->Exception
    end
    subgraph Test Method
        subgraph Given
            SI(Specific Input)
            EE(Expected Exception)
        end
        subgraph When
            MI(Method Invocation)
            Test--builds-->SI
            Test--builds-->EE
            Test--performs-->MI
            MI--invoked with-->SI
            MI--invokes-->Method
        end
        subgraph Then
            AE(Actual Exception)
            MI--throws-->AE
            AE--is compared with-->EE
        end
    end
```
---
Simple test (Mock interaction)
```mermaid
graph v
    subgraph Targeted Method
        OM1(Other Method 1)
        OM1(Other Method 2)
        Method--receives-->Input
        Method--calls-->OM1
        Method--calls-->OM2
    end
    subgraph Test Method
        subgraph Given
            SI(Specific Input)
            Mock1
            Mock2
        end
        subgraph When
            MI(Method Invocation)
            Test--builds-->SI
            Test--builds and defines behavior-->Mock1
            Test--builds and defines behavior-->Mock2
            Mock1--injected-->Method
            Mock2--injected-->Method
            Mock1--mocks-->OM1
            Mock2--mocks-->OM2
            Test--performs-->MI
            MI--invoked with-->SI
            MI--invokes-->Method
        end
        subgraph Then
            Interaction
            Test--checks-->Interaction
            Interaction--checks in order of calls-->Mock1
            Interaction--checks in order of calls-->Mock2
        end
    end
```
---
Simple test (Mock interaction with dynamic input)
```mermaid
graph v
    subgraph Targeted Method
        OM(Other Method)
        Method--receives-->Input
        Method--calls-->OM
    end
    subgraph Test Method
        subgraph Given
            SI(Specific Input)
            Mock
            MCI(Mock Call Input)
            EMCI(Expected Mock Call Input)
        end
        subgraph When
            MI(Method Invocation)
            Test--builds-->SI
            Test--builds and defines behavior-->Mock
            Test--builds-->MCI
            Test--builds-->EMCI
            Mock--injected-->Method
            Mock--mocks-->OM
            Mock--uses-->MCI
            Test--performs-->MI
            MI--invoked with-->SI
            MI--invokes-->Method
        end
        subgraph Then
            Interaction
            Test--checks-->Interaction
            Interaction--checks-->Mock
            Interaction--checks-->MCI--is compared with-->EMCI
        end
    end
```