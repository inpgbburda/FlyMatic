# Motor Control for Propulsion System

## Overview
This document outlines the control of electric motors that drive the drone's propellers. The motors are controlled using PWM signals, which are modulated to adjust the speed and direction of the propellers.

## Hardware Components
- **Motors:** RCX 1806 2400kV (Clockwise and Counterclockwise)
- **Motor Drivers:** Brushless ESC 20A 2-3S with a built-in BEC 2A

## Controlling Motor Drivers

### PWM Configuration
- **Frequency:** 50 Hz
- **Duty Cycle:** 5% (1ms) to 10% (2ms) (corresponding to minimum and maximum speed)

### Relationship Between PWM and Motor Speed
The PWM signal's duty cycle directly controls the motor speed. A higher duty cycle increases the speed, while a lower duty cycle decreases it.

### Practical Implementation
The PWM signals are generated by the STM32 microcontroller running FreeRTOS. The values are dynamically adjusted based on inputs from the accelerometer and gyroscope data.

## Related Sections
- [RTOS Configuration](rtos.md): For details on task scheduling related to motor control.

## Software solution

Software Architecture  
![Alt text](images/MotorCtrlArchitecture.drawio.png)

```mermaid
    ---
    title: CalculateMotorsSets()
    ---
    flowchart TD
        Start(["Start"]) --> A["Get latest power requests"]
        A --> B["Calculate new PWM values"]
        B --> C["Apply new PWM values"]
        C --> Stop(["Stop"])
```

```mermaid
    ---
    title: Main Application Sequence
    ---
    sequenceDiagram
        participant Task_1 as Task_1
        participant Task_2 as Task_2
        participant Spi_Hw as Spi_Hw
        participant Pwm_Hw as Pwm_Hw
        participant P1 as Rtos_Queue
        Spi_Hw -) Task_1: MessRxCompleted()
        Task_1 ->>+ P1: SetNewValues()
        P1 -->>- Task_1: 
        Task_1 ->>+ Spi_Hw: SpiReadIt()
        Spi_Hw -->>- Task_1: 
        Task_2 ->>+ P1: GetLastValues()
        P1 -->>- Task_2: 
        Task_2 ->>+ Pwm_Hw: UpdatePwm()
        Pwm_Hw -->>- Task_2: end
```
