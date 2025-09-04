# RTOS_Blink_Task (STM32 + FreeRTOS)

Minimal FreeRTOS demo on STM32: showing how to run multiple tasks under a scheduler.  
- Step 1: Blink task.  
- Step 2: UART task.  

## Target
- Board: B-L475E-IOT01A2 Discovery Kit
- MCU: STM32L475VG
- IDE: STM32CubeIDE
- Middleware: FreeRTOS (CMSIS-RTOS v2)

## Progress
| Task        | Status |
|-------------|--------|
| Project setup (CubeIDE + FreeRTOS) | ✅ Done |
| Configure LED2 (PB14) as output   | ✅ Done |
| TaskBlink: toggle LED every 500 ms | ✅ Done |
| TaskUART: print message every 1 s  | ✅ Done |
| Run both tasks concurrently        | ✅ Done |

**Overall progress:**  
🟩🟩🟩🟩🟩 (5/5 completed)

---

## Getting started
1. Create a new **STM32 Project** in STM32CubeIDE.
   - Board: `B-L475E-IOT01A2`.
   - SYS → Debug: **Serial Wire**.
   - GPIO → configure **LED2** (PB14) as output.
   - Middleware → enable **FreeRTOS** (CMSIS-RTOS v2).
2. Generate code.
3. Implement the application tasks in `main.c`:
   - **TaskBlink:** toggles LED every 500 ms (✅ DONE).
   - **TaskUART:** sends “Hello from FreeRTOS” every 1 s over UART (✅ DONE).
4. Build & flash the project.

## Example code (TaskBlink)


void StartBlink(void *argument) {
  for(;;) {
    HAL_GPIO_TogglePin(LED2_GPIO_Port, LED2_Pin); // LED2 on IoT board
    osDelay(500);
  }
}


##Example code (TaskUART)
void StartUartTask(void *argument) {
  const char *msg = "Hello from FreeRTOS\r\n";
  for(;;) {
    HAL_UART_Transmit(&huart1, (uint8_t*)msg, strlen(msg), 100);
    osDelay(1000);
  }
}


On the B-L475E-IOT01A2 Discovery Kit the ST-LINK Virtual COM Port is usually mapped to USART1 (115200 baud, 8N1).
If no output appears, try huart3 instead.

Demo

Here are the tasks running concurrently on the STM32L475 board:

Blink task (LED2 toggling every 500 ms)

UART task (printing every 1 s via VCP)

![RTOS demo](Docs/media/rtos1.gif)
