# SMART TRAFFIC LIGHT CONTROLLER 
## OVERVIEW
The main objective of this traffic light controller is to provide sophisticated control and coordination to confirm that traffic moves as smoothly and safely as possible. To ensure the safety of pedestrians, a manual switch (IR sensor) is used to halt the busy moving traffic in case of any emergency. This project makes use of LED lights and IR sensor for indication purpose and a VSD Squadron Mini development board is used for auto changing of signal at specified range of time interval. 

## COMPONENTS REQUIRED
   ```
   1. VSD Squadron Mini Board

   2. LEDs (3): Depicting red yellow and green light

   3. IR sensor

   4. Jumper wires

   5. Breadboard

   6. Platform IO

   7. VS Code for software development
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

#define TRAFFIC_GPIO_PORT GPIOD
#define RED_LED GPIO_Pin_6
#define YELLOW_LED GPIO_Pin_5
#define GREEN_LED GPIO_Pin_4
#define SWITCH_PIN GPIO_Pin_2   //IR sensor

#define TRAFFIC_CLOCK_ENABLE RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOD, ENABLE)

void NMI_Handler(void) __attribute__((interrupt("WCH-Interrupt-fast")));
void HardFault_Handler(void) __attribute__((interrupt("WCH-Interrupt-fast")));
void Delay_Init(void);
void Delay_Ms(uint32_t n);

void handle_switch_press(void);

int main(void)
{
    NVIC_PriorityGroupConfig(NVIC_PriorityGroup_2);
    SystemCoreClockUpdate();
    Delay_Init();

    GPIO_InitTypeDef GPIO_InitStructure = {0};

    TRAFFIC_CLOCK_ENABLE;

    // Initialize traffic light LEDs
    GPIO_InitStructure.GPIO_Pin = RED_LED | YELLOW_LED | GREEN_LED;
    GPIO_InitStructure.GPIO_Mode = GPIO_Mode_Out_PP;
    GPIO_InitStructure.GPIO_Speed = GPIO_Speed_50MHz;
    GPIO_Init(TRAFFIC_GPIO_PORT, &GPIO_InitStructure);

    // Initialize switch pin
    GPIO_InitStructure.GPIO_Pin = SWITCH_PIN;
    GPIO_InitStructure.GPIO_Mode = GPIO_Mode_IPU; // Input with pull-up
    GPIO_Init(TRAFFIC_GPIO_PORT, &GPIO_InitStructure);

    while (1)
    {
        if (GPIO_ReadInputDataBit(TRAFFIC_GPIO_PORT, SWITCH_PIN) == 0) // Switch pressed
        {
            handle_switch_press();
        }
        else
        {
            // Green light on
            GPIO_WriteBit(TRAFFIC_GPIO_PORT, GREEN_LED, Bit_SET);
            for (int i = 0; i < 5000; i++)
            {
                Delay_Ms(1);
                if (GPIO_ReadInputDataBit(TRAFFIC_GPIO_PORT, SWITCH_PIN) == 0) 
                {
                    handle_switch_press();
                    break;
                }
            }
            GPIO_WriteBit(TRAFFIC_GPIO_PORT, GREEN_LED, Bit_RESET);

            // Yellow light on
            GPIO_WriteBit(TRAFFIC_GPIO_PORT, YELLOW_LED, Bit_SET);
            for (int i = 0; i < 2000; i++)
            {
                Delay_Ms(1);
                if (GPIO_ReadInputDataBit(TRAFFIC_GPIO_PORT, SWITCH_PIN) == 0) 
                {
                    handle_switch_press();
                    break;
                }
            }
            GPIO_WriteBit(TRAFFIC_GPIO_PORT, YELLOW_LED, Bit_RESET);

            // Red light on
            GPIO_WriteBit(TRAFFIC_GPIO_PORT, RED_LED, Bit_SET);
            for (int i = 0; i < 5000; i++)
            {
                Delay_Ms(1);
                if (GPIO_ReadInputDataBit(TRAFFIC_GPIO_PORT, SWITCH_PIN) == 0) 
                {
                    handle_switch_press();
                    break;
                }
            }
            GPIO_WriteBit(TRAFFIC_GPIO_PORT, RED_LED, Bit_RESET);
        }
    }
}

void handle_switch_press(void)
{
    // Turn off all LEDs
    GPIO_WriteBit(TRAFFIC_GPIO_PORT, RED_LED, Bit_RESET);
    GPIO_WriteBit(TRAFFIC_GPIO_PORT, YELLOW_LED, Bit_RESET);
    GPIO_WriteBit(TRAFFIC_GPIO_PORT, GREEN_LED, Bit_RESET);

    // Turn on yellow LED for 1 second
    GPIO_WriteBit(TRAFFIC_GPIO_PORT, YELLOW_LED, Bit_SET);
    Delay_Ms(1000);
    GPIO_WriteBit(TRAFFIC_GPIO_PORT, YELLOW_LED, Bit_RESET);

    // Turn on red LED for 3 seconds
    GPIO_WriteBit(TRAFFIC_GPIO_PORT, RED_LED, Bit_SET);
    Delay_Ms(3000);
    GPIO_WriteBit(TRAFFIC_GPIO_PORT, RED_LED, Bit_RESET);
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

https://github.com/ridhikapila27/vsdsquadron-mini-internship/assets/72308639/16f9a9ab-b6fb-42f5-8846-87536bf02578






