<!--
``` mermaid
```
-->

# Strangler Pattern
This pattern is helpful when trying to completely or partially replace old systems with new ones. Instead of having to go with the "big bang" approach and change everything at once you can do a gradual shifts in order to reach your end goal.

## Stage 0
It all begins with having applications A1-A4 tightly coupled to the Original System (OS). Changing the OS will directly effect all of the applications connected to it.

``` mermaid
graph TD
    A1 --> O(Original System)
    A2 --> O
    A3 --> O
    A4 --> O
```

## Stage 1
The first change is to add a Decoupling Layer which removes the direct dependency between one or more of the applications and the original system. Some changes to the applications using the Decoupling Layer might be needed like for example configuration.

``` mermaid
graph TD
    A1 --> O(Original System)
    A2 --> O
    A3 --> I
    A4 --> I
    I(Decoupling Layer) --> O
```

## Stage 2
The New System is now ready to take over some of the work from the Original System so the Decoupling Layer is changed to direct that trafic to its new destination.

``` mermaid
graph TD
    A1 --> O(Original System)
    A2 --> O
    A3 --> D
    A4 --> D
    D(Decoupling Layer) -.-> O
    D --> N(New System)
```

## Stage 3
In the ideal world this is where no applications point to the Original System and it can be removed. You might be tempted to remove the Decoupling Layer, but my strong suggestion is to keep it since it provides a lot of benefits by itself. One of them - the ability to make changes easier - we have already seen, but there are alot more. If you keep the decoupling layer just be careful so you don't build that into a new mononlith!

``` mermaid
graph TD
    A1 --> D
    A2 --> D
    A3 --> D
    A4 --> D
    D(Decoupling Layer) -.-> O(Original System)
    D --> N(New System)
    style O stroke-dasharray: 5 5
```

### Example of using a micro service architecture to implement the Decoupling Layer
The micro services in this case could be integrations and the orchestration service might be implementing some business rules.

``` mermaid
flowchart TB
    A1-->AM
    A2-->AM
    A3-->AM
    A4-->AM
    subgraph DL [Decoupling Layer]
        direction TB
        AM(API Management) --> b1 & b2(microservice)
        b1(orchestration service)--> b2 & b3(microservice) & b4(microservice)
    end
    b2 --> N(New System)
    b3 --> N
    b4 --> N
    
```
