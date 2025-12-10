  # 10MHz Frequency Reference Distributor and 25MHz generator and distributor.

  ## Purpose
  
  This hardware project is intended for people posessing a 10MHz sinusoidal reference oscillator (GPS DO / Rubidium Source) 
  but require a 25MHz reference for use with an SDR (Adalm-Pluto) or LNB (modified Bulls-Eye).

  ## Implementation

  The circuit first converts the incoming sine-wave to a square-wave. A potentiometer allows to set the square-wave
  duty factor to 50%. This square-wave is then presented to 3 external outputs of which 1 is DC coupled. A 4th internal
  copy is then available internally to be connected to the input of an external 50MHz band-pass filter.
  The 50MHz sinusoidal output of this filter is then connected to the 50MHz input, that is once again transformed to a 
  square-wave and finally divided by 2 to generate 25MHz that is presented to 4 outputs of which 2 are DC coupled.
  
  The circuit also has an interface J6 for the required power supplies (+15V, +5V) for the FE-5650 Rb frequency standard.
  As the FE-5650 module uses a 9 pin Cannon D connector, a special flat-cable with on one side the DB9 F and on the other
  side a 2 x 7 header is needed. The pin correspondances are marked in a table on page 2 of the schematic.
  Note that pin 1 of either connector are aligned (connected).
  
  ## Mounting sequence and Commissioning
  
  ### Preparations
  1. Solder SMD parts on F-side and B-side **EXCEPT: power jumpers R10, R14, R22 and Edge-mount coax connectors**
  2. Solder through-hole parts: potentiometer R15 and U6 regulator
  ### Power-supply
  3. Connect VBUS to a 16V power-supply and while measuring (with a DVM) the voltage between TP_GND and TP_15V
     trim potentiometer R15 to obtain 15V.
  4. Solder through-hole parts: potentiometers R12, R17 and regulators U2, U3.
  5. Trim potentiometer R17 while measuring TP_P5V to get 5V
  6. Trim potentiometer R12 which measuring TP_P3V3 to get 3.3V
  7. Solder power jumpers: R10, R14 (+5V and +3.3V) and measure the current going into VBUS (IBUS) to be ~30mA.
  ### 10MHz distributor
  8. Solder Edge-mount SMA coax J1, J2, J3, J4, transistor Q1 and potentiometer R5.
  9. Inject 10MHz ~1.3Vpp in port 10MHz in (J4).
  9. With a DSO (Inputs high-Z) measure the signals at J1, J2 -> ~3.5Vpp AC and J3 -> ~3.5V DC (0 thru +3.5V)
  10. Trim R5 for 50% duty-factor (J1, J2 and J3) Note: V-bias at node C1, R6, R3 will be ~ +1.55V  
  ### 50MHz output
  11. Solder Edge-mount SMA coax J13, through-hole SMA coax: J5, J7, power jumper R22 (+15V, 50MHz gain stage), 
  transistor Q2 and potentiometer R23. 
  12. Connect a previously prepared BPF50 from port BPF50 in (J7) to BPF50 out (J5)
  13. With a DSO (Inputs high-Z) measure the signals on port MHz50 out (J13). -> 50MHz signal ~3.5Vpp AC
  14. Trim R23 for 50% duty-factor 
  ### 25MHz distributor
  15. Solder Edge-mount SMA coax : J9, J10, J11 and J12.
  16. With a DSO (Inputs high-Z) measure the signals on ports J9, J10: 25 MHz DC -> ~3.5V DC (0 thru +3.5V)
  17. With a DSO (Inputs high-Z) measure the signals on ports J11, J12: 25 MHz AC -> ~3.5V AC (50% duty-factor)
 
 Notes: 
  - At the level 17 test configuration IBUS ~0.2A at VBUS +16V
  - Regulator U3 will become hot (70°C) without any heatsink. This may be a good moment to add the heatsink.
  
  18. Connect a flat-cable to J6 and **before connecting the correct Rb reference (FE-5650)**, 
  measure the supply voltages on the DB9 connector.
	- Pin 1: +15V
	- Pin 2: Gnd +15V
	- Pin 4: +5V
	- Pin 5: Gnd +5V
  19. Power-down, connect the DB9 side of the flat-cable to the Rb reference, connect the Rb reference 10MHz output
  to J4 the 10MHz input.
  20. Power-up, check supplies, verify and if needed correct the 10MHz 50% duty-factor setting R5. 
  
  ## Trouble shooting
  - In case of no output on the 50MHz port, measure the DC voltages at the outputs of U4 (+3.4V) and U5 (+4.9V).
  If one of these is absent verify the solder joints of either L1 or L2.
 
  ## Issues with Rev 1.0.0 built 20251031
  - The SMA Edge-mount connector footprints have a greater ground pin spacing than the "standard" Edge-mount SMA
  connectors available. Nevertheless these connectors can be soldered in place, bridging the slight gap between
  the pads and the connector Gnd pins.
  - The TO92 footprint of transistors Q1, Q2 (2N2222) has pin numbering 1,2,3 instead of 3,2,1 (collector emitter swap).
  The workaround is to mount Q1 and Q2 with the flat side opposite to that on the serigraphie.
  - C21 is too close to J6, the 2 x 7 pin header, effectively falling underneath the header plastic. By first mounting
  C21 and then letting the header stick out sufficiently the connector and capacitor can cohabitate.
  - As the 39 nF capacitors are not in the standard series these were replaced by 47 nF capacitors.

  ## Notes
  1. The series terminated DC Coupled outputs are intended to be connected to high-Z (3.3V) logic level inputs.
     The AC Coupled outputs can be terminated in 50 Ohms, typically like when connected to a clock input of an SDR.
  2. The 6th order 50MHz filter is constructed using 3 side-coupled (LC) resonating circuits that yield a good quality factor.
     More details on the construction of this filter will follow soon.
