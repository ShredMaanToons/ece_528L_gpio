# ECE 528/L - Robotics and Embedded Systems Lab
**CSU Northridge**

**Department of Electrical and Computer Engineering**

## GPIO Lab
### Thomas Anderson / 
---
<details><summary>The GPIO lab interfaces with the following:</summary>

* User buttons and LEDs of the TI MSP432 LaunchPad
* PMOD SWT (4 Slide Switches) - [Product Link](https://digilent.com/reference/pmod/pmodswt/start)
* PMOD 8LD (8 LEDs) - [Product Link](https://digilent.com/shop/pmod-8ld-eight-high-brightness-leds/)
</details>

<details>
<summary><h2>Introduction</h2></summary>

This lab serves as an introduction into general purpose input/output (<b>gpio</b>) and using the <b>pmod</b> components.    
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
2. Connect the PMOD SWT and PMOD 8LD to the MSP432 LaunchPad
3. Connect to computer and build then flash the program
4. Verify that the current build works then run a debugging session and observe how the registers are modified.
  * Screen shots of this step in "Screenshots" folder.
5. Exit debugging.

<b>Tasks</b>
1. Modify LED_pattern_1 by changing color for the RGB LED, adding a blinking function, and changing when the PMOD 8LD is active.
2. Create the LED_pattern_3 function by building a binary down counter.
3. Create the LED_pattern_4 function by building a ring counter.
4. Create the LED_pattern_5 function by building a ring counter that counts backwards.
5. Create the Johnson_Counter function by building a twisted ring counter.

<b>These steps were demonstrated in lab.</b>
</details>


<details>
<summary><h2>Conclusion</h2></summary>

text
</details>
