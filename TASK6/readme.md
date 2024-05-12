# TRAFFIC LIGHT CONTROLLER
## OVERVIEW
This project makes use of LED lights for indication purpose and a VSD Squadron Mini development board is used for auto changing of signal at specified range of time interval. LED lights gets automatically turns on and off by making corresponding port pin of the board “HIGH”. The main objective of this traffic light controller is to provide sophisticated control and coordination to confirm that traffic moves as smoothly and safely as possible.

## COMPONENTS REQUIRED
   ```
   1. VSD Squadron Mini Board

   2. LEDs (3): Depicting red yellow and green light

   3. Jumper wires

   4. Breadboard

   5. Platform IO

   6. VS Code for software development
   ```

## HARDWARE CONNECTIONS
 LED Connections: 
   * Positive end (Anode) of LED 1 connected to GPIO Pin 6 of VSDSquadron Mini.
   * Positive end (Anode) of LED 2 connected to GPIO Pin 5 of VSDSquadron Mini.
   * Positive end (Anode) of LED 3 connected to GPIO Pin 4 of VSDSquadron Mini.
   * Negative end (Cathode) connected to GND pin of VSDSquadron Mini.
   
      
## HOW TO PROGRAM
```
#include <ch32v00x.h>
#include <debug.h>

#define BLINKY_GPIO_PORT GPIOD
#define Led1 GPIO_Pin_6
#define Led2 GPIO_Pin_5
#define Led3 GPIO_Pin_4
#define BLINKY_CLOCK_ENABLE RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOD, ENABLE)

void NMI_Handler(void) _attribute_((interrupt("WCH-Interrupt-fast")));
void HardFault_Handler(void) _attribute_((interrupt("WCH-Interrupt-fast")));
void Delay_Init(void);
void Delay_Ms(uint32_t n);

int main(void)
{
    NVIC_PriorityGroupConfig(NVIC_PriorityGroup_2);
    SystemCoreClockUpdate();
    Delay_Init();

    GPIO_InitTypeDef GPIO_InitStructure = {0};

    BLINKY_CLOCK_ENABLE;
    GPIO_InitStructure.GPIO_Pin = Led1 | Led2 | Led3;
    GPIO_InitStructure.GPIO_Mode = GPIO_Mode_Out_PP;
    GPIO_InitStructure.GPIO_Speed = GPIO_Speed_50MHz;
    GPIO_Init(BLINKY_GPIO_PORT, &GPIO_InitStructure);

    while (1)
    {
        // LED1 ON
        GPIO_WriteBit(BLINKY_GPIO_PORT, Led1, Bit_SET);
        Delay_Ms(2500);
        // LED1 OFF
        GPIO_WriteBit(BLINKY_GPIO_PORT, Led1, Bit_RESET);

        // LED2 ON
        GPIO_WriteBit(BLINKY_GPIO_PORT, Led2, Bit_SET);
        Delay_Ms(1000);
        // LED2 OFF
        GPIO_WriteBit(BLINKY_GPIO_PORT, Led2, Bit_RESET);

        // LED3 ON
        GPIO_WriteBit(BLINKY_GPIO_PORT, Led3, Bit_SET);
        Delay_Ms(2500);
        // LED3 OFF
        GPIO_WriteBit(BLINKY_GPIO_PORT, Led3, Bit_RESET);
		
    }
}

void NMI_Handler(void) {}
void HardFault_Handler(void)
{
    while (1)
    {
    }
}
```
  
## APPLICATION VIDEO

https://github.com/ridhikapila27/vsdsquadron-mini-internship/assets/72308639/34f7a3e4-2e81-4757-8e5e-17c0278fb237




