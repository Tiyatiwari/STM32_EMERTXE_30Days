# Day 4: HC-SR04 Ultrasonic Distance Measurement

## Aim
Interface HC-SR04 ultrasonic sensor with STM32F103C6 and display distance on UART.

## Pin Connections
| HC-SR04 | STM32F103C6 |
| --- | --- |
| VCC | 5V |
| TRIG | PA0 |
| ECHO | PA1 |
| GND | GND |
| UART TX | PA9 |

## Working Logic
1. Send 10us HIGH pulse on TRIG pin PA0
2. Measure ECHO pin PA1 high time using TIM2 in 1us resolution
3. Calculate: Distance(cm) = (Echo_Time_us * 0.0343) / 2
4. Send distance via UART1 at 115200 baud every 500ms

## Output Screenshot
![Ultrasonic Output](Day4_Ultrasonic_Output.png)

## Tested Range
25 cm to 159 cm - verified using PICSimLab slider
