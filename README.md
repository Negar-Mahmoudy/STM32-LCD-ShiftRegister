# STM32 LCD16x2 Interface (Direct & Shift Register Versions)

## Description
This repository demonstrates two approaches to interface an **LCD16x2** display with an **STM32 microcontroller**.  
The goal is to compare a traditional direct GPIO connection with an optimized method using a **74HC595 shift register** and **SPI** to reduce pin usage.

---

## Version 1: Direct GPIO Connection
The LCD16x2 is directly connected to the STM32 using **6 GPIO pins**, and all data and control lines are handled by standard `HAL_GPIO_WritePin` functions. This method is simple and easy to understand but consumes many I/O pins.

---

## Version 2: Shift Register with SPI (74HC595)
The LCD16x2 is driven through a **74HC595 shift register**, which reduces the required pins to only 3(Clock, Latch, MOSI). Data is sent with SPI, and the latch pin is toggled with a LATCH function to update the LCD. This method uses less GPIO pins.

---

## Library
A modified version of the **LCD16x2 library** in Version2 is included and all GPIO writes are replaced with SPI communication (`HAL_SPI_Transmit`) plus latch control.  
The library abstracts the low-level implementation, allowing to write or read text very easily on a LCD.

---

## Advantages of Version 2
Much less amount of GPIOs and less connections are needed. additionally it practically uses SPI peripheral for driving external devices.


![LCD Setup](https://github.com/Negar-Mahmoudy/STM32-LCD-ShiftRegister/blob/main/images/1.PNG?raw=true)
![74HC595](https://github.com/Negar-Mahmoudy/STM32-LCD-ShiftRegister/blob/main/images/2.png?raw=true)
