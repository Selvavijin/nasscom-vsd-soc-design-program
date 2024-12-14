1.Sky130 Day 1 - Inception of open-source EDA, OpenLANE and Sky130 PDK
1.1.SKY130_D1_SK1 - How to talk to computers
1.1.1.SKY_L1 - Introduction to QFN-48 Package, chip, pads, core, die and IPs

Let us understand the flow with the help of arduino board which is available and used vastly.

![a](https://github.com/user-attachments/assets/c52fdd82-cf98-45dc-8f81-db231597a6d8)


The architecture inside the arduino chip is shown below.

![b](https://github.com/user-attachments/assets/ab0b16af-6e89-4b75-8c81-972ec2f2fedb)


The architecture inside the processor/ Soc is shown below. And from now on we will not call this as a chip but as a package. Various packages are available and the chip is present inside the package as shown in the diagram below.

![c](https://github.com/user-attachments/assets/fda304cd-b667-4ab9-b33d-c7b0fc33a6e1)


The boundaries of the chip is connected to the pins present in the boundaries of the package.

![d](https://github.com/user-attachments/assets/9c8b2c14-246d-4ec9-b072-b65a56fa39d6)


Now the internal architecture of the chip is shown below which has Pads(the signals has to cross the pads for entering or exiting the chip), Core and Die(the outer layer of chip).

![e](https://github.com/user-attachments/assets/8f588e7c-979f-458b-8292-bda21ed0d981)



And inside the core we have foundry IPs and Macros. To communicate with the foundry IPs, we need some interface and these are main things. IP stands for intelligence properties because we need some intelligence to build these foundries. The digital blocks such as gates are present inside the Macros.

![f](https://github.com/user-attachments/assets/4c00b579-fac7-4541-be7d-5f8c121d9b1c)

1.1.2. SKY_L2 - Introduction to RISC-V

Instruction set architecture(ISA) - It is the language of the computer and this is the way which we talk to the computer. If we write a C code and it need to be executed inside the layout of an architecture, first the code will be compiled and converted into assembly language(RISC V) and then it is converted into binary language and then it will sent to the architecture to get the required output. Also, inbetween the RISC V architecture and the layout we need another interface called Hardware Description language(HDL). So, the RTL implements the RISC V architecture and then it is sent to the layout.

![image](https://github.com/user-attachments/assets/f97e0038-8559-408d-ad66-6dc14c584012)


1.1.3.SKY_L3 - From Software Applications to Hardware

To operate a software in a laptop, it needs to sent a signal to the hardware. The software applications and the Hardware can be connected throught the block called system software. The system software has elements like OS(has different tasks as shown in the right side of the diagram), Compiler and Assembler and the OS send the task to the compiler to convert the High level language(C, C++,...) into instruction set through the compiler and then it is converted to binary language through the Assembler and then it is sent to the layout. It is important to note that the Instruction set that is generated is in the format for the respective processor(like intel x866). In this case we are using RISC V.

![image](https://github.com/user-attachments/assets/aeef0996-d5dd-43d3-890d-2998b131b7a8)

The real time example using stop watch is shown below. Here the C code is given and it is converted to the RISC V instruction set using the compiler and then the Assemble will convert it into binary code and then it is sent to the chip as shown in the diagram.

![image](https://github.com/user-attachments/assets/f7fd0f88-489d-49c2-add6-8ffc2111b1d5)

The instruction set architecture(RISC V) is called the Abstract interface to communicate with the Hardware, in our case, the instruction in written for the RISC V architecture

![image](https://github.com/user-attachments/assets/3fcfedee-d920-43f2-9473-b991824eacf6)

The instructions given by the instruction set is implemented by the HDL after binary conversion and the Netlist is synthesized and finally the physical design implementation of the netlist occurs to the chip.

![image](https://github.com/user-attachments/assets/15ea842d-5731-43a8-bbc2-1ea89ffd6e43)


1.2.SKY130_D1_SK2 - SoC design and OpenLANE
1.2.1.SKY_L1 - Introduction to all components of open-source digital asic design

![image](https://github.com/user-attachments/assets/9045f848-1a87-469e-9644-b65d89ef95a7)

![image](https://github.com/user-attachments/assets/c6aa5381-439e-4011-afe4-dc017aede4c8)

Getting all the process in chip design in open source is a challenging process before. But now it is possible by using the open source tools as shown in the diagram below.

![image](https://github.com/user-attachments/assets/a3ab57db-cffb-467e-8536-a0cdd4076d8e)

![image](https://github.com/user-attachments/assets/916f7c12-e640-49d1-894c-48d753f91efb)

![image](https://github.com/user-attachments/assets/6d8a5016-23d5-45e7-aaf3-71ef77d9f53d)

1.2.2.SKY_L2 - Simplified RTL2GDS flow

![image](https://github.com/user-attachments/assets/ca272f2e-16bf-4882-a57b-ca7cae275b45)

