# Lab01 – Hardware/Software Prototyping

## Goals of this lab:

1. Familiarize ourselves with the **NUCLEO-L031K6**
2. Understand how to develope code with the **STM32CubeIDE**
3. Write a simple **BlinkTest** program for the NUCLEO
4. Test multiple useful libraries by writing the **ClickRNG** program
5. Write the **ProjectCode** for the STM32L031K6

### 1. NUCLEO-L031K6

STMicroelectronics produces a large catalog of high performance microcontrollers for a wide range of applications. We will be utilizing a chip from the [STML0](https://www.st.com/en/microcontrollers-microprocessors/stm32l0-series.html) line because they offer extreme power saving capabilities. This is nesecary because the dice will be battery powered and very hard to open up after assembly. Prototyping directly with an MCU can be difficult. Thankfully, ST offers the [NUCLEO-L031K6](https://www.st.com/en/evaluation-tools/nucleo-l031k6.html) which utilizes the STM32L031K6 MCU. This board allows for quick and easy developement.

Here are some resources to learn more about the STM32L031K6:

- [Low-Power Modes on the STM32L0 Series](https://www.digikey.com/eewiki/display/microcontroller/Low-Power+Modes+on+the+STM32L0+Series)
- [STM32L031x6 Reference Manual](https://www.st.com/resource/en/reference_manual/dm00108282-ultralowpower-stm32l0x1-advanced-armbased-32bit-mcus-stmicroelectronics.pdf)
- [STM32L031x6 Datasheet](https://www.st.com/resource/en/datasheet/stm32l031k6.pdf)

### 2. STM32CubeIDE

STM32CubeIDE is an all in one integrated developing environment used to easily setup, develop, and debug code for STM32 MCUs and developement boards...

### 3. BlinkTest

Before we write involved programs with multiple libraries, we should test the basic funcionality of our board and ensure that the STM32CubeIDE debugger works. To do that, we will write a simple program that flashes an LED (LD3) on the NUCLEO. Your task is to use this [Description of STM32L0 HAL and Low Layer drivers](https://www.st.com/resource/en/user_manual/dm00113898-description-of-stm32l0-hal-and-low-layer-drivers-stmicroelectronics.pdf) to find useful functions that achieve this goal. LD3 has already been correctly configured and all you need to do is add some lines of code to the while loop in main.c. 

<details>
  <summary>Hint: Toggle the LED</summary> 
  
  To change the LD3 pin from low to high (and vice versa), you should implement this function:
  
  ```c
  void HAL_GPIO_TogglePin(GPIO_TypeDef * GPIOx, uint16_t GPIO_Pin)
  ```
</details>
  
### 4. ClickRNG

For this test program, we will now be exploring more functionality that will be used in our final project code... RNG, Shift register

To recieve data from the NUCLEO, we must connect to it through UART (universal asynchronus reciever/transmitter). By default, STM32CubeIDE initialized the MCU pins in such a way that no extra connections are necessary and we can communicate through USB. The default baud rate is 115200 bits/s. Confirm that this is true for your setup. If using Windows, you should install [PuTTY](https://www.putty.org/) and connect through the graphical interface. If on Mac or Linux, you can use the Screen command to connect to the board. To view available devices, type the following into your command line:

```c
ls /dev/cu.*
```

Your output should look something like this:

```
/dev/cu.Bluetooth-Incoming-Port	/dev/cu.WH-H910Nhear-SerialHPC
/dev/cu.WH-H910Nhear-Airoha_APP	/dev/cu.WH-H910Nhear-SerialMC
/dev/cu.WH-H910Nhear-GSOUND_BT_	/dev/cu.usbmodem143103
/dev/cu.WH-H910Nhear-IAPSERVER
```

Identify the correct port, and connect to it using a command similar to:

```
screen /dev/cu.usbmodem143103 115200
```

You should now be connected to your NUCLEO!

<details>
  <summary>Hint: Communicate with UART</summary> 
  
  To transmit data over UART, read about and implement the following function:
  
  ```c
  HAL_StatusTypeDef HAL_UART_Transmit(UART_HandleTypeDef * huart, uint8_t * pData, uint16_t Size, uint32_t Timeout)
  ```
</details>

### 5. ProjectCode
