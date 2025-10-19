# Overview

The MainUnit is a master for all system logic and control.  
It's deployed on `RPI4B` board with OS:  

System name :simple-linux::  
- `Linux raspberrypi 6.6.31-rt30-v8+ #1 SMP PREEMPT_RT`
Hardware name:  
- `aarch64`

The OS is patched with `PREEMPT_RT` - more about here [linux_foundation_link](https://wiki.linuxfoundation.org/realtime/start#documentation).  
To avoid building kernel from scratch, pre-prepared version was built. [GitHub - remusmp/rpi-rt-kernel](https://github.com/remusmp/rpi-rt-kernel)

The most important feature of the `PREEMPT_RT` patch, is that it that **the scheduler can preemt almost every kernel operation**.  

As a consequence, the user (time critical) threads cam now treated with the higher priority.  
In most cases, it allows to achieve `100us` time resolution. More about it: [linux_doc_link](https://docs.kernel.org/next/core-api/real-time/theory.html)

### Dynamic Architecture
```puml
@startuml
title Reading the MPU sensor

participant "Thr_Mpu6050_Read"  as Thr_Mpu6050_Read
participant "Thr_Flight_Ctrl"   as Thr_Flight_Ctrl
participant "Balancer"          as Balancer
entity       "mpu6050"          as mpu6050
entity       "Mpu6050::sensor_" as Mpu6050_sensor_
participant "i2c"               as i2c
participant "Spi_Hw"            as Spi_Hw

note over Mpu6050_sensor_: member-object of 'mpu6050'

Thr_Mpu6050_Read ->> Balancer : ReadAccSensor()
activate Thr_Mpu6050_Read
activate Balancer

Balancer ->> mpu6050: mpu6050.ReadSensorData()
activate mpu6050
mpu6050 ->> Mpu6050_sensor_:         sensor_.ReadSensorData()
activate Mpu6050_sensor_
Mpu6050_sensor_ ->> Mpu6050_sensor_: ReadAcceleration()
activate Mpu6050_sensor_
Mpu6050_sensor_ ->> i2c:             ReadBlockOfBytes()
activate i2c

i2c -->> Mpu6050_sensor_
deactivate Mpu6050_sensor_
deactivate i2c
Mpu6050_sensor_ -->> mpu6050
deactivate Mpu6050_sensor_

mpu6050 -->> Balancer
Balancer -->> Thr_Mpu6050_Read:

@enduml
```