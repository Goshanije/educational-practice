```mermaid
classDiagram
    direction TB

    class IRobotAI~out TCommand~ {
        <<interface>>
        +GetCommand() TCommand
    }

    class IDevice~in TCommand~ {
        <<interface>>
        +ExecuteCommand(TCommand command) string
    }

    class Device~TCommand~ {
        <<abstract>>
        +ExecuteCommand(TCommand command)* string
    }

    class ShooterAI {
        -int counter
        +GetCommand() ShooterCommand
    }

    class BuilderAI {
        -int counter
        +GetCommand() BuilderCommand
    }

    class Mover {
        +ExecuteCommand(IMoveCommand command) string
    }

    class ShooterMover {
        +ExecuteCommand(IShooterMoveCommand command) string
    }

    class Robot~TCommand~ {
        -IRobotAI~TCommand~ ai
        -IDevice~TCommand~ device
        +Start(int steps) IEnumerable~string~
    }

    class RobotFactory {
        +Create~TCommand~(IRobotAI~TCommand~ ai, IDevice~TCommand~ executor)\$ Robot~TCommand~
    }

    IRobotAI <|.. ShooterAI
    IRobotAI <|.. BuilderAI
    IDevice <|.. Device
    Device <|-- Mover
    Device <|-- ShooterMover

    Robot --> IRobotAI : controls
    Robot --> IDevice : dispatches
    RobotFactory ..> Robot : creates

    style IRobotAI fill:#48b0d6,stroke-width:2px,color:#fff
    style IDevice fill:#48b0d6,,stroke-width:2px,color:#fff
    style Device fill:#48b0d6,stroke-width:2px,color:#fff
    style ShooterAI fill:#48b0d6,stroke-width:1px,color:#fff
    style BuilderAI fill:#48b0d6,stroke-width:1px,color:#fff
    style Mover fill:#48b0d6,stroke-width:1px,color:#fff
    style ShooterMover fill:#48b0d6,stroke-width:1px,color:#fff
    style Robot fill:#48b0d6,stroke-width:2px,color:#fff
    style RobotFactory fill:#48b0d6,stroke-width:1px,color:#fff
```
