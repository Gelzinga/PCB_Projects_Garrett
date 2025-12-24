#### THIS IS THE READ ME FILE FOR THE IOT BOARD #####

In this folder you will find 

- Schematics 
- PCB pictures 
- KiCad files


Motivation for this board: 
This board is designed as a custom IOT device to read a digital output from a load cell ( Analog values already converted using off-board PCB) and display the value on a screen, 
indicating that more or less ingredients from the recipe sent from phone to the esp32 need to be included. Will make cooking easier and more convenient. 


Design Decisions: 
1. Multiple decoupling capacitors, each with different values to block low high, low and midband frequency noise. Decoupling capacitors were placed at several stages, but most noteably the raw input from the power supply.
2. Decoupling capacitors were placed close to the power/ground pins that they are connected to in order to further reduce noise (low noise is an absolute esssential, as the power supply must be  extremely stable
to get accurate readings from the load cell).
3. Buck converter was implimented to convert the 5v to 3.3v. The converter holds the voltage at .8 V at FB pin, so a resistor divider with high value resistors (to reduce power loss) was used. Values of 312.5k  and 100k achieve necessary 3.3v.
5. Ground was implimented as a plane to reduce potential sources of noise
6. Hardware support for a button was added, using an external pull up resistor for clarity as well as clean design. Large R values to reduce current power consumption 
7. Hardware support for SPI screen was included as well, to display the scale readings/progress.

Debugging process: 
1. Appropriate spacing to ensure proximity of capacitors to rails while still allowing for reasonable space for soldering and placement was a major problem.It required moving traces and footprints around, implimenting vias and using traces on both sides.
2. ESP 32 S3 footprint straight from the library had some vias that were .2 mm, changed to .3 mm for fabrication plausability/compatibility
3. Buck converter comes as an SMD, so this complicated things as either vias had to be made or priority for top-side traces.
4. Resistors were changed from SMD to THT for prototyping and less complexity/crowded traces on the front side. SMD technology to be explored in later iterations.
