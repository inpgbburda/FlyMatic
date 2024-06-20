# Angle Sensing with MPU-6050 for Spirit Level Application

## Introduction

This documentation provides an overview of using the MPU-6050 sensor to measure angles and calculate a spirit level using the `arcsin` function. The MPU-6050 sensor integrates a 3-axis gyroscope and a 3-axis accelerometer, which can be used to determine the orientation of an object.

## Key Concepts

### MPU-6050 Accelerometer Data

The MPU-6050 provides acceleration data for three axes (X, Y, Z). These values represent the acceleration due to gravity along each axis and can be used to calculate the tilt angle of the sensor.

### Angle Calculation

To calculate the tilt angle of the sensor, we use the acceleration data. The relevant formula involves the `arcsin` function, which is used to derive the angle from the ratio of the accelerometer readings to the gravitational constant.

### Formula for Angle Calculation

1. **Reading Accelerometer Data:**
   - `Ax`: Acceleration along the X-axis
   - `Ay`: Acceleration along the Y-axis
   - `Az`: Acceleration along the Z-axis
