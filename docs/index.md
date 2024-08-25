# FlyMatic Project Documentation Index

## Overview
FlyMatic is an drone project that integrates both software and hardware components to enable precision control. This documentation provides detailed information on the repositories, project architecture, and key functionalities.

### Software Repositories
- [STM32 Firmware Repository](https://github.com/inpgbburda/Stm32f401.git): Contains the firmware for the STM32F4 microcontroller, including FreeRTOS and motor control logic.
- [Raspberry Pi Software Repository](https://github.com/TomBartDrone/drone_code.git): Contains the real-time Linux code for sensor data processing and communication.

### Hardware Repositories
- **To Be Determined** (Pending completion)

## Project Architecture

``` mermaid
    graph TD
    
    A[Raspberry pi
    Real Time Linux/ C++] <--> |I2C| B[Accelleration sensor]
    A --> |Spi| C[Stm32F4 
    FreeRTOS/C]
    C --> |Pwm| D[Electric motors]
```