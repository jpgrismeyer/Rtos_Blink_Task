# RTOS_Blink_Task (STM32 + FreeRTOS)

Minimal FreeRTOS demo on STM32: two tasks — LED blink and UART "Hello" — to show scheduling and basic interleaving.

## Target
- Board: B-L475E-IOT01A2 Discovery Kit
- MCU: STM32L475VG
- IDE: STM32CubeIDE
- Middleware: FreeRTOS (CMSIS-RTOS v2)

## Getting started
1. Create a new **STM32 Project** in STM32CubeIDE.
   - Board: `B-L475E-IOT01A2`.
   - SYS → Debug: **Serial Wire**.
   - GPIO → configure **LED2** (PB14) as output.
   - (Optional) USART → configure one UART at 115200 baud for printf/debug.
   - Middleware → enable **FreeRTOS** (CMSIS-RTOS v2).
2. Generate code.
3. Implement two tasks in `freertos.c`:
   - **TaskBlink:** toggles LED every 500 ms.
   - **TaskUART:** sends “Hello from FreeRTOS” every 1 s over UART.
4. Build & flash the project.

## Example code
```c
void StartBlink(void *argument) {
  for(;;) {
    HAL_GPIO_TogglePin(GPIOB, GPIO_PIN_14); // LED2 on IoT board
    osDelay(500);
  }
}

void StartUart(void *argument) {
  const char *msg = "Hello from FreeRTOS\r\n";
  for(;;) {
    HAL_UART_Transmit(&huart1, (uint8_t*)msg, strlen(msg), 100);
    osDelay(1000);
  }
}

Checklist

 Project created in CubeIDE with FreeRTOS enabled

 LED configured as GPIO output

 (Optional) UART configured at 115200 baud

 LED blinks every 500 ms

 UART prints message every 1 s

 Commit & push project to GitHub



---

