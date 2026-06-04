# STM32_EMERTXE_30Days

30 Days of STM32F103C8T6 Projects - Building production-ready embedded skills.

## Day 1: LED Blink @1Hz using HAL

**Board**: STM32F103C8T6 "Blue Pill"  
**IDE**: STM32CubeIDE 1.19.0  
**HAL Version**: STM32CubeF1 v1.8.5  
**Verified**: PICSimLab 0.9.2

### Pin Configuration
| Function | Pin | Mode |
| --- | --- | --- |
| User LED | PC13 | GPIO_Output |

### Timing Calculation
- **System Clock**: 8MHz HSI
- **Requirement**: 1Hz toggle = 500ms ON, 500ms OFF
- **Implementation**: `HAL_Delay(500)` in while loop

### Key Code - main.c
```c
while (1)
{
  HAL_GPIO_TogglePin(GPIOC, GPIO_PIN_13);
  HAL_Delay(500); // 500ms
}
