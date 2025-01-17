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


2.Sky130 Day 2 - Good floorplan vs bad floorplan and introduction to library cells
2.1.SKY130_D2_SK1 - Chip Floor planning considerations
2.1.1.SKY_L1 - Utilization factor and aspect ratio


![image](https://github.com/user-attachments/assets/6c20a77f-68fe-4e55-991f-2cb281337134)


![image](https://github.com/user-attachments/assets/7ed23541-23eb-4644-a7a1-566a8cbcd693)

The dimensions of the chip depends on the dimensions of the individual elements(gates, FFs, etc).

![image](https://github.com/user-attachments/assets/81e5e7a0-dcc0-4442-bb62-fb0f77b5f550)

So, let us give a rough units for the standard cells and FFs as 1 unit. As of now we won't consider the wires. So, let us remove the wires and place the cells and FFs.

![image](https://github.com/user-attachments/assets/675acbe6-87ed-4d7f-9734-fece5a29227b)

So, this has 2*2=4 units which is the rough dimension of the netlist. The core is placed inside the die.

![image](https://github.com/user-attachments/assets/e29627a0-428f-4f3e-87b5-ffc823f979f7)

Now, let us try to place that netlist inside the core. here, the netlist occupics the 100% of core. So, this is called 100% utilization.

![image](https://github.com/user-attachments/assets/e959c77a-c92e-4bdf-b93c-4b1b3d0a19a6)

So, the utilization factor is 1. Practically we will not go for 100% utilization. We will go for 50 to 60% utilization. Also, when aspect ratio is 1 the shape is square. Else the shape is rectangle.

![image](https://github.com/user-attachments/assets/3e44dce5-4610-4175-8a5e-81285d24b8f3)

![image](https://github.com/user-attachments/assets/58bcee5b-161f-4291-a208-3c4c2540dcb7)

2.1.2.SKY_L2 - Concept of pre-placed cells

Here only 25% of the chip is occupied and the remaining 75% is used for optimization and placing other cells or routing purposes.

![image](https://github.com/user-attachments/assets/d8270d21-9433-4524-8e5a-8b4de6e568ac)

The next step is to define the locations of pre placed cells. For that purpose, let us understand what is preplaced cells ?. To understand this, let us consider a combinational logic that has n number of gates, lets say some 50k gates. We split that into different sections and use that for different purposes as a Black box. Here the functionality is implemented only once and can be used multiple times.

![image](https://github.com/user-attachments/assets/98718e13-9772-425a-ae4f-062123d2a9b1)

To split these into different blocks, the step is given in the below diagram. Once these blocks are placed in during the placement plase, even if we autonomously do the further steps, the positions of these black boxes will not be affected. These blocks are placed before the placement of other blocks. So, this is called pre-placed cells.

![image](https://github.com/user-attachments/assets/0e68aa45-6f04-437f-af63-0021891124a1)

![image](https://github.com/user-attachments/assets/8d8f7ed1-9ec9-4126-8aff-44741337474f)

2.1.3.SKY_L3 - De-coupling capacitors

Now let us see how to locate these pre-placed cells in the core of the chip. Once these cells are placed in location, it can't be changed during the further design process, so placing them is very important. And one more thing we need to do.ie) we need to surround these blocks with the de-coupling capacitors.

![image](https://github.com/user-attachments/assets/f21db4cc-91b0-4a53-9800-518a118749fc)

Let us assume that the inputs pins are in the left side of the core and the output pins are in the right side of the core, so the blocks are placed near the left edge of the core.

![image](https://github.com/user-attachments/assets/dcff2796-0afd-42c2-91fb-4c2bf8b0ed2e)

First let us understand why we need De coupling capacitors.  In the below shown circuit, consider an AND gate. When switching happen in this AND gate(Let us take switching from 0 to 1), it is the responsibility of the Vdd to give supply to the gate to charge the capacitor in the AND gate. Similiarly for switching from 1 to 0, responsibility of Vss to discharge the capacitor. But, if the length of the wire from the supply to the circuit is large, there will be R and L, so in the place where we need to get '1', we get less than that(like 0.7,0.8). Also, even if it is less than '1', the value should be present between the noise margin, other wise the value will be undefined.

![image](https://github.com/user-attachments/assets/6e443daf-b035-410a-b955-cc5f101cd6d1)

![image](https://github.com/user-attachments/assets/c11bbe80-0285-437c-a3fa-e9fec8c73de9)

![image](https://github.com/user-attachments/assets/ad0a8fa7-2d88-42b8-afc0-3ef3c05b7f9f)

To solve this problem, we can use Decoupling capacitors. This is a big capacitor, which can charge till the voltage present in the source. Since the capacitor is present close to the circuit, there will not be any voltage drop in the circuit.

![image](https://github.com/user-attachments/assets/865a8072-926d-4b90-8cfd-bab2563af048)

When there is switching operation happening, the Decoupling capacitor spends charge in the circuit and when the switching operation is not occuring, the capacitor spends time in charging from the main source. So, through this approach, the problem of local communication is solved. The problem of global communication can be solved by using the Power planning method.

![image](https://github.com/user-attachments/assets/1bf1ca9c-11f5-4b0f-bf19-b33fbea50bf7)

2.1.4.SKY_L4 - Power planning

let us consider the same circuit that was considered above and now assume it as a black box. ie) it has to be used multiple times in the chip. 

![image](https://github.com/user-attachments/assets/0fe46d2b-ed93-4f11-b32e-2e910ad48f72)

Let us consider four black boxes and the vss and vdd is connected to all of them. Now let us assume that there is a connection between the first and the last block and the operation is switching from 0 to 1. To make this operation performed, the switch state as mentioned in the diagram should be maintained from the starting to end. To make this done, we have to maintain the Vdd in the red line but we can't add coupling capacitor everywhere. Let us assume the red wire as the 16-bit bus. The value in the wire will not be Vdd because it is distant from the source. So, let us see what will be the value of the red line.

![image](https://github.com/user-attachments/assets/8f1cbfcb-bc6e-4cf2-8d0f-883d5f94310c)

Now let us take the initial conditions of 16-bit bus. It is shown in the diagram below. They have different lines and each have different values. Let us say that it is connected to a inverter, so 1 has to be 0(ie discharge) and 0 has to be 1 (ie charge).  

![image](https://github.com/user-attachments/assets/4955210f-0244-410a-a15b-a669618bbe74)

All of this happen at the same time and we have single ground for the complete 16-bit bus, which results in the ground bounce. If the Ground bounce exceeds the noise margin level, it will results in undefined results. This happens during discharge.

![image](https://github.com/user-attachments/assets/48751270-f42c-4252-8198-3f7ec801d59b)

And during Charging, all the points demanding for voltage at the same time and there is only a single point. At that time there will be a Voltage Droop. It is also OKay when it is within the Noise margin.

![image](https://github.com/user-attachments/assets/2b2f03b0-3065-4e95-8e54-3730ef15fa31)

So these problems can be avoided by adding multiple supple sources.
 
![image](https://github.com/user-attachments/assets/e8e009db-afcb-4b83-ac62-8440d4ffdc51)

![image](https://github.com/user-attachments/assets/aa91310d-5b4f-4734-a398-5df249758114)

This is how the global communication is done. The blocks are placed anywhere and the power is taken or dumped in the nearby Vdd or Vss respectively. This method is used in modern chips. The entire chip is connected with the Vdd, Vss and a Contact.

2.1.5.SKY_L5 - Pin placement and logical cell placement blockage

Let us assume the below circuit for understanding the pin placement. This has two sections of same circuit and have two blocks of preplaced cells and connected as shown in the below diagram.

![image](https://github.com/user-attachments/assets/36884184-d16f-4336-a35a-61e94302a600)

Again let us consider the circuit with the same section as shown above with different colous and also has a preplaced cell.

![image](https://github.com/user-attachments/assets/a17b7ec9-08df-47dc-8255-d93df596ccae)

So the below show is the complete design. 

![image](https://github.com/user-attachments/assets/52d121ca-df28-4e17-b48e-5a42787227b0)

Let us modify the connections as shown below. And this type of connection can be obtained by using the verilog or vhdl. And this is called the Netlist.

![image](https://github.com/user-attachments/assets/a57d1e01-c4dc-48e5-a0d3-d2845a2c0ba8)

Now, let us place the above circuit in the core. For that, let us first place the pin configuration in between the core and die. The pin configuration is fixed by the designer. Here we use, left side for input ports and right side for output ports. Also, it should not affect the preplaced cells. Also note that the clk(in,out) port has higher width. Because, it has to be circulated all over the circuit and so it need a low resistance path as it is driven continuously. 

![image](https://github.com/user-attachments/assets/a293e4a7-8aca-4ed2-82bb-19b92cd5ad76)

We should not place any cells in between the die and core. Because, to make sure that the automated placement and routing tools doesn't place any cells here. Becuause, this area is reserved for pin configuration. This is called the Logical cell blockage. The floorplanning process is over till this step and then we will continue Placement and Routing steps.

![image](https://github.com/user-attachments/assets/e5a4d435-365e-4c1c-bcb9-e8bcfd15c488)

2.1.6.SKY_L6 - Steps to run floorplan using OpenLANE

Standard cells are placed during the placement stage and not during the floorplanning stage.
There are switches present in the synthesis, floorplanning, placement that can be seen from the location openlane->Configurations->Readme file(The variables are the switches). Some of the switches in the floorplanning are, core util, aspect ratio, IO hmetal. Some of the swiches in the placement are Target Density which mentions whether the netlist is closely packed or not by representing the value between 0 to 1. Also in that same location, there are many .tcl files. In that the floorplan.tcl contains the default parameters for the floorplanning. In that, if the FP IO mode is 1, the pin position is random but is equidistant and if 0, the pin position won't be equidistant.
Floorplaning can be runned using 'run_floorplan' command.

![image](https://github.com/user-attachments/assets/69981623-9e83-46a0-926b-e82c0ad41d02)

![image](https://github.com/user-attachments/assets/b694135f-4c49-43c0-bfad-befc8ce8c890)

The variables or switches are shown here from openlane->Configurations->Readme file, shows the requirements for the design. The switches required for the floorplan of the design is shown below.

![image](https://github.com/user-attachments/assets/323fbf37-a423-4d1b-a757-368701342931)

Now let us see, where are these switches set. In the same directory itself, open the floorplan and see the default values set for the floorplan in openlane.

![image](https://github.com/user-attachments/assets/b7ea5005-5037-4597-b9ea-b85a6c1bf1d2)

In the below image, the left terminal shows the system default files and given lowest priority and in the right side, we saw the files earlier and the second priority is given to config.tcl and the first priority is given to the next green coloured text starting with sky130...

![image](https://github.com/user-attachments/assets/09af0f4f-d6af-4e15-b6ad-58c3d1d22302)

The parameters such as io vmetal and io hmetal in config.tcl is +1 more than what is specified in default.



2.1.7.SKY_L7 - Review floorplan files and steps to view floorplan

Now we will check whether the switches present after floorplan take precedence over the system default switches. Here, if we open the runs->logs->floorplan->ioplacer file and compare the io v and h metal with the config.tcl, the value present in the ioplacer file is one more than that of config.tcl(default value).
The config.tcl file shown below shows all the configurations taken by the current flow.

![image](https://github.com/user-attachments/assets/e85e28a1-d096-4865-ab2b-f033575048fc)

To see the floor plan file, go to results->floorplan. Here, Diearea (0 0) implies the least x and y value and the next value represents the highest x and y value. 

![image](https://github.com/user-attachments/assets/ef532966-863c-4c53-a9f5-1d3065a5c103)

By looking into the .def file, we don't know where what is placed. So, we can see the actual layout in magic. 

![image](https://github.com/user-attachments/assets/930c6763-7e11-4e52-b22a-2ea7f97e2a0c)

Here, -T implies tech file.

2.1.8.SKY_L8 - Review floorplan layout in Magic

To work with the Magic file, first click s to select all and press v to fit to the screen. To zoom a particular area, first left mouse click, then right mouse click followed by click z to zoom.

![image](https://github.com/user-attachments/assets/bd2f2f0f-07bd-421b-9d38-889bf19979c7)

In a previous video, it is mentiond that the IO mode is 1 to keep the pins equidistant, so the pins are equidistant as shown in the above diagram. To select a particular object from the layout, hover the cursor on that object and click s to select. When a object is selected and we type what in the window that is generated along with the magic layout, we will get the details of the particular object as shown below. Also, there are decap cells in the boundries as shown in the image which are called the end endcap cells.

![image](https://github.com/user-attachments/assets/4db73577-938c-400b-9619-2f524284bea8)

Also we have tapcells which is used to avoid the latch up condition in the cmos devices. They connect the Nwell to the Vdd and substrate to the Ground. These tap cells are diagonally equidistant. As mentioned before, the standard cells are not taken into consideration. But, standard cells present here in the lower left corner. If we wish to make any changes, we can make in design related config.tcl file which makes it more flexible.

![image](https://github.com/user-attachments/assets/2d4140b3-885b-45c2-a49a-555883a08a54)

2.2.SKY130_D2_SK2 - Library Binding and Placement
2.2.1.SKY_L1 - Netlist binding and initial place design

 The next step is to bind netlist with physical cells. Genrally we find the functionality of the gate by looking into it like, if it is OR shaped gate, it performs Addition. But, in real time, there is no different physical shape to gate. Instead, a gate will be given a specific width and height.

 ![image](https://github.com/user-attachments/assets/1e246303-7b4e-4acb-afeb-d0f2db8a9ca2)

![image](https://github.com/user-attachments/assets/7e7b95ac-28b7-45af-a514-a11834f86391)

All these shape and size and delay information are found in the library file. There are two library files. In one file there will be information about the shape and size of the gates and in another file there will be delay of gates specified. Also it contains various flavors of the same cells.

Lets say that the number '2' indicates the AND gate. When the size is bigger, there will be low resistance path and the gate will be faster. So, these are the various flavours.

![image](https://github.com/user-attachments/assets/2127b5e2-efb3-4541-b623-150013431139)

The next step is to take this and place it in the floorplanning. In the figure shown below, only the last image is placed in floorplan and the middle picture is used only for connectivity purpose.

![image](https://github.com/user-attachments/assets/6d0f69d6-bf46-4fbe-b95f-71b456a56a2b)

Now we will place the components and it should not affect the preplaced cells that are present already. Also, the components we are placing should close as possible with the input and output ports to minimize the delay. In the figure shown below, the orange colour gate will have some delay and the yellow color gates will have very minimum delay because the gates are close to each other.

![image](https://github.com/user-attachments/assets/7c4345d3-b349-47f4-80d0-efdf1b8068e6)

2.2.2.SKY_L2 - Optimize placement using estimated wire-length and capacitance

The blue and green colour gates are placed in a manner as shown in the figure below because of the distance between the input and output ports. This problem can be solved using optimize placement.

![image](https://github.com/user-attachments/assets/6677d805-7742-46f7-80f8-b7cead5703f4)

Let us assume Din2 and FF1 of yellow gate. Here, the distance is large. So we find out the capacitance between the gate and Din2. This step is done before the routing stage. So, since the distance is large, we use repeaters(Buffers) to maintain the signal integrity. The disadvantage here is the loss of area. Repeaters and Area are inversely proportional to each other.
 
As shown in the diagram below, we place repeaters between Din2 and FF1 to maintain signal integrity. The decision to place repeators will be based on the estimation of wirelength and capacitance and transition value and slew value which we will see in the upcoming videos.

![image](https://github.com/user-attachments/assets/047375c0-50e1-4506-bcda-38aefc427c43)

2.2.3.SKY_L3 - Final placement optimization

When we don't want any delay and work at high speed, we can abet the circuit as shown for the orange gates.

![image](https://github.com/user-attachments/assets/1a472301-0e81-4836-a43f-682f74ff0a29)

Once the placement is done, we have to check whether what we have done is correct or not. Since there are no clock, we have to consider the clock to reach the gate is ideal or zero and look into the data path. So, we have to do a setup timing analysis(Hold will not make any sense since there is no clock). Based on the timing analysis we will come to know whether the placement we done is reasonable. If the timing doesn't meet the specifications, we have to correct this by this step itself. because, it will go worse if we go to further steps and then change it.

2.2.4.SKY_L4 - Need for libraries and characterization

Let us see the technical IC design flow that every design needs to go through. CTS(Clock tree synthesis) take care of sending the clock signals to the cells at the right or equal time. The clock buffers that is present in the below diagram in triangular shape make sure that the clock signals has equal rise and fall time. Then, while routing two cells, the properties of the cells should need to be taken care.

![image](https://github.com/user-attachments/assets/8220da0a-6110-4199-b204-7ee589e9db82)

The final thing in IC design flow is STA

![image](https://github.com/user-attachments/assets/f62e7a6d-c30f-4f07-87a9-13e25af91314)

The common thing among all these steps is the Gates. How library is related to this is, the gates are represented using the values that are represented in the library. Only then the EDA tool will understand which gate is this. Eg: We will understand the AND gate by simply giving two inputs and one output, but the EDA tool will not understand that.

2.2.5.SKY_L5 - Congestion aware placement using RePlAce

Placement occurs in two stages global and detailed. The objective of global placement is to reduce the Half parameter wire length(HPWL) and once we run the command run_placement, number of iterations will run and as the number of iterations increase, the overflow value will gets reduced. 

![image](https://github.com/user-attachments/assets/616333b1-3634-4364-84e4-257080fc8067)

The standard cells are placed in this stage and the placed standard cells are shown below. Usually, the power distribution networks(Vdd, ground) are placed in the floorplan stage itself. But in Openlane, we will do it before routing.

![image](https://github.com/user-attachments/assets/c6924e35-3711-4478-a934-ac5e78e37b07)

![image](https://github.com/user-attachments/assets/d8112398-6bea-4e77-ab02-85285418bd36)

2.3.SKY130_D2_SK3 - Cell design and characterization flows
2.3.1.SKY_L1 - Inputs for cell design flow

Standard cells are placed in the library which contains all the information about the gates or standard cells. All the cells present in the ciruit other than preplaced cells are standard cells.

![image](https://github.com/user-attachments/assets/01fc68eb-5d50-4eaa-8300-0dd4e041c5de)

The library will have cells of same name(AND, OR) with different functionality, size, Voltage Vt. 

![image](https://github.com/user-attachments/assets/b294d5bb-4e44-4167-8f52-f69b228b2b42)

Let us take an inverter for example. We will say an inverter as a one input cell. But, in IC design flow, it has some more things such as timing behaviour, shape, power characteristics. To design a inverter, it has to go a typical flow.

![image](https://github.com/user-attachments/assets/473e2c8b-b153-4107-8238-dfdcb696c53f)

The inputs to design a inverter will come from the foundry using PDKs which consists of DRC & LVS rules, SPICE models, library and user defined specs. 

![image](https://github.com/user-attachments/assets/8bf5f79d-5f6a-42a0-a947-77d675701689)

The SPICE model has different parameters. The circled variables in the idendities shows the SPICE model parameters where the values will be given form the foundry.

![image](https://github.com/user-attachments/assets/7fb5e802-5307-4c87-897b-c47f9392086e)

2.3.2.SKY_L2 - Circuit design step

In the library and user-defined specs, the example is the cell-height which is between the ground and power line. The drive strength varies from 1 to x. If the drive strength is low for a wire, then it will be difficult for that wire to drive huge wire. This drive strength decides the cell width.

<img width="907" alt="image" src="https://github.com/user-attachments/assets/47fc20c6-7836-47e5-8d11-e43158198ef9" />

Also, it is responsible for the user to define the metal layers when needed, also the pin location where ever additionally we need.

<img width="883" alt="image" src="https://github.com/user-attachments/assets/8bc721b2-fe3a-4ef5-9375-f4a806212005" />

Now it is the responsibility of the developer to obey the steps mentioned in the inputs and follow to design the library cell. So, the next step is Design steps which consists of Circuit design, layout design and characterization.
Design steps:
Circuit design :
   In this step, the the pmos and nmos are designed in such a way that it meets the library file requirements like setting the width and height, current of transistors. Once we know the W/L of the Nmos and Pmos, we enter into the second step which is layout design. Before going into that, the output we get from the circuit design is the CDL(Circuit Description Language).
Layout Design:
   Here, the function is implemented through the MOS transistor and the next step is to get the Pmos and Nmos network graph of the design that we implemented.

<img width="911" alt="image" src="https://github.com/user-attachments/assets/a67a3cc1-a6ce-49b2-bcc0-d3ac475ef454" />

2.3.3.SKY_L3 - Layout design step

The next step in Layout design is to draw the Euler's path.

<img width="926" alt="image" src="https://github.com/user-attachments/assets/f75943b9-0f3b-409f-b26a-c8cc4d4806c2" />

Based on Euler's path, the next step is to draw the stick diagram.

<img width="929" alt="image" src="https://github.com/user-attachments/assets/9db011f5-7db5-405c-948b-b5ec73714b45" />

The next step is to get is layout diagram as per the rules like DRC rules in the input and get the layout done.

<img width="904" alt="image" src="https://github.com/user-attachments/assets/2e79c9cb-e051-4a97-b84f-21e2c9284447" />

The output of the Layout design will be GDS II, lef(contains the width and height of the cell), extracted spice netlist(parasitics or the R and C of each and every element present there)
Characterization:
The next step is to extract the parasitics from this particular layout and characterize in terms of timing, noise, power.

<img width="904" alt="image" src="https://github.com/user-attachments/assets/fe08e880-552e-4ae2-9739-2daa377ae2ce" />

2.3.4.SKY_L4 - Typical characterization flow

Before going into the characterization flow, we will see what are the things we have now. 

<img width="898" alt="image" src="https://github.com/user-attachments/assets/54abe5d1-394d-41dc-a16f-1ba924c7536f" />

We have the description of the buffer which contains subset of inverter which has the nmos and pmos models. Both ineverters shown in the diagram are called from the subset and the resistance, capacitance are shown in the main description.
The spice models of the NMOS and PMOS are shown in the below image. These spice models are nothing but the characteristics of nmos and pmos.

<img width="943" alt="image" src="https://github.com/user-attachments/assets/487dab40-41bd-43c9-9ad1-1762aea27451" />

These are the things that are available with us. Now let us do the characterization flow. So, the first step is to read the models(nmos, pmos), the second step is to read the extraced spice netlist, the third step is to define the behavior of the buffer. The next step is to read the subcircuit of inverters. The next step is to read the necessory power supplys. The sixth step is to apply the stimulus. The next step is to provide the necessory output capacitors. the last(8th) next step is to give the necessory simulation commands. In this case we are doing transient analysis so we are using .trans. Then we have to feed in all the inputs from the 8 steps in the form of configuration software called GUNA. And this software will generate Timing, noise and power models.

<img width="862" alt="image" src="https://github.com/user-attachments/assets/ec621ded-9163-4d47-b652-98c033cec11a" />

<img width="864" alt="image" src="https://github.com/user-attachments/assets/1ef1fe55-e8f8-45de-bc72-4f7968999215" />

<img width="914" alt="image" src="https://github.com/user-attachments/assets/47605f30-38e7-463c-8961-e14de5dfe374" />

2.4.SKY130_D2_SK4 - General timing characterization parameters
2.4.1.SKY_L1 - Timing threshold definitions

Here we will understand about the power.lib, timing.lib and noise.lib. These are important concepts because these are important to understand GUNA software.

<img width="916" alt="image" src="https://github.com/user-attachments/assets/6ec3bd65-f216-43aa-a86b-114f66beca5e" />

Here we have two plots which are used to understand the different threshold point of waveform which are called Timing threshold definitions. slew_low_rise_thr says that if we want to find the slope or slew of a waveform, we need to have two any different points from the waveform. But, we need to define these values. And this value of the threshold could be 20% or 30%. Let us take it as 20%. 
slew_high_rise_thr is the value of 20% from the top. The slew can be calculated from the timing difference between high and low slew threshold. This is for the rising waveform.similarly for the falling waveform, we have, slew_low_fall_thr and slew_high_fall_thr.

<img width="931" alt="image" src="https://github.com/user-attachments/assets/a8693a76-460e-4260-b76f-68be0896364e" />

To understand the next 4 threshold let us take the input stimulus and the output of the buffer. We calculated the slew initially, similarly we can also find the delay of an inverter, we need some points to calculate. The required points are one input point and one output point. We take the 50%(center point) for our purpose.

<img width="926" alt="image" src="https://github.com/user-attachments/assets/cf117834-c591-4541-ae35-44fb4a8ecba2" />

<img width="947" alt="image" src="https://github.com/user-attachments/assets/1acff943-aa1d-401e-97b2-5e127fd25b90" />

A buffer will get two kinds of delay(rise delay and fall delay).
slew_low_rise_thr(the value of rising waveform, lowest point, used to find the slew)
in_fall_thr(it is the point in falling waveform, used to find the delay).

2.4.2.SKY_L2 - Propagation delay and transition time

Timing characterization for propagation delay:
If the propagation delay is not taken care, it might lead to unexpected results.
Let us consider the same buffer cicuit that was shown above. We find the delay of buffer using the formula mentioned in the diagram. Also, let us take the value as 50% of the waveform and this may vary in industries.

<img width="922" alt="image" src="https://github.com/user-attachments/assets/6be5e447-6842-416e-84c5-88ecd5124fcb" />

Let us take a sample waveform and see how we can apply all these in that waveform.

<img width="926" alt="image" src="https://github.com/user-attachments/assets/de3032d2-c78e-4b50-8610-2277613c0ece" />

Here, the in_rise is taken as 50% and the out_fall is also taken as 50% and the delay is calculated. Here there is no problem. But, the problem arises if by any chance if the threshold is in other place of waveform, there are chances of getting negative delay value which is not desired as shown below.

<img width="913" alt="image" src="https://github.com/user-attachments/assets/d7d61180-ad2b-4ff5-baac-93a667ea185f" />

There is another case when we choose the correct threshold but still we get the negative value if the waveform is like as shown in the below figure. This problem occurs if the wire length is high due to which the delay occurs(ie: The distance between the two inverters is large)

<img width="925" alt="image" src="https://github.com/user-attachments/assets/182d09b5-ac25-499b-976b-dba79b067155" />

If we zoom into the center of graph that is shown above, we will get the delay and that is negative which is not desired.

<img width="919" alt="image" src="https://github.com/user-attachments/assets/52257ecb-26f0-499f-a5ad-b4b3903c7398" />

Timing characterization for transition time:
  It is quite easier to calculate. We can find it by subtracting the high and low threshold of rise(fall) waveform. 
Here there is no input or output delay, there is only rise delay, fall delay and rise transition time and fall transition time. Now, let us take the value for the low threshold as 20% and for high threshold as 80% and calculate the transition time is calculated.

<img width="943" alt="image" src="https://github.com/user-attachments/assets/0f186196-e294-4ff5-acc9-587958d7d350" />

3.Sky130 Day 3 - Design library cell using Magic Layout and ngspice characterization
3.1.SKY130_D3_SK1 - Labs for CMOS inverter ngspice simulations
3.1.0.SKY_L0 - IO placer revision

It is difficult to design the inverter from the scratch. So, we will download pads from the github and see how things work. Now, let us see how the IO pins are placed in the code. Right now it is equidistant and randomly placed. Let us say that we need to change the IO pins to another IO strategy(current strategy is present in floorplan.tcl file). There are 4 strategies supported by IO space(An opensource EDA tool to place the pins around the core). Currently the IO mode is set to 1. Also, 0 is one of the modes, 2 is also one of the modes. Now, let us switch the mode to 2. The output file is shown below.

![image](https://github.com/user-attachments/assets/391ac35a-a3a9-4740-ae2d-28ca23c1aec0)

3.1.1.SKY_L1 - SPICE deck creation for CMOS inverter

To do the SPICE simulation, the first step is to create the SPICE deck which is the connectivity information about the netlist. Here we need to mention the connectivity of the substrate also. So, it is shown as arrow. There are lot of theory in the cload. Those things we see when we do the dynamic characteristics of CMOS. Now we are not going to looking into it because we are seeing only static characteristics of CMOS. Just we are taking a value for cload and proceed.

![image](https://github.com/user-attachments/assets/47ff9882-f286-429d-a289-92d145da36e2)

After connectivity, the next step is to define the value for the components. There is another case where the width of the Pmos should be greater than Nmos, we will come to it later. Now let us consider the same width. Next step is to define the input gate voltage and supply voltage. usually the ip gate voltage will be in the multiple of transistor length. 

![image](https://github.com/user-attachments/assets/11ce7dc1-b448-4e81-8d8e-361227506b7d)

Next step is to define the nodes. It is formed between two components. For SPICE simulation we need to say that the component is placed in between this and that node. 

![image](https://github.com/user-attachments/assets/54573841-46d5-4bd8-8071-b7528007f7d0)

Next step is to name the nodes.

![image](https://github.com/user-attachments/assets/b81a6c12-4de8-4135-97f7-a1b142c734c3)

Let us start writing the SPICE deck. *** is for comment. Then the code is written for M1 and M2. Let us understand the M1, out -> node of drain, in->node of gate, vdd->node, vdd->node of source, vdd->node of substrate, pmos->mentions that the M1 is pmos.

![image](https://github.com/user-attachments/assets/294a5486-75d4-4b2b-a55b-7280c8672830)

3.1.2.SKY_L2 - SPICE simulation lab for CMOS inverter
  Once we write the commands for all the components in the netlise, we need to write command for simulation. Here, .dc Vin 0 2.5 0.05 states that the input voltage is sweeping from 0 to 2.5V at the step size of 0.05. The final step is describe the model file.  This has the complete description of the nmos and pmos transistors. All the details for the nmos and pmos are taken from this file by identifying the nmos or pmos keyword that is mentioned in M1, M2.

![image](https://github.com/user-attachments/assets/b56a2f47-a21e-4949-bcc4-a0d0a35635d9)

Now let us see the model file.

![image](https://github.com/user-attachments/assets/7e2da4ee-e6a7-436e-a4d6-32a46887f341)
M2 is identified as pmos by using this keyword. Now the simulation is done using ngspice. 
The simulation result of above code is given below. At is center part, it is slightly shifted to the left. Let us see it why later.

![image](https://github.com/user-attachments/assets/6138cb0a-0500-448e-89cc-1977dda99735)

Now we are increasing the pmos width to 2.5 times of nmos. Why?, we will see it later. The code for this case is shown below. 

![image](https://github.com/user-attachments/assets/a6548586-0f00-40ab-8eee-3b66097b39a7)

The output of this case is shown below.

![image](https://github.com/user-attachments/assets/338cd8a6-32c8-4393-ad8d-80a6f27eb221)

we will compare the two graph in the next video.

3.1.3.SKY_L3 - Switching Threshold Vm

Each types has different applications. There is nothing good or bad. 
The shape of both waveforms are same. In both graph, when the ip is high, the op is low and vice versa. This shows that the Cmos is very Robust. 

![image](https://github.com/user-attachments/assets/d304db38-3cff-4cb0-ab85-683345d87a13)

Another parameter that defines the robustness in switching threshold(Vm). It is the point where Vin=Vout. The Vm of first graph is around 0.9 and that of second graph is around 1.2. This is a very critical area where there are chances of leakage current. In the upper or lower part of the graph, either pmos or nmos will be in ON state. But, at this point, both will on at the same time(Both will be in saturation region). 

![image](https://github.com/user-attachments/assets/e5988cc8-a56f-4d83-bbcb-fb8fe18893a5)

![image](https://github.com/user-attachments/assets/b9448e7f-c0b3-4673-8f08-7f2baa6f2830)

At this point where Vgs=Vds, Idsp and Idsn are equal but in opposite direction.

3.1.4.SKY_L4 - Static and dynamic simulation of CMOS inverter

We saw the DC transfer characteristics. Now let us try to understand the dynamic characteristics of the CMOS and find the delay. For this we will see the deck which is same as we saw before. But, the only chage is in the Vin we are giving the pulse input and in the simulation command, we are giving code for transient analysis. The pulse input is shown in the diagram below. In the code, "pulse 0 2.5 0(step size) 10p(rise delay) 10p(fall delay) 1n(pulse width) 2n(width of a cycle)"

<img width="932" alt="image" src="https://github.com/user-attachments/assets/81afe6b0-3932-40b7-8725-687f90343425" />

Now we are going to give this wave as the input to the cmos and do transient analysis. We can calculate the rise and fall delay. rise delay is the case where the output rise.

<img width="870" alt="image" src="https://github.com/user-attachments/assets/5900deb8-badf-48e6-95cd-7061c2944977" />

As selected in the diagram, we are selecting the 50% of the waveform and calculate the delay.

<img width="928" alt="image" src="https://github.com/user-attachments/assets/87fae96d-366f-4354-8399-ad3474a5c720" />

So, we get the rise delay as 0.14831. 
Similarly calculating for the fall delay, we get 0.07167.

<img width="938" alt="image" src="https://github.com/user-attachments/assets/88618412-6374-4e49-bbc8-80cee98d688c" />

This is how we calculate the delay of inverter.

<img width="946" alt="image" src="https://github.com/user-attachments/assets/1a96b2ab-788a-49d8-817e-79939203bb0d" />

3.1.5.SKY_L5 - Lab steps to git clone vsdstdcelldesign

We are not goint to build the inverter from the scratch, instead we will clone a github link and use it. From there we get .mag file. We are going to do spice extraction and post layout spice simulation.

![image](https://github.com/user-attachments/assets/d2b2c646-8271-4635-955a-85b7f90a88d2)

To open the .mag file, we need .tech file. So, we will copy the tech file in the cloned directory itself.

![image](https://github.com/user-attachments/assets/453a8b9a-1614-4a43-8cfa-fd1ee5294266)

'&' is used to free up the command prompt. If we didn't give it, it will be like as shown below.

![image](https://github.com/user-attachments/assets/9f0f89f7-01af-41bc-b7ce-703943b5e548)

3.2.SKY130_D3_SK2 - Inception of Layout ÃÂ CMOS fabrication process
3.2.1.SKY_L1 - Create Active regions

16-mask CMOS process:
The first step is selecting a substrate. All the things that we do in physical design is fabricated on the substrate. There are many substrates available, we will look into one of the commonly used substrate which is the p-type silicon substrate. The substrate doping level should be less than that of well doping. SiO2 act as an insulator.

<img width="924" alt="image" src="https://github.com/user-attachments/assets/e2b0ee1c-9c07-4386-8bd5-75a157bd801b" />

The next step is to create active region for the transistors. And to create active region, we need to create buckets that are isolated. And we have to identify the regions that we are going to create the bucket. We do some things in the photoresist, that will clearly define some layers in the substrate. Mask is placed above the photoresist layer. It is used to protect the n-well region from any reaction.

<img width="934" alt="image" src="https://github.com/user-attachments/assets/22a694d3-9cd3-462d-a940-224f281a41e9" />

When the UV rays are passed on the top layer, the masked layer will not get affected and the other layer will do some chemical reaction and that layer is cutted off.

<img width="925" alt="image" src="https://github.com/user-attachments/assets/d799e2d4-7f40-4127-87bd-5f81d55c4d5a" />

The next step is to remove the mask. 

<img width="938" alt="image" src="https://github.com/user-attachments/assets/21d2d9ba-a42c-4c42-9af2-6b63b3755ffb" />

We can also remove the silicon nitride in the unused area.

<img width="923" alt="image" src="https://github.com/user-attachments/assets/56b37df1-3e8f-4d96-ac8f-d143d57b3379" />

The next step is to remove the photoresist itself. Because, the Si3N4 itself will act as a very good protective layer. If we put the complete setup in the oxidation furnace, only the place which does not have Si3N4 will grow and the other layers are protected. The places where the SiO2 is grown is called Isolation region. So, while fabricating transistors, they won't be able to communicate with eachother because of this isolation region. This process is called LOCOS(Local Oxidation of Silicon)

<img width="947" alt="image" src="https://github.com/user-attachments/assets/8e6f23c5-bb73-44c1-bade-93dd3e2af060" />

The next step is to remove the Si3N4 and this can be done using hot Phosphoric acid.

<img width="931" alt="image" src="https://github.com/user-attachments/assets/8767b9f0-1ca9-4227-88d3-31efac132b8e" />

3.2.2.SKY_L2 - Formation of N-well and P-well

N-well will be used for NMOS fabrication and P-well will be used for PMOS fabrication. Both can't be done at same time. We need to protect one area while we fabricate the other. Now, again the same steps are repeated like creating a photoresist and mask.

<img width="933" alt="image" src="https://github.com/user-attachments/assets/7b6c078b-45b0-41dc-b215-6f5e16973a21" />

Let us see the top layout of mask. The place where the cursor is placed is the mask region.

<img width="936" alt="image" src="https://github.com/user-attachments/assets/2b95618b-2f71-4be2-b5c8-355520db0f8a" />

Then the UV light is passed and the below layout occurs.

<img width="935" alt="image" src="https://github.com/user-attachments/assets/987939d6-83e8-4cf5-b99a-b6220db76564" />

Then we remove the mask. Then we create a p-well using Boron which is a p-type material and it is diffused into the p-type substrate using a process called ion implantation. The energy need for the Boron to diffuse through the SiO2 layer is about 200keV. Ion implantation is the process where some ions are shot into the particular area with very high energy. While penetrating throught the layer, the SiO2 layer will get damaged and we will see how we can repair it.

<img width="932" alt="image" src="https://github.com/user-attachments/assets/2382f562-a46b-4370-9802-93dc6ce18dfa" />

The similar steps is followed for N-well. Here we use Phosphorus which is a n-type material and it is heavier than Boron. So, we need quite high energy to penetrate through the Si02 layer.

<img width="933" alt="image" src="https://github.com/user-attachments/assets/df367ea1-4c07-4d8d-b0b9-eb71094f11ce" />

Now we have created the well region. But, the depth of the well is not finalized yet. Then we have to diffuse the well so that it occupies half of the substrate.

<img width="942" alt="image" src="https://github.com/user-attachments/assets/458f8e4d-cd65-4213-8aff-935b38fbaf0b" />

Then we put this setup in a very high temperature about 1100 degree celcius for 4 to 6 hours which is called the drive in diffusion. This make the diffusion of wells. This is called Twin Tub process because there are two tub like structure(N and P well). This is the bucket creation.

<img width="926" alt="image" src="https://github.com/user-attachments/assets/ac095e94-38d1-4612-8bbb-82c5edf8d9c9" />

3.2.3.SKY_L3 - Formation of gate terminal

The gate is the one which control the threshold voltage(turning ON voltage of transistor).

<img width="942" alt="image" src="https://github.com/user-attachments/assets/2230f755-e13a-4273-b024-e25f62274bac" />

So, we look into how to control the Cox and Na in further steps. 
This is the 16-mask process and now we are using the 4th mask. And the steps remain same.

<img width="943" alt="image" src="https://github.com/user-attachments/assets/5b0556af-bb33-4698-b5bb-2332bddb5618" />

Again we are going to use Boron but with low energy. Because, now we need the Boron to be just in the surface. The dose of the Boron is maintained in such a manner that we achieve the required doping concentration and this concentration is dependent on the threshold voltage. Again, there will be damages in the Sio2 layer and we will see how to repair it later.

<img width="935" alt="image" src="https://github.com/user-attachments/assets/177317b6-1fbe-4ed8-ba25-42bee29e2e5f" />

Similarly it is done for N-well and here we can use Phorsphorus or Arsenic which are n-type impurity.The energy required is also very low.

<img width="943" alt="image" src="https://github.com/user-attachments/assets/04cdc843-f504-4b3b-98a5-fb45ef1bfb01" />

Then we have to repair the SiO2 by removing using the HCL acid which reacts to SiO2 to remove the Oxide part. Then we regrow the High quality SiO2 with the same thickness. Oxide capacitane is controlled using the oxide thickness. Doping concentration is maintained by the p and n type impurity that we added. 

<img width="938" alt="image" src="https://github.com/user-attachments/assets/55bc63a5-0d82-4ad2-bd13-ee935016a4c0" />

The next step is the formation of gate where we deposit the thick polysilicon layer. The gate should be of low resistance.So, we dope it with some more imputities. We use any N-type materials like Arsenic and implant it on the top of polysilicon for low gate resistance. Then we follow the same steps that we followed above.

<img width="925" alt="image" src="https://github.com/user-attachments/assets/2d0cfa98-5e02-4cf2-beaa-b30b6b2bbec8" />

The top view of the mask6  is shown below and tilted 90 degree. We will see the reason later.

<img width="926" alt="image" src="https://github.com/user-attachments/assets/9325b59d-71ac-4151-bb53-ebf3589ac224" />

The remaining areas of the polysilicon can be removed.

<img width="912" alt="image" src="https://github.com/user-attachments/assets/47e4ee58-7fa4-4799-8741-782b4ecd9fa8" />

Then we remove the photoresist region. Then the remaining we get as gate.

<img width="935" alt="image" src="https://github.com/user-attachments/assets/9b0ca583-0ab3-4040-adc5-ec3323023422" />

3.2.4.SKY_L4 - Lightly doped drain (LDD) formation

So, as mentioned earlier, Pmos will be fabricated in the N-well. For that we need P+ source and drain and lightly doped P-. Similar case for P-well.

![image](https://github.com/user-attachments/assets/ca84990d-2733-4798-87a6-ad1ba9740794)

We can go with P+ and N(Which is already present). Why this P- is needed ? . 2 reasons for this as shown in the image below.

![image](https://github.com/user-attachments/assets/7c776e0c-cc9e-4d92-bc91-3c220c1ca5f5)

Let us understand the Hot electron effect first. E-Electric field, d-device size. When the size of the device decreases, the Electric field increases, so the electrons and holes will attain the tremendous amount of energy which even break Si-Si bonds leading to more holes and electrons. The general conduction band energy is 3.2eV. So, if the carriers crosses this voltage, it will enter into the SiO2 layer.
In the second effect, for short channels, the drain area will just penetrates into the channel area.So, it is difficult for the gate to control the source and drain current.
The standard steps for the Photolithography remains same. And we are passing n-type impurity like phosphorus into the p-well. Then the N-(Lightly doped) implant takes place. Here, the dose of the phosphorus should be carefully chosen so that it does not diffuse deep in the well. The gate will protect phosphorus from entering into the center area.

![image](https://github.com/user-attachments/assets/ea257dfc-3d7d-42a2-b2cd-a7566459d24b)

![image](https://github.com/user-attachments/assets/ff0513b2-65b8-4c1e-b97f-9d329c3f93fb)

The process is not over yet. When we create the actual source and drain, the Lightly Doped regions should not get disturbed. So, we need to protect these. We can do this by using the side-wall spacer zone.
We have to deposit a thick layer of Si3N4 or SiO2 on the top and do anisotropic etching.

![image](https://github.com/user-attachments/assets/a01ebcb6-6656-4168-99e2-440690b4bbb4)

![image](https://github.com/user-attachments/assets/371d7572-b68c-4894-a8e5-ad603f2af183)

As shown in the above diagram, the green coloured layer protects the below Lightly doped region during the Source and drain formation.

3.2.5.SKY_L5 - Source and drain formation

Then a thin layer of SiO2 is added over the top to avoid the effect of channeling.

![image](https://github.com/user-attachments/assets/d72958d3-52b2-4727-ad54-60533ab73e84)

Now, we are using mask 9 with the same procedure above.

![image](https://github.com/user-attachments/assets/c5118808-a3f4-4237-b94a-6c318b49560e)

![image](https://github.com/user-attachments/assets/94c00613-976b-43f6-8fc5-3053757c2804)

Now we got a N+ source, lightly doped N- region, P region, Lightly doped N- region, N+ drain

![image](https://github.com/user-attachments/assets/989dc56b-4a94-4bcb-a4ff-516bd02f9fc2)

We put this setup in high temperature annealing(method used for diffusion of layers) of 1000 degree celcius for some deep penetration into the wells.

![image](https://github.com/user-attachments/assets/4652ebd4-af93-4241-8fb6-64fae3bfa1c3)

3.2.6.SKY_L6 - Local interconnect formation

Contacts are very important because that are the only thing that is accessible to users to control the electrical characteristics of mos.
Remove the screen layer.

![image](https://github.com/user-attachments/assets/03e568e6-39c9-4d90-8109-816ae60e9520)

Titanium - metal with very low resistivity. 
sputtering - Hit the titanium metal with some Argon gas. so, the metal particles in titanium is removed and deposited on the substrate.

![image](https://github.com/user-attachments/assets/3ea74a66-a28f-42bd-b4d5-8c9d28c7bddf)

![image](https://github.com/user-attachments/assets/695e6851-fc2a-4f85-acff-e3fcf80deb8b)

The next step is to create the contact between the titanium that we deposited and the source, drain and gate. This can be done by heating the wafter with the N2 ambient at 600 to 700 degree celcius. The result is we get TiSi2 which is low resistant and can be used for local interconnect.

![image](https://github.com/user-attachments/assets/4dc17c37-4e5e-4897-be17-8a17e91e5a4a)

Also, there is TiN layer is developed which is used only for local communication.

![image](https://github.com/user-attachments/assets/e06e67ff-8225-453c-9409-2c2d56235e26)

![image](https://github.com/user-attachments/assets/51bf8f4c-f600-4d28-9fe4-8e58bd6cc232)

These are the contacts that we need to come out from the chip. So, we can remove the remaining TiN by RCA cleaning.

![image](https://github.com/user-attachments/assets/064aa377-23f6-422e-9185-9c9e15d7715c)

![image](https://github.com/user-attachments/assets/c087d761-e429-446c-bba4-6795ae773362)

3.2.7.SKY_L7 - Higher level metal formation

Now we have an uneven surface. So, we deposit a thick layer of SiO2.

![image](https://github.com/user-attachments/assets/bfbc02ab-c3cf-49e0-9c8b-ff84ee2b5288)

Still we have uneven surface. We polish this surface which is called Chemical Mechanical Polishing(CMP).

![image](https://github.com/user-attachments/assets/b372446c-0c7a-4846-9941-2adc9f051eaa)

We drill the contact points by using the photolithography method. Then we deposit a thin layer of TiN. Because it acts as a very good barrier for the lower and higher metal layer.

![image](https://github.com/user-attachments/assets/b856dbec-98d1-402c-9086-61001a4a2145)

Blanket tungsten layer helps to get a very good contact from bottom to top.

![image](https://github.com/user-attachments/assets/d56b76a3-b1f6-46d3-aa61-a166af4c9a11)

Again we do CMP

![image](https://github.com/user-attachments/assets/a8f5321c-2c36-461d-ac2b-1c67a0a5aea3)

Now we have to bring these contact points outside the chip. So, we deposit a Al layer and do photolithography steps. Here 13th mask is used. 

![image](https://github.com/user-attachments/assets/640ffd2b-8283-4b44-b3be-8e4891dbc5d6)

![image](https://github.com/user-attachments/assets/faa09be0-7c65-4ec4-8092-6b38e4a00f7a)

Again we have to move to higher level metal. So, again deposit SiO2 and do CMP. Then we do Photolithography to drill holes. Then deposit TiN

![image](https://github.com/user-attachments/assets/0842a973-ecf7-485c-852b-a0b112ec6193)

Then we deposit Blanket tungsten layer and then deposit slightly thicker Al.

![image](https://github.com/user-attachments/assets/2945403b-2575-4c25-bb20-0864d17d5062)

Then we deposit Si3N4 which is used to protect the chip. Here we use Mask-16 to drill and get the contacts outside the chip.

![image](https://github.com/user-attachments/assets/b026d0a5-cac9-42e8-a1fd-15d805521303)

This is the 16-Mask process.

![image](https://github.com/user-attachments/assets/ef12bd5c-bd32-4cc7-9e00-51c681b70512)

3.2.8.SKY_L8 - Lab introduction to Sky130 basic layers layout and LEF using inverter

![image](https://github.com/user-attachments/assets/f3aaad0f-85b8-4e27-9bcf-f83e8170fec8)

This is the layout of the CMOS inverter. Let us understand the layers first. The place where the cursor is placed is the local interconnect(local i) or the first layer.

![image](https://github.com/user-attachments/assets/f07ee9ed-90d9-4bf9-b908-5f3d8254ea65)

Then we have metal 1
![image](https://github.com/user-attachments/assets/825b411f-fad9-479c-aaa9-79a1912ee348)

Then we have metal 2 which is pinkish cross
![image](https://github.com/user-attachments/assets/65e3dcac-241b-476a-bb09-30fc5e7b36da)

Then we have N-well
![image](https://github.com/user-attachments/assets/f26a4a4f-7581-4382-864f-275faec8b953)

For n diffusion and p diffusion the colours are green and brown respectively. If we hover the cursor on the left side green color, we can see the caption on the top as n diffusion. When, the poly cross the n diffusion, it becomes the NMOS.
To confirm it, we can hover the cursor in the poly on the intersection of n diffusion layer, and click s. This selects the area. Then we can move to the tkon file and type 'what' and the result will be nmos.

![image](https://github.com/user-attachments/assets/fd022069-6098-4ea3-abc6-ffffd97edf0c)

To check whether the drain of the nmos and pmos is connected, we can hover over there and click 's' three times to see what are connected over there.

![image](https://github.com/user-attachments/assets/1771c18a-8256-42a6-9202-7dc78d9a0fb2)

Also, how to build a inverter form scratch is described in 'https://github.com/nickson-jose/vsdstdcelldesign'

3.2.9.SKY_L9 - Lab steps to create std cell layout and extract spice netlist

![image](https://github.com/user-attachments/assets/7ced32aa-7bfb-4f20-b62c-afe0b4b4a89e)

Here, inside the root cell box, llx-lower left x, urx-upper right x. Inside the FIXED_BBOX, (0 0 ) is the lower left corner value and the next value is upper right corner value.

![image](https://github.com/user-attachments/assets/ad021672-b376-41be-bf15-5e65067c8153)

The contact where the cursor is placed is the contact between the locali and metal 1.

![image](https://github.com/user-attachments/assets/1add0a6e-a14a-4e6a-bff6-9806392e571e)

The place where the cursor is placed is the contact between the locali and N-well.
Generally, for PMOS there is N-well and above that there is locali and above that there is metal 1.

Similarly, for nmos there is no well so, this contact is connected with the p-substrate and the locali.
![image](https://github.com/user-attachments/assets/f1e01bb7-7650-458e-9b50-89f93848957e)

Magic is an interactive window. If we erase a part from the layout as shown below, we can see the updated DRC value at the top. And if we need to see where the error is, go to DRC->DRC find next error.

![image](https://github.com/user-attachments/assets/f28afc3c-91f2-4749-8746-2d2eba999791)

If we need to know what is the error, after following the above steps, go to the tkcon window. We need to make sure that the final design should be DRC free.

We can reduce the error by selecting the error region and selecting the respective layer as shown below.
![image](https://github.com/user-attachments/assets/b9babffc-5413-4195-aacd-47474ff9e816)

![image](https://github.com/user-attachments/assets/74af334e-6ad4-4b89-bc30-6b512eea237e)

![image](https://github.com/user-attachments/assets/f9ef7fe4-70e8-49c2-92db-0323edac26da)

How do we know what is the logical functioning of this inverter?. To understand that, first we extract the spice and we do simulation on ngspice.
The extracted file is shown below.
![image](https://github.com/user-attachments/assets/ff598cb7-fc69-4189-a87e-fcec10f664af)

We will use this .ext file to create spice file for ngspice. 

Now the spice file is created.
![image](https://github.com/user-attachments/assets/81a400ce-60ac-43be-970c-9ba3af2a795b)

The spice file is shown below. It can be opened using 'vim sky...spice' command

![image](https://github.com/user-attachments/assets/9e3e9f09-2ad5-495d-b886-bdd7d7fbfeb5)

3.3.SKY130_D3_SK3 - Sky130 Tech File Labs
3.3.1.SKY_L1 - Lab steps to create final SPICE deck using Sky130 tech

The understanding of the spice file is shown below.

![image](https://github.com/user-attachments/assets/3beaaf20-78c9-45cb-9c05-eb56f5ef2d6d)

Now a pulse voltage is given as input to the gate(Va), Vss and Vdd.

![image](https://github.com/user-attachments/assets/61355075-f299-4634-8494-a1044a3a96f4)

![image](https://github.com/user-attachments/assets/d2127572-2174-429c-9b51-ebfc72c3198b)

![image](https://github.com/user-attachments/assets/9b98cfa0-b835-4d0b-8e12-e2ae95613a2a)

Here, we have included the libs file for nmos and pmos, Vdd, Vss, Va and finally we added the code for transient analysis. Also, we have changed the scale value by seeing the dimension of the lowest box in layout.
![image](https://github.com/user-attachments/assets/e3039577-969f-4aec-8e5e-1a3e99bd8d83)

Also there is a small change in the code. We modified the pshort to pshort_model and nshort to nshort_model after referring to the pshort and nshort file.
![image](https://github.com/user-attachments/assets/d33dc523-a5dc-4b67-a0ba-06f37dfce926)

Now the spice deck is ready. To run it, we can give the command, 'ngspice sky...spice' 

![image](https://github.com/user-attachments/assets/95494782-98aa-4806-9930-f0645f9bf18e)

3.3.2.SKY_L2 - Lab steps to characterize inverter using sky130 model files

![image](https://github.com/user-attachments/assets/501acd81-cbb6-4444-9e41-9890d72d4055)

 This the output we are getting for the transient analysis. Next we are going to do the characterization. For that we need to consider 4 parameters. 1. rise transition ie) the ability of the output waveform to transit form its 20% of max value to 80% of max value. Similarly, 2. Fall transition ie) the ability of the output waveform to fall form its 80% of max value to 20% of max value. We can find this delay by zooming into graph and clicking at the point. So that it will get printed on the plot terminal as shown below.
 ![image](https://github.com/user-attachments/assets/db74d300-7db2-4976-9308-478fec70f57a)

If find the difference between both the X values, we will get the rise transition. Similarly we can find the fall transition. 3. Cell rise delay. This can be calculated by the difference between the 50% of output wave to the 50% of input waveform. And it is shown below.

![image](https://github.com/user-attachments/assets/a43c3e58-7c77-4bcf-8437-95ba46423e87)

In the similar way we can calculate the Cell fall delay. These all things are done for a temperature of 27 degree celcius. In the next step, we are going to use the layout to create a lef file. And we try to add this inverter cell in picorv32 using openlane.

3.3.3.SKY_L3-Lab introduction to Magic tool options and DRC rules.

3.3.4.SKY_L4-Lab introduction to Sky 140 pdk's and steps to download labs.

This is the website where we find the documentation for the skywater pdks and it has design rules.

![image](https://github.com/user-attachments/assets/bb49e83d-fd8c-4814-98a0-b6834257ac95)

![image](https://github.com/user-attachments/assets/bb5d2daf-78c6-4486-8701-fa35554003d0)

![image](https://github.com/user-attachments/assets/40dbe46f-b96f-47fd-9dc7-1a14a09c0560)

3.3.5.SKY_L5 - Lab introduction to Magic and steps to load Sky130 tech-rules.

![image](https://github.com/user-attachments/assets/baee6778-0ea3-4d4b-9abf-355e31737eed)

3.3.6.SKY_L5-Lab exercise to fix poly.9 error in Sky130 tech-file.

Here the poly is loaded and there are errors present there. That has to be founded and corrected.

![image](https://github.com/user-attachments/assets/b139d5d7-fb98-45b8-ac70-a0f761e4b240)

Go to the sky130.tech file using the vim sky130.tech and find the 'poly.9' by typing '/poly.9' in the file and edit it as shown below. we have to edit in two places.

![image](https://github.com/user-attachments/assets/ec6d04f1-e05a-429d-9bc5-47c1deaede71)

![image](https://github.com/user-attachments/assets/138c05ee-0b19-4fbe-af5d-cbca93459b88)

Then use the command 'tech load sky130.tech' and then 'drc check' in the tkcon file to see the difference in the layout. Because there are errors in the layout, we do this to correct the errors. 

![image](https://github.com/user-attachments/assets/8145d649-844d-4588-b005-6115f069c478)

4.Sky130 Day 4 - Pre-layout timing analysis and importance of good clock tree
4.1.SKY130_D4_SK1 - Timing modelling using delay tables
4.1.4.SKY_L4 - Introduction to delay tables

<img width="960" alt="image" src="https://github.com/user-attachments/assets/dea6d934-7b0d-41b8-91fa-ffe62a7bc9d6" />

We can give clock inputs using these gates as shown in the diagram. How do we use this in the clock tree. A sample snippet of clock tree is shown in the diagram below. Here, a buffer is replaced with an AND gate for gated clock. While replacing we should consider parameters like skew, latency.... We have to consider all these things. First let us consider the timing parameters of the first circuit. We will come back to the second circuit later.

<img width="960" alt="image" src="https://github.com/user-attachments/assets/5d519ea5-b1a6-4b59-b790-07664af95395" />

The assumptions and observations are shown in the below figure. Why do we consider these observations?, because the load of each and every buffer will not be same so, the input to the buffer will also not be same. So, there are varying gusses. So, there is a concept called Delay tables.

<img width="960" alt="image" src="https://github.com/user-attachments/assets/9a1d6726-183a-4603-b1b0-9d691042c1ae" />

Let us take a buffer of size 1 as an example. The delay table is calculated by applying different input transitions and the output is also varied with different loads. S, with this varying input transitions and output load, the delay of that particular cell is characterized and put in a table form.

<img width="960" alt="image" src="https://github.com/user-attachments/assets/36519160-c1a2-40c2-8ee1-b8a867c9e177" />

Each cells with different size and different threshold voltage will have different delay table. In the above diagram, for a buffer of fixed size(1) and fixed threshold voltage, the delay table is given.

4.1.5.SKY_L5 - Delay table usage Part 1

<img width="960" alt="image" src="https://github.com/user-attachments/assets/a6e40ab2-b4f6-4ed7-88e3-3acb8029065e" />

Let us apply this concept in real circuits

![image](https://github.com/user-attachments/assets/76a9b217-f79d-45be-b904-1357702e0dbf)

Let us consider 40ps as input transition and assume 60fF as the output load. In the delay table, there is no 60fF, so we will use 50fF and 70fF which are closer to the 60fF to find the identity and solve to find the delay. Let us say the delay is x9'.
The objective is to find the delay or clock latency in the FF at the end. To do that we find the delay of individual elements.
