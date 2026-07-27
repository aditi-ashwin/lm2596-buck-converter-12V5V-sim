# LM2596 Buck Converter Simulation

## Overview
This project contains an LTspice simulation of a step-down converter using the LM2596 voltage regulator. The circuit steps down a 12V input to a 5V output. I completed this project to learn more about how LTSpice simulations are completed, and the different kinds of analysis that can be performed with a virtual simulation compared to a physical analysis.

## Circuit Design
* **Input Voltage:** 12V
* **Output Voltage:** 5V
* **Key Components:** LM2596 regulator, 38µH inductor, MBRS340 Schottky diode, 470µF input capacitor, 330µF output capacitor.
* **Testing Conditions:** I simulated steps through different load resistors (6.67Ω, 3.33Ω, 2.22Ω, and 1.67Ω). This tests the converter's performance at different output currents, all the way up to 3 Amps which was the specified current output.

## Schematic
<img width="975" height="493" alt="image" src="https://github.com/user-attachments/assets/cda6c286-9d06-41fc-9f96-00fee5a02d57" />

## Data and Results
### Initial Simulation

<img width="597" height="227" alt="image" src="https://github.com/user-attachments/assets/58e17638-5ebf-4f69-b588-16ffe02448ce" />

I first simulated the circuit against a resistance of 1.67 ohms to measure the output current at the expected 3 Amps. The green curve demonstrates the movement of voltage as the converter starts up, overshoots, and then balances at 5V, while the blue curve demonstrates the current output.

<img width="621" height="469" alt="image" src="https://github.com/user-attachments/assets/fc47b69d-37a5-4b44-a21f-b574706fb6ad" />

This zoomed in image of the current shows that it has a variation of about 0.5A, and stays under the 3.6 Amps that the components are rated for. The expected ripple current can be calculated using $$\frac{(V_{in} - V_{out})\cdotV_{out}}{V_{in}\cdotL\cdotf_{switching}}$$ which, when values are plugged in, comes to 0.511 Amps. This expected value matches the value acquired from the graph.

<img width="1894" height="434" alt="image" src="https://github.com/user-attachments/assets/960cee73-59df-4772-a02c-dbfba25c0ffb" />

This is the zoomed in image of the voltage, showing that it varies from 4.98V to 5V, demonstrating a stable output voltage.

### Inrush Current

<img width="681" height="223" alt="image" src="https://github.com/user-attachments/assets/93b13a18-18f6-4f22-88e3-668b7c854fe1" />

This graph corresponds to the inrush current simulation. To ensure that the inrush current did not exceed the current ratings of the power supply, inductor, diode, and LM2596, I measured the current at the power source as the simulation started up. Specifically for the inductor, many of the inductors listed on the TI datasheet for the chip are out of production, so I decided to simulate the Schott 67148400 (L34) Inductor and its specifications.

### Step Load

<img width="713" height="223" alt="image" src="https://github.com/user-attachments/assets/5754a07a-6ed5-488d-b3c4-3f91dbdcdd19" />

After ensuring that the circuit performed as expect, I stepped the load to determine its performance at different current draws. To measure at 25%, 50%, 75%, and 100% current draws, I used resistance values of 6.67 Ω, 3.33 Ω, 2.22 Ω, and 1.67 Ω, using .step param R_val list 6.67 3.33 2.22 1.67 to move through each. Each curve corresponds to a resistor value, with the highest peak belonging to the 6.67 Ω resistor. Its light load causes slower drain, meaning it peaks much higher before it is able to stabilize. However, it is still well under the voltage rating for each component.

### Average Input/Output Power and Efficiency

After measuring the different loads, I measured their efficiency based on power calculated from the voltages and currents coming in and out of each resistor.

<img width="1106" height="477" alt="image" src="https://github.com/user-attachments/assets/80e50989-50b2-4e68-b1a1-6a39ef03a5ed" />

The trend in the graph shows how increasing the load draw will decrease the efficiency as expected, but the efficiency is maintained at above about 89%. 


