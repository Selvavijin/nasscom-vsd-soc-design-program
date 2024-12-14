Sky130 Day 1 - Inception of open-source EDA, OpenLANE and Sky130 PDK
  SKY130_D1_SK1 - How to talk to computers
    SKY_L1 - Introduction to QFN-48 Package, chip, pads, core, die and IPs

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
