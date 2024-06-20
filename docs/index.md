# Welcome to FlyMatic

## Overview

### Sofware repositories
[stm_slave_repo](https://github.com/inpgbburda/Stm32f401.git)  
[main_repo](https://github.com/TomBartDrone/drone_code.git)

### Hardware repositories

## Project architecture

``` mermaid
    graph TD
    
    A[Raspberry pi
    Real Time Linux/ C++] <--> B[Accelleration sensor]
    A --> C[Stm32F4 
    Bare metal /C]
    C --> D[Electric motors]
```