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
