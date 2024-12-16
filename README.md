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

![image](https://github.com/user-attachments/assets/70c85d00-2c52-4e26-8e8c-e26aa4d7f737)

![image](https://github.com/user-attachments/assets/aec68b27-5bf9-4e5c-a1c5-7780956ddbca)

The objective in floorplanning or powerplanning is to plan the silicon area

![image](https://github.com/user-attachments/assets/53d291a9-9c2b-470a-bfd0-9a8fd685de3c)

In Macro floor planning, the rows and the routes are defined which will be used later in the placement and routing stage

![image](https://github.com/user-attachments/assets/843833df-5d46-491c-b120-f35e46879814)

Power planning is used to route the power pins. It is done through using horizontal and vertial metal straps. Typically the power distribution network uses the upper metal layer as they are thicker than lower metal layer. Hence, they have less resistance.

![image](https://github.com/user-attachments/assets/4eacb3b9-7c15-4e4d-aa01-c01065baf0bc)

The next step is placement. Here, the gate level netlist is placed in the macro plan. The conical cells are placed close to each other to avoid the interconnect layer.

![image](https://github.com/user-attachments/assets/71584cb8-8810-4d69-886e-ca3c7b3e978b)

Placement is usually done in two steps. Global followed by the Detailed placement. Global placement tries to find the optimal place for all cells and those cells may overlap also. In detailed placement, the overlaps are avoided.

![image](https://github.com/user-attachments/assets/cf3766ca-a50c-4cda-8dec-d21753f0a29c)

![image](https://github.com/user-attachments/assets/e71be08a-8e52-428d-aa71-d0419ba4c7df)

After the routing is done for clock signal, the routing is done for other objects by using the interconnects with the width and and specifications mentioned in the PDK. The skywalker PDK defines six routing layers. The lowest layer is called the local interconnect layer and uses Titanium. The other five layers are Aluminium layers.

![image](https://github.com/user-attachments/assets/3286bc22-9fb9-4f40-9ab1-b3709989a7e1)

Most routers are grid routers. As the routing grid is huge, divide and conquer approach is used for routing. Global routing uses the coarse grain grids and create the routing guides and the Detailed routing uses the fine grain grids.

![image](https://github.com/user-attachments/assets/eaa40ff2-99d6-4c0b-8f36-7be74ce285bb)

Once routing is done, we can go for the final layout which undergoes verification. DRC checks whether the final layout obeys the design rules. LVS checks whether the final layout matches the gate level netlist. STA make sure that all the timing constraints are met and the circuit run at the designated clock frequency.

![image](https://github.com/user-attachments/assets/76266911-0742-4e02-8574-eeb8ffb7cba7)

1.2.3.SKY_L3 - Introduction to OpenLANE and Strive chipsets

![image](https://github.com/user-attachments/assets/1cb75eb1-ea4b-4ad3-861e-eab60147434d)

![image](https://github.com/user-attachments/assets/79e6d3bb-69aa-4b6b-bb29-a4c60e5d9d5e)

![image](https://github.com/user-attachments/assets/365a97b0-0e01-44a5-8b9e-4b2f74711d8d)

![image](https://github.com/user-attachments/assets/6037e284-d99b-4d2b-8902-31926a8188f0)

![image](https://github.com/user-attachments/assets/96bf7e7e-ee9e-4a4b-bd2b-3d082319469e)

1.2.4.SKY_L4 - Introduction to OpenLANE detailed ASIC design flow

![image](https://github.com/user-attachments/assets/d941a814-d579-47e7-be86-9af6dc5bfcf9)

![image](https://github.com/user-attachments/assets/c8956dc9-7cda-47b8-9e6f-15b9d6138260)

![image](https://github.com/user-attachments/assets/b2128454-e4a0-4c93-8081-df9078d6a9da)

![image](https://github.com/user-attachments/assets/dc3243f8-1676-40b3-89c2-81a7f9889829)

Openlane is based on several open source products as shown in the diagram below.

![image](https://github.com/user-attachments/assets/58c3ff12-f11b-4ca2-a45f-ba6921bfb5ff)

Fault is a product used for testing 

![image](https://github.com/user-attachments/assets/7b89c084-5d34-49cb-aca6-085eff7ffda7)

When a metal wire is fabricated, it acts as an antenna and causes charge accumulation which damages transistor.

![image](https://github.com/user-attachments/assets/4eace871-8976-43ed-abcc-3214a038bece)

So, this can be avoided by using two solutions

![image](https://github.com/user-attachments/assets/85ebffb6-8bdb-4dd6-a804-f169a89cd5f1)

![image](https://github.com/user-attachments/assets/6a96a823-b55c-4419-b4b5-34198a049e3a)

![image](https://github.com/user-attachments/assets/0f6f1b3d-307e-4031-973e-639bd230e300)

1.3.SKY130_D1_SK3 - Get familiar to open-source EDA tools
1.3.1.SKY_L1 - OpenLANE Directory structure in detail

It is good to say that the Openlane is not a tool but actually a flow because it is a flow that will happen from RTL to GDS using various tools inside the Openlane. It is similar to commertial tool
![image](https://github.com/user-attachments/assets/6b09b8de-6cd9-4030-8ab4-9263c28b2cfb)

In the above shown diagram, the skywater-pdk has all the pdk related files(timing libs, cell libs).
These silicon control files are compatible to work with commertial EDA tools and not with open source EDA tools. open_pdks mitigate this risk by making it compatible with open source EDA tools(Magic, Netgen). sky130A is a PDK varient. Inside the sky130A, we have two files and the .ref file has the technological related things and .tech has the files related to tool. It is shown in the below image.

![image](https://github.com/user-attachments/assets/5072109b-dd05-47da-b8b3-8e0ec967ec10)

From the libs.ref file, we will be using sky130_fd_sc_hs where, fd-foundry, sc-standard cell, hd-high density.
Lets explore the files inside the libs.ref

![image](https://github.com/user-attachments/assets/79aab84d-8154-4534-9eee-e34fcd98306f)

Here, techlef contains the layer information. mag is the magic files. lib contains all the time files. There, tt-typical, ss-slow, f-fast.

1.3.2.SKY_L2 - Design Preparation Step

In the flow.tcl, we are giving as interatctive mode, The below shown step is to open the openlane

![image](https://github.com/user-attachments/assets/e774f7d9-40b8-47c5-8dcf-744b139fe8ec)

And the command 'package require openlane 0.9' should be done everytime. All the designs that openlane run is from the 'designs' folder. let us see the 'picorv32a' file which has the src, config.tcl and other one file. The 'src' file has the verilog file and the .sdc file. 

Now we will learn the first step which is synthesis. And before that we need to do the design setup stage. And in this stage, the two 'lef' files present are merged so that it is not needed to search the requirements like layer information from two different files and then the preparation stage is completed. and before we go to the synthesis, we will check whether anything new is created in our design directory and a new file named 'runs' is created.

![image](https://github.com/user-attachments/assets/560c787f-879a-4d5b-9341-0881c7560f78)

1.3.3.SKY_L3 - Review files after design prep and run synthesis

Inside the runs folder we have files like tmp, results, reports and logs. except the tmp file everything will be empty as of now because we didn't performed synthesis yet. tmp file contains the merged lef(contains layer and other information) files and other files. the config.tcl file here shows which all default parameters taken by the runs.

![image](https://github.com/user-attachments/assets/378f8763-8a12-4ecc-b686-e5ffb95989bc)

so, after the merging lef files are done using 'prep -design picorv32a' command, synthesis can be done using 'run_synthesis' command. so this will run the yosys synthesis as well as the abc.

![image](https://github.com/user-attachments/assets/6bcb92bc-eb6c-4380-97bd-73722de762db)

1.3.4.SKY_L4 - OpenLANE Project Git Link Description

Now we are running a interactive flow. If we want to run a fully automated flow, we can use the command './flow.tcl -design spm'

1.3.5.SKY_L5 - Steps to characterize synthesis results

First Task:
Let us calculate the flop ratio, which is the number of D Flip Flop to the total number of cells.


![image](https://github.com/user-attachments/assets/5019a0b2-5ccd-4a23-8a13-d802d67d3f04)

now let us see the results, reports in the runs folder. In reports folder, the last yosys file gives the actual synthesis report that we seen in the 'printing statistics' during synthesis.


![image](https://github.com/user-attachments/assets/37da2773-9ac5-457c-9fee-afb1db5b4b9d)


![image](https://github.com/user-attachments/assets/bc3c7120-42a3-4fad-af4b-3e5fc268a6c0)
