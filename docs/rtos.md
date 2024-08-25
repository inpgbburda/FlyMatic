## Configured Tasks

### 1. SPI Communication Task
- **Function:** Reads SPI messages containing requested PWM values from the Raspberry Pi.
- **Priority:** High
- **Execution Frequency:** 100 Hz

### 2. PWM Output Task
- **Function:** Writes PWM signals to the motor driver hardware based on the received SPI messages.
- **Priority:** Medium
- **Execution Frequency:** 50 Hz

### Task Synchronization
The tasks are synchronized using FreeRTOS semaphores to ensure that PWM adjustments are made in real-time without data conflicts.

## Related Sections
- [Motor Control](motor_control.md): For understanding how the PWM values are generated and used.