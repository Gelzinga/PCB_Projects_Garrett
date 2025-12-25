###### THIS IS THE READ ME FOR THE RECEIVER BOARD #######



This board is a receiver for a laser tag project. The circuit is built with two op-amps with active filtering. The low pass filters are implimented using a series capacitor and resistor, and the high pass filters 
with the Gain bandwidth product property of the OP-AMP. The circuit attenuates high and low noise frequencies and provides around 160 dB of gain to the desired current domain signal genererated through the photdiode. Expected noise frequencies of 100 Hz and 10k hz. Circuit provides more than enough attenuation for noise signals, around 60 dB. 


Design Choices 
1. Capacitors were placed close to the power rails in order to achieve effective stabilization of power supply. 
2. Additional low pass filter was placed on power supply to eliminate higher frequency noise directly from the power.
3. Gain bandwidth property of opamp was used for high frequency noise attenuation to reduce compenents/complexity/poles of the circuit.
4. Gain around 160 dB in order to provide a useful signal. Attenuation of expected noise signals around 60 dB down. Bode plot is included in the PCB folder.
5. Ground was made a plane to reduce noise
6. Two inverting OP-AMPS were used. More OP-AMPS could've been used to increase gain, but for lower complexity and cost just two were used. 


Debugging Process
1. Major challenge was fitting all of the components in the board. Several vias had to be used
2. LT Spice schematic was used to verify appropriate attenuation of signals.
3. Included hardware support for extra filters for more attenuation if needed. Pins were used that can be bypassed with header caps. 
   
