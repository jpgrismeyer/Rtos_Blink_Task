# RTOS_Blink_Task (STM32 + FreeRTOS)

Minimal FreeRTOS demo on STM32: showing how to run tasks under a scheduler.  
Step 1: Blink task.  
Step 2 (next): UART task.

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
| TaskUART: print message every 1 s  | ⏳ Pending |
| Run both tasks concurrently        | ⏳ Pending |

**Overall progress:**  
🟩🟩🟩⬜⬜ (3/5 completed)

---

## Getting started
1. Create a new **STM32 Project** in STM32CubeIDE.
   - Board: `B-L475E-IOT01A2`.
   - SYS → Debug: **Serial Wire**.
   - GPIO → configure **LED2** (PB14) as output.
   - Middleware → enable **FreeRTOS** (CMSIS-RTOS v2).
2. Generate code.
3. Implement the application tasks in `main.c`:
   - **TaskBlink:** toggles LED every 500 ms (DONE ✅).
   - **TaskUART:** sends “Hello from FreeRTOS” every 1 s over UART (coming soon).
4. Build & flash the project.

## Example code (TaskBlink)

```c
void StartBlink(void *argument) {
  for(;;) {
    HAL_GPIO_TogglePin(LED2_GPIO_Port, LED2_Pin); // LED2 on IoT board
    osDelay(500);
  }
}


## Demo

Here is the Blink task running on the STM32L475 board:

![Blink demo](Docs/media/blink.mp4)

