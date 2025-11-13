## INTERFACING-OF-STEPPER-MOTOR-WITH-ARM-PROCESSOR.
# Aim :
To write an Embedded C program to interface a Stepper Motor with ARM processor LPC1768 using Keil MicroVision IDE.
# Components Required :
# HARDWARE:
ARM LPC1768 Development Board ,
Stepper Motor (4-phase, unipolar or bipolar type) ,
ULN2003 or L293D Motor Driver IC ,
12V DC Power Supply ,
Connecting Wires .
# SOFTWARE:
Keil µVision 4.0 IDE , 
Flash Magic (for code dumping) .
# PROCEDURE:
⮚	Open the Keil software and select the New uvision project from Project Menu as shown below.
⮚	Browse to your project folder and provide the project name and click on save.

⮚	Once the project is saved a new pop up “Select Device for Target” opens, Select the controller (NXP: LPC1768) from NXP (founded by philips) and click on OK.
⮚	Select the controller (NXP: LPC1768) and click on OK.

⮚	As LPC1768 needs the startup code, click on Yes option to include the LPC17xx Startup file.

⮚	Create a new file by file → new to write the program.
 
⮚	Type the code.

⮚	After typing the code save the file as main.c eg. (abc.c).

⮚	Right click target and Add the suitable files to source group1 and header for the project.

⮚	Add the main.c along with system_LPC17xx.c.

⮚	Build the project and fix the compiler errors/warnings if any.

⮚	Code is compiled with no errors. The .bin file is still not generated.

⮚	Right Click on Target Options to select the option for generating .bin file.

⮚	Set IROM1 start address as 0x2000. Bootloader will be stored from 0x0000-0x2000 so application should start from 0x2000
⮚	Write	the	command	to	generate	the .bin file	from
.axf file
Command: fromelf --bin projectname.axf --output filename.bin
⮚	in c/c++ → include paths → desktop (00-libfiles).
⮚	.Bin file is generated after a rebuild.
⮚	Check the project folder for the generated .Bin file. 

# ADD FILES :
Target1:

Source group1:

Startuplpc17xx.s, main.c (t), delay.c (t), systemlpc17xx.c (t), gpio.c (t)

Header:

Delay.h, stdutils.h, gpioi.h

# PIN DIAGRAM :
<img width="508" height="691" alt="image" src="https://github.com/user-attachments/assets/249accd4-89c5-4ed2-8c0b-e87ac89d8a08" />
<img width="427" height="355" alt="image" src="https://github.com/user-attachments/assets/f41864e5-cc55-47b7-abf5-7c3cadd117bd" />

# CIRCUIT DIAGRAM :
<img width="533" height="364" alt="image" src="https://github.com/user-attachments/assets/d168a178-61c1-4fba-8335-c2cdd9bb97f5" />

# PROGRAM :
```
#include<lpc17xx.h>
#include "gpio.h"
#define pin1 20
#define pin2 21
#define pin3 22
#define pin4 23
#define control LPC_GPIO1
-
>FIOPIN
void cmotor1() {
control |=(1<<pin1);
control |=(1<<pin2);
control &=~(1<<pin3);
control &=~(1<<pin4);
}
void cmotor2() {
control &=~(1<<pin1);
control |=(1<<pin2);
control |=(1<<pin3);
control &=~(1<<pin4);
}
void cmotor3() {
control &=~(1<<pin1);
control &=~(1<<pin2);
control |=(1<<pin3);
control |=(1<<pin4);
29
}
void cmotor4() {
control |=(1<<pin1);
control &=~(1<<pin2);
control &=~(1<<pin3);
control |=(1<<pin4);
}
void delay_ms(unsigned int ms) {
unsigned int i,j;
for(i=0;i<ms;i++)
for(j=0;j<20000;j++);
}
int main() {
SystemInit();
//Clock and PLL configuration
LPC_PINCON
->PINSEL3 =
0x000000;
LPC_GPIO1
->FIODIR
=(1<<pin1)|(1<<pin2)|(1<<pin3) | (1<<pin4);
while(1) {
cmotor1();
delay_ms(50);
cmotor2();
delay_ms(50);
cmotor3();
delay_ms(50);
cmotor4();
delay_ms(50); }
}
```
# OUTPUT :

![WhatsApp Image 2025-11-11 at 13 25 47_313b70ef](https://github.com/user-attachments/assets/67fbb586-16be-4ac2-8776-a12180d9abd1)
The stepper motor rotates step by step in the forward direction, showing successful interfacing with the ARM LPC1768 processor.
https://github.com/user-attachments/assets/cf3942a0-7b5b-4b41-af3d-584a615e064b

# Result :
Thus, an Embedded C program was written and executed to interface a Stepper Motor with ARM LPC1768 processor successfully.



