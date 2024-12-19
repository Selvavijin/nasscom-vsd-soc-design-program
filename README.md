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
