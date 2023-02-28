# NIOS2_Core_OriodMalo 

## Introduction

After learning about Embedded Systems FPGA and CPU design I wanted to build my basic Nios-II Core for later use on my DE10-Lite development board. <br>
This would help me to have a nice small, custom embedded framework for later, higher-level software projects that could be built on my DE-10 Lite. <br>
Furthermore, this project provided a nice step-by-step algorithm for creating a Processor system with all its necessary components. <br>

## Work Description 
Before starting the project I set up the default configuration from the System builder and generate it.<br>
You also need to download the "Factory Configuration - MAX10 DE10 Lite" from the altera system.<br>
The process for building a CPU system consists in adding and interconnecting:<br>

* Qsys starts with a clock called "clk_0". This is the basic clock in your system so the next thing to be added is a PLL.<br>
The PLL has to take in input a 50MHz clock (MAX10_CLK1_50) and give in output several clocks.<br>
Since I wanted it to create smth that handles a VGA which requires 25MHz, I created a PLL with 4 outputs:<br>
100MHz for the core, 50MHz for the SDRAM, 50MHz -90° phase for the Input/Output Peripherals and 25MHz for the VGA.
* Then I needed another clock for the ADC so I created a new clock source called "clk_1" and another pll for it which takes in input and gives in output a 10MHz clock. This is the "ADC_CLK_10".
* At this point I added the Nios 2 core, to which I even added hardware multiplication and division support.
* 32 KB OnChip RAM
* OnChip FLASH
* SDRAM
* Clock Crossing Bridge - to link together different clock domains, more specifically the 100MHz and 50MHz-90° one.
* Timer (1ms) 
* JTAG Master and UART
* Modular ADC with JTAG to Avalon Master bridge.
* System ID - necessary to identify the system. Also has to be called by a default name "sysid".
* Several PIO modules, out of which (for Eclipse default Debug Project reasons) the LEDS PIO has to be called "LED_PIO" and one of the 7-segment PIO modules has to be called "SEVEN_SEG_PIO".
* Base addresses and IRQ levels assigned automatically
* Compile, generate hdl.

## FAQ
* How to install? Create a "NIOS2_Core_OriodMalo" folder in your Quartus path and put there all the files from this Git. Unpack the ".rar" files which are the packed folders from my project. Compile and run

* If there are any issues? Contact me here.

* What happens after the Qsys compilation? The module has to be instantiated in the main Verilog file and then everything compiled together (in my PC takes roughly 10 min).

* How do you test the project? I create an Eclipse Workspace and use the default project template on board diagnostics to verify if the elements I wanted are really controllable.

## Screenshoots

![image](https://user-images.githubusercontent.com/123891760/221951920-f3516cde-ea0f-4e71-bba2-9d103cfbf2ed.png)
