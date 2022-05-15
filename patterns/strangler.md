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
In the ideal world this is where no applicaitons point to the Original Sytem and the Original System can be removed. You might even want to remove the Decoupling Layer, but my strong suggestion is to keep it since it provides a lot of benefits by itself. One of them - the ability to make changes easier - we have already seen, but there are alot more.

``` mermaid
graph TD
    A1 --> D
    A2 --> D
    A3 --> D
    A4 --> D
    D(Decoupling Layer) -.-> O(Original System)
    D --> N(New System)
```
