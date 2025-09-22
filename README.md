# STM32 LCD16x2 Interface (Direct & Shift Register Versions)

## Description
This repository demonstrates two approaches to interface an **LCD16x2** display with an **STM32 microcontroller**.  
The goal is to compare a traditional direct GPIO connection with an optimized method using a **74HC595 shift register** and **SPI** to reduce pin usage.

---

## Version 1: Direct GPIO Connection
- The LCD16x2 is directly connected to the STM32 using **6 GPIO pins**.  
- All data and control lines are handled through standard `HAL_GPIO_WritePin` functions.  
- This method is simple and easy to understand but consumes multiple I/O pins, which can limit scalability in more complex designs.

---

## Version 2: Shift Register with SPI (74HC595)
- The LCD16x2 is driven through a **74HC595 shift register**, reducing the required pins to only **3 connections**:
  - **Clock**
  - **Latch**
  - **MOSI (Master Out Slave In)**  
- Data is sent via **`HAL_SPI_Transmit`**, and the latch pin is toggled with a dedicated `LATCH` function to update the LCD.  
- This approach frees up valuable GPIOs, making it more efficient for applications where pin availability is limited.

---

## Library
A modified version of the **LCD16x2 library** is included:
- In Version 1: standard GPIO functions (`HAL_GPIO_WritePin`) are used.  
- In Version 2: all GPIO writes are replaced with SPI communication (`HAL_SPI_Transmit`) plus latch control.  
- The library abstracts low-level implementation, so the user can work with simple LCD functions (e.g., writing text) without worrying about the communication details.

---

## Key Advantages of Version 2
- Significant reduction in the number of GPIO pins required.  
- Cleaner hardware design with fewer connections.  
- Demonstrates practical usage of **SPI peripheral** in STM32 for driving external components.


![LCD Setup](images/lcd_setup.png "LCD16x2 Wiring Diagram")
![74HC595](images/lcd_setup.png "LCD16x2 Wiring Diagram")
