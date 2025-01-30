# Samsung-Chip-Design-SoC
## Day 1: Section 1: How to Talk to Computers
### Introduction to QFN-48 Package, Chip, Pads, Core, Die, and IPs
The processor in a QFN-48 is not the processor itself, but is called the package. 
Within the package lies the chip which does the processing, and is connected to the package using wire bonds (connected to the boundaries of the chip), and helps in transferring all the signals coming from the outside world to the interiors of the chip.

![Image](https://github.com/user-attachments/assets/3e07d90e-b8fd-45fa-87ef-c15a2b1c44b6)

Within the chip lie many important components, one of which are called pads. Pads help in sending the signal inside and outside the chip.
The core of a chip is the place where all the digital logic sits, such as AND gates, OR gates, MUX, etc. 
Die is the size of the chip.

![Image](https://github.com/user-attachments/assets/00c56f93-4e1f-4843-8c8d-e3a60c8098b9)

In an example of a sample Soc (RISC V SoC), the core consists of an SoC, SRAM, ADC, DAC, PLL, SPI, etc. The SRAM, DAC, ADC, PLL are called **Foundry IPs**. Foundry is a very critical term in Chip Design. The performance of all devices that we use is dependant on the foundry. A Foundry is a big factory, which has machines and tools and aids in manufacture of chips. Engineers continuously communicate with the foundry to make chips. IP (Intellectual Property), means such components (SRAM, ADC, DAC, PLL, SPI, etc.) needs a certain level of intelligence to be built.
The digital blocks of a chip are called **Macros**. 
There is a clear distinction between macros and IPs. Macros are digital blocks, but IPs need some intelligence to build it.
To build a chip, one needs to interact with the foundry (files which the foundry gives us). We communicate with the foundry with those files.

![Image](https://github.com/user-attachments/assets/67e0624b-970f-46aa-97ab-2a8550b26e03)


### Introduction to RISC-V
RISC-V Instruction Set Architecture (ISA) is a language of the computer, used to talk with the computers. 
Layout is the interior of a chip. If we want to run a particular C program on a particular layout, we need to pass that information to the hardware in certain terms. To do so, the C program is first complied to its assembly program language, which is then converted to the machine language (binary language) program. The bits in binary language, then gets executed in the layout, and you get the required output. 

This conversion cannot happen directly. It needs a certain interface, which is the hardware description language (HDL). RISC-V Architecture can be thought of as specifications, and these specifications gets implemented by the RTL. There is a standard RTL2GDS flow between the RTL and the layout.

![Image](https://github.com/user-attachments/assets/668a648d-f32a-415b-a534-96b387847430)

### From Software Applications to Hardware
The applications like Firefox, Google Chrome, Word, etc., that we use in our computers, runs on a chip present in the computer. 

The applications that we use goes into the system software, and the system software in turn converts the application program into hardware language. The main components of system software are Operating System, Compiler and Assembler. 

The **OS** handles IO operations, allocates memory, and takes care of low level system functions. The OS converts the application program to the assembly language and then to the binary language which is understood by the hardware, apart from its regular functions. The output of the OS are small functions in C, C++, Java, etc., which acts as input to the compiler.

The **Compiler** converts these inputs into instructions, and the syntax of the instructions depends on the type of hardware. The important function of compiler is to convert the input it receives in the software programming language to instructions (in the form of a .exe file). 

The **Assembler** converts these inputs (instructions) to the respective binary language (machine language program). The hardware reads these binary codes, and performs the respective function. 

![Image](https://github.com/user-attachments/assets/cd318d7d-efae-4261-ac66-a5b332d76307)

The instructions (output) of compiler actually acts as an abstract interface between the C language and the hardware, and this abstract interface is called as Instruction Set Architecture (ISA/acrchitecture of the computer). There is another interface between the instructions and the hardware, which is the HDL, as the hardware only understands 0s and 1s. The output of the assembler (binary code) gets implemented by am RTL, which then gets synthesized into the netlist (the instructions are written in the form of AND, OR, NOT gates), and is then physically implemented into the hardware.

![Image](https://github.com/user-attachments/assets/818a8404-f27c-422b-888c-d9acf73eb9be)


## Day 1: Section 2: SoC Design and OpenLANE
### Introduction to All Components of Open-Source Digital ASIC Design
ASIC - Application Specific Integrated Circuits.

Designing Digital ASIC require several elements, which needs to be present. These are:

**RTL IPs**

**Electronic Design Application (EDA) Tools**

**Process Design Kit (PDK) Data:** PDK is the interface between the FAB and the designers. The PDK contains very sensitive information. It has information on the successful implementation of ASIC.

A flow is a piece of software which glues different tools together.

### Simplified RTL2GDS Flow
The major steps involved in RTL to GDS conversion are:

1. **Synthesis:** Converts RTL to a circuit out of components from the standard cell library (SCL). The standard cells have a regular layout. Each has different views/models (electrical, HDL, SPICE, et.c)
2. **Floor Planning/Power Planning:** In Chip Floor-Planning, the chip die is partitioned between different system building blocks and place the I/O pads. In Macro Floor-Planning, the dimensions, pin locations, and rows are defined, which will be used in the Placement and Grounding steps. In Power-Planning, the power network is constructed. Typically, a chip is powered by VDD and Ground pins. The power pins are connected to the components through several vertical and horizontal metal straps, and these parallel structures help to reduce the resistance.

![Image](https://github.com/user-attachments/assets/13b9af66-db7f-4d3f-b438-8bea0993cd7a)

3. **Placement:** During placement, the cells are placed on the floorplan rows, aligned with the sites. Placement is done in 2 ways - global and detailed. In global placement, it tries to find optimal placement of the cells. Such positions are not necessarily legal, thus cells may overlap. In detailed placement, positions obtained from global placements are slightly altered, to become legal.
4. **Clock Tree Synthesis:** Before routing the signals, we need to route the clock, by creating a clock distribution network, and deliver the clock to all clock cells (like Flip-Flops). The clocking network looks like a tree. The clock tree is in size to deliver the clock to all things in a good shape with minimum skew and minimum latency. Clock skew means the arrival of the clock at different components at different times.
5. **Routing:** After routing the clock, comes signal routing. This is implementation of the interconnect using the available metal layers. The router uses the available metal layers as defined by the PDK.
6. **Sign Off:** Once routing is over, the final layout can be constructed, which undergoes verifications. This includes Design Rules Checking (DRC), where we check if the final layout follows all design rules, and the Layout vs Schematic (LVS), that makes sure that the final layout matches the gate-level netlist that we started with. This is physical verification. Timing verification is done through Static Timing Analysis (STA), to make sure that all timing constraints are met, and the circuit will run at the designated clock frequency.

### Introduction to OpenLANE and STRIVE Chipsets
