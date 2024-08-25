# Angle Sensing with MPU-6050 for Spirit Level Application

## Introduction
This document describes the use of the MPU-6050 sensor for angle measurement, particularly in the context of a spirit level application. The MPU-6050 integrates a 3-axis accelerometer and a 3-axis gyroscope, enabling it to accurately measure the orientation of an object.

## Key Concepts

### MPU-6050 Accelerometer Data
The MPU-6050 provides acceleration data across three axes (X, Y, Z). These values represent the gravitational force acting on each axis, which can be used to determine the tilt angle.

### Angle Calculation
To calculate the tilt angle, we use the acceleration data provided by the MPU-6050. The angle is derived using the `arcsin` function, which computes the angle from the ratio of the accelerometer readings to the gravitational constant.

### Formula for Angle Calculation
The angle θ can be calculated as follows:
$$
\[
\theta = \arcsin\left(\frac{A_x}{\sqrt{A_x^2 + A_y^2 + A_z^2}}\right)
\]
$$
Where:
- `Ax`: Acceleration along the X-axis
- `Ay`: Acceleration along the Y-axis
- `Az`: Acceleration along the Z-axis

### Practical Application
This angle calculation is crucial for maintaining the balance of the drone and can also be used in applications like a digital spirit level.

## Related Sections
- [Motor Control](motor_control.md): To understand how angle data influences motor adjustments.
