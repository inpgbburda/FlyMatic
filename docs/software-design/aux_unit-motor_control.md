# Motor Control for Propulsion System

## Related Sections
- [AuxUnit - RTOS Configuration](aux_unit-rtos.md): For details on task scheduling related to motor control.

## Software solution

### Static Architecture
![alt text](../images/MotorCtrlArchitecture.drawio.png)

### Dynamic Architecture
```puml
@startuml
title CalculateMotorsSets()

participant "RTOS"       as RTOS
participant "Task_1"     as Task_1
participant "Task_2"     as Task_2
participant "Spi_Hw"     as Spi_Hw
participant "Pwm_Hw"     as Pwm_Hw
queue       "RTOS_Queue" as P1

RTOS -> Task_1 : StartTask_1
activate Task_1

Task_1 ->> P1 : SetNewValues()
activate P1

P1 -->> Task_1 :
deactivate P1

Task_1 ->> Spi_Hw : SpiReadIt()
activate Spi_Hw 

Spi_Hw -->> Task_1 :
deactivate Spi_Hw
deactivate Task_1

loop infinite
Task_2 ->> P1 : GetLastValues()
activate Task_2
activate P1

P1 -->> Task_2 : 
deactivate P1

Task_2 ->> Pwm_Hw : UpdatePwm()
activate Pwm_Hw

Pwm_Hw -->> Task_2 :
deactivate Pwm_Hw
deactivate Task_2

Spi_Hw -> Task_1 : MessRxCompleted()
activate Task_1

Task_1 ->> P1 : SetNewValues()
activate P1

P1 -->> Task_1 :
deactivate P1

Task_1 ->> Spi_Hw : SpiReadIt()
activate Spi_Hw 

Spi_Hw -->> Task_1 :
deactivate Spi_Hw
deactivate Task_1
end
@enduml
```

### Detailed Design
```puml
@startuml

scale 2
title MotorCtrlExecutePeriodic()

start
:Get latest power requests;
if (item succesfully rceived from queue?) is (yes) then
repeat
:Calculate new PWM values;
:Apply new PWM values;
backward: motor++;
repeat while (motor<MOTORS_NUMBER?) is (yes) not (no)
else (no)

endif
stop

@enduml
```

```puml
@startuml

scale 2
title ReceiverCallRxCompleted()

start
:Notify Receiver main function;
note right 
    Set the xHigherPriorityTaskWoken to True,
    when higher Prio Task scheduled
end note
:portYIELD_FROM_ISR(xHigherPriorityTaskWoken);
note right 
    Immediately switch context,
    if xHigherPriorityTaskWoken set to True,
end note
stop
@enduml
```

```puml
@startuml

scale 2
title ReceiverExecute()

start
:Request Asynchronous SPI read;
:ulTaskNotifyTake();
note right 
    Wait for the SPI finish notification 
end note
:xQueueSendToFront();
stop
@enduml
```