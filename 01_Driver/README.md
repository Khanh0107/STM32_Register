# STM32F767 GPIO Register Configuration Guide

## Project Overview
This document provides a detailed register-level configuration guide for STM32F767 microcontroller GPIO setup:
- **LED Control**: GPIO B0 (Output Pin)  
- **Button Input**: GPIO B11 (Input Pin with External Interrupt)

## Quick Simplified Steps (No Bit/Address Detail)

### LED PB0 Initialization
1. Enable clock for GPIOB.
2. Set PB0 as output mode.
3. Configure output type = push‑pull.
4. Set speed = fast.
5. No pull-up / pull-down.
6. Initialize output low (LED OFF).

### Button PB11 Interrupt Initialization
1. Enable clock for GPIOB.
2. Enable clock for SYSCFG (needed for EXTI mapping).
3. Set PB11 as input (for interrupt line).
4. Set speed = fast.
5. Enable pull-up resistor.
6. Configure EXTI line for falling edge trigger.
7. Map PB11 to EXTI11 in SYSCFG.
8. Unmask EXTI11 interrupt line.
9. Set NVIC priority for EXTI15_10.
10. Enable NVIC interrupt for EXTI15_10.
11. In ISR: clear pending flag and toggle LED.

### Runtime Behavior
Press button (PB11 pulled high, falls to low) -> EXTI triggers -> ISR runs -> LED PB0 toggles.

## Hardware Configuration Summary

### LED Configuration (GPIO B0)
- **Port**: GPIOB (Base Address: 0x40020400)
- **Pin**: Pin 0
- **Mode**: General Purpose Output (01)
- **Type**: Push-Pull (0)
- **Speed**: Fast (10)
- **Pull-up/Pull-down**: None (00)
- **Initial State**: Low (LED OFF)

### Button Configuration (GPIO B11)
- **Port**: GPIOB (Base Address: 0x40020400)
- **Pin**: Pin 11
- **Mode**: External Interrupt Falling Trigger (GPIO_MODE_IT_FT = 4)
- **Speed**: Fast (10)
- **Pull-up/Pull-down**: Pull-up enabled (01)
- **Interrupt Line**: EXTI11
- **NVIC IRQ**: EXTI15_10 (IRQ Number 40)
- **Priority**: 3

