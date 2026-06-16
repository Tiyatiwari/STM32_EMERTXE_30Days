# Day 5 - TIM1 Interrupt + NVIC

**MCU:** STM32F103C8T6 Blue Pill  
**Task:** Blink LED every 1 second using TIM1 interrupt and NVIC

**Clock Config:**
- System Clock: 72MHz
- TIM1 Prescaler: 7199
- TIM1 Period: 9999
- Formula: 72MHz / 7200 / 10000 = 1Hz

**Key Learning:**
- First project using hardware interrupts instead of HAL_Delay
- NVIC TIM1 Update Interrupt must be enabled in CubeMX
- `HAL_TIM_Base_Start_IT(&htim1)` starts timer with interrupt
- Callback function: `HAL_TIM_PeriodElapsedCallback`

**Pins Used:**
- `PC13` = Onboard LED for real STM32 Blue Pill
  

**How it works:**
1. TIM1 counts up every 1/10,000 second
2. After 10,000 counts = 1 second, TIM1 triggers interrupt
3. NVIC jumps to `HAL_TIM_PeriodElapsedCallback`
4. Callback toggles the LED

**Tested on:** PICSimLab STM32F103 Blue Pill

