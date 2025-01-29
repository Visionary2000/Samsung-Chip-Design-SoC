# Samsung-Chip-Design-SoC
## Day 1: Section 1: How to Talk to Computers
### Introduction to QFN-48 Package, Chip, Pads, Core, Die, and IPs
The processor in a QFN-48 is not the processor itself, but is called the package. 
Within the package lies the chip which does the processing, and is connected to the package using wire bonds (connected to the boundaries of the chip), and helps in transferring all the signals coming from the outside world to the interiors of the chip.
![Image Alt](https://github.com/Visionary2000/Samsung-Chip-Design-SoC/blob/main/Chip%20and%20Wire%20Bonds.JPG?raw=true)

Within the chip lie many important components, one of which are called pads. Pads help in sending the signal inside and outside the chip.
The core of a chip is the place where all the digital logic sits, such as AND gates, OR gates, MUX, etc. 
Die is the size of the chip.
![Image Alt](https://github.com/Visionary2000/Samsung-Chip-Design-SoC/blob/main/Pads,%20Core,%20Die.JPG?raw=true)

In an example of a sample Soc (RISC V SoC), the core consists of an SoC, SRAM, ADC, DAC, PLL, SPI, etc. The SRAM, DAC, ADC, PLL are called **Foundry IPs**. Foundry is a very critical term in Chip Design. The performance of all devices that we use is dependant on the foundry. A Foundry is a big factory, which has machines and tools and aids in manufacture of chips. Engineers continuously communicate with the foundry to make chips. IP (Intellectual Property), means such components (SRAM, ADC, DAC, PLL, SPI, etc.) needs a certain level of intelligence to be built.
The digital blocks of a chip are called **Macros**. 
There is a clear distinction between macros and IPs. Macros are digital blocks, but IPs need some intelligence to build it.
To build a chip, one needs to interact with the foundry (files which the foundry gives us). We communicate with the foundry with those files.
![Image Alt](https://github.com/Visionary2000/Samsung-Chip-Design-SoC/blob/main/Macros%20and%20Foundry%20IPs.JPG?raw=true)
