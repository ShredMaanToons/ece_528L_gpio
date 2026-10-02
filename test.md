# ECE 528/L - Robotics and Embedded Systems Lab
**CSU Northridge**

**Department of Electrical and Computer Engineering**

## Lab 0: General Purpose Input Output (GPIO)
### Thomas Anderson / Abraham Santiago
---
<details><summary>The GPIO lab interfaces with the following:</summary>

* User buttons and LEDs of the TI MSP432 LaunchPad
* PMOD SWT (4 Slide Switches) - [Product Link](https://digilent.com/reference/pmod/pmodswt/start)
* PMOD 8LD (8 LEDs) - [Product Link](https://digilent.com/shop/pmod-8ld-eight-high-brightness-leds/)
</details>

<details>
<summary><h2>Overview</h2></summary>

This lab serves as an introduction into general purpose input/output (<b>gpio</b>) and using the <b>pmod</b> components to read the inputs from the switches and control the outputs of the LED.    
Additionally it introduces the methods to view the memories of registers while debugging.
</details>

<details>
<summary><h2>Components</h2></summary>
  
<b>Description</b> | <b>Quantity</b> | <b>Manufacture</b>
--- | --- | ---
MSP432 LaunchPad | 1 | Texas Instruments
USB-A to Micro-USB Cable | 1 | N/A
PMOD 8LD | 1 | Digilent
PMOD SWT | 1 | Digilent
</details>


<details>
<summary><h2>Theory</h2></summary>

<b>Key Concepts</b>
---

<details>
<summary><b>Active Low</b></summary>

The launchpad buttons are active low, meaning the pins they connect to will be set to 1 by default and only become 0 when the button is pressed.    
This requires that the internal resistors are activated as pull up resistors to ensure that the pins are in a known state when no external signal is connected.

<table>
    <tr>
      <td>⚠️ <b>Tip:</b> Button one is mapped to pin P1.1  Button two is mapped to pin P1.4</td>
    </tr>
  </table>

</details>

<details>
<summary><b>GPIO Initialization</b></summary>

To initialize general purpose input and output for a pin we must set multiple bits that are used to control the purpose of the pin.    
<b>First</b> we must set select 0 (<b>SEL0</b>) and select 1 (<b>SEL1</b>) registers in the port we want to use.    
When both of these are set to 0 the pin is as GPIO, but the direction still needs to be specified.    
<b>Second</b> we must set the direction (<b>DIR</b>) register, with 0 being input and 1 being output.    
<b>Finally</b> if we have an input we may need to enable pull up or pull down resistors.    
<b>REN</b> is the resistor enable register which enables the resistor if the bit is set to 1.    
<b>OUT</b> is the output register and when resistors are enabled setting the bit to 1 indicates pull up resistors and vice versa.
</details>

</details>


<details>
<summary><h2>Procedure</h2></summary>

<b>Pre-Task</b>
---
1. Copy repository using Git Bash
2. Connect the PMOD SWT and PMOD 8LD to the MSP432 LaunchPad using the following pin configuration
<details>
<summary><h2>Connections</h2></summary>

<b>PMOD SWT Pin</b> | <b>MSP432 LaunchPad Pin</b> 
--- | --- 
SWT1 | P10.0
SWT2 | P10.1
SWT3 | P10.2
SWT4 | P10.3
Pin 5 (GND) | GND
Pin 6 (VCC) | VCC (3.3V)

<b>PMOD 8LD Pin</b> | <b>MSP432 LaunchPad Pin</b> 
--- | --- 
LED0 | P9.0
LED1 | P9.1
LED2 | P9.2
LED3 | P9.3
Pin 5 (GND) | GND
Pin 6 (VCC) | VCC (3.3V)
LED4 | P9.4
LED5 | P9.5
LED6 | P9.6
LED7 | P9.7
Pin 11 (GND) | GND
Pin 12 (VCC) | VCC (3.3V)
</details>

3. Connect the MSP432 LaunchPad to the computer and build then flash the program
4. Verified that the current build works by testing the different Test Cases in the table below. The test cases test how the switches will affect the LEDs

<details>
<summary><h2>Cases</h2></summary>

<b>Test Case</b> | <b>Input</b> | <b>LED 1</b> | <b>RGB LED</b> |  <b>PMOD 8LD</b>
--- | --- | --- | --- | ---
0 | Button 1 is pressed | ON | OFF | LEDs 0-3: ON, LEDs 4-7: OFF
1 | Button 2 is pressed | OFF | GREEN | LEDs 0-3: OFF, LEDs 4-7: ON
2 | Both Button 1 and Button 2 are pressed | ON | GREEN | LEDs 0-7: ON
3 | Neither buttons are pressed | OFF | OFF | LEDs 0-7: OFF

When only SWT1 is enabled

<b>Test Case</b> | <b>Input</b> | <b>LED 1</b> | <b>RGB LED</b> |  <b>PMOD 8LD</b>
--- | --- | --- | --- | ---
0 | Only SWT1 is enabled | ON |RED | Binary Up Counter
</details>

5. Then run a debugging session and observe how the registers are modified.
  * Screen shots of this step in "Screenshots" folder.
6. Exit debugging.

<b>Tasks</b>
---
1. Modify LED_pattern_1 by changing color for the RGB LED, adding a blinking function, and changing when the PMOD 8LD is active.

<details>
<summary><h2>Cases</h2></summary>

<b>Test Case</b> | <b>Input</b> | <b>LED 1</b> | <b>RGB LED</b> |  <b>PMOD 8LD</b>
--- | --- | --- | --- | ---
0 | Button 1 is pressed | ON | OFF | LEDs 0,2,4,6: ON, LEDs 1,3,5,7: OFF
1 | Button 2 is pressed | OFF | BLUE | LEDs 0,2,4,6: OFF, LEDs 1,3,5,7: ON
2 | Both Button 1 and Button 2 are pressed | Toggle every 1 second | GREEN toggle every 1 second | LEDs 0-7: OFF
3 | Neither buttons are pressed | OFF | OFF | LEDs 0-7: ON
</details>

2. Create the LED_pattern_3 function by building a binary down counter.

<b>Test Case</b> | <b>Input</b> | <b>LED 1</b> | <b>RGB LED</b> |  <b>PMOD 8LD</b>
--- | --- | --- | --- | ---
0 | Only SWT2 is enabled | ON | BLUE | Binary Down Counter

3. Create the LED_pattern_4 function by building a ring counter.

<details>
<summary><h2>Cases</h2></summary>

<b>Iteration</b> | <b>LED 1</b> | <b>RGB LED</b> | <b>PMOD 8LD</b>
--- | --- | --- | ---
0 | OFF | OFF | 1
1 | OFF | OFF | 2
2 | OFF | OFF | 4
3 | OFF | OFF | 8
4 | OFF | OFF | 16
5 | OFF | OFF | 32
6 | OFF | OFF | 64
7 | OFF | OFF | 128
</details>

4. Create the LED_pattern_5 function by building a ring counter that counts backwards.

<details>
<summary><h2>Cases</h2></summary>

<b>Iteration</b> | <b>LED 1</b> | <b>RGB LED</b> | <b>PMOD 8LD</b>
--- | --- | --- | ---
0 | OFF | OFF | 128
1 | OFF | OFF | 64
2 | OFF | OFF | 32
3 | OFF | OFF | 16
4 | OFF | OFF | 8
5 | OFF | OFF | 4
6 | OFF | OFF | 2
7 | OFF | OFF | 1
</details>

5. Create the Johnson_Counter function by building a twisted ring counter.

<details>
<summary><h2>Cases</h2></summary>

<b>Iteration</b> | <b>LED 1</b> | <b>RGB LED</b> | <b>PMOD 8LD (Binary)</b>
--- | --- | --- | ---
0 | ON | GREEN | 0000_0000
1 | ON | GREEN | 0000_0001
2 | ON | GREEN | 0000_0011
3 | ON | GREEN | 0000_0111
4 | ON | GREEN | 0000_1111
5 | ON | GREEN | 0001_1111
6 | ON | GREEN | 0011_1111
7 | ON | GREEN | 0111_1111
8 | ON | GREEN | 1111_1111
9 | ON | GREEN | 1111_1110
10 | ON | GREEN | 1111_1100
11 | ON | GREEN | 1111_1000
12 | ON | GREEN | 1111_0000
13 | ON | GREEN | 1110_0000
14 | ON | GREEN | 1100_0000
15 | ON | GREEN | 1000_0000
0 (repeat) | ON | GREEN | 0000_0000 (repeat)
</details>

<b>These steps were demonstrated in lab.</b>
</details>

<details>
<summary><h2>Know Issues or Limitations</h2></summary>

We gained a thorough understanding of all the concepts in the lab and successfully demonstrated the entire lab working without bugs.    
<b>This lab was a complete success.</b>
</details>

<details>
<summary><h2>Author Contribution</h2></summary>

We both completed every component of the lab and worked on the report together.    
</details>

<details>
<summary><h2>References</h2></summary>

[MSP432P401R SimpleLink Microcontroller LaunchPad Development Kit User's Guide](https://docs.rs-online.com/3934/A700000006811369.pdf)

[MSP432P401R Datasheet](https://www.ti.com/lit/ds/slas826e/slas826e.pdf)

[Robot Systems Learning Kit (TI-RSLK) User Guide](https://www.ti.com/lit/pdf/sekp166)

[MSP432P4xx SimpleLink Microcontrollers Technical Reference Manual](https://web.archive.org/web/20200402132841/http:/www.ti.com/lit/ug/slau356i/slau356i.pdf)

[PMOD SWT Reference Manual](https://digilent.com/reference/pmod/pmodswt/reference-manual)

[PMOD LED Reference Manual](https://reference.digilentinc.com/reference/pmod/pmodled/reference-manual)

[PMOD 8LD Reference Manual](https://digilent.com/reference/pmod/pmod8ld/reference-manual)
</details>
