  # 10MHz Frequency Reference Distributor and 25MHz generator and distributor.

  ## Purpose
  
  This hardware project is intended for people posessing a 10MHz sinusoidal reference oscillator (GPS DO / Rubidium Source) 
  that require a 25MHz reference for use with an SDR (Adalm-Pluto) or LNB (modified Bulls-Eye).

  ## Implementation

  The circuit first converts the incoming sine-wave to a square-wave. A potentiometer allows to set the square-wave
  duty factor to 50%. This square-wave is then presented to 3 external outputs of which 1 is DC coupled. A 4th internal
  copy is then available internally to be connected to the input of an external 50MHz band-pass filter.
  The 50MHz sinusoidal output of this filter is then connected to the 50MHz input, that is once again transformed to a 
  square-wave and finally divided by 2 to generate 25MHz that is presented to 4 outputs of which 2 are DC coupled.

  ## Notes
  1. The series terminated DC Coupled outputs are intended to be connected to high-Z (3.3V) logic level inputs.
     The AC Coupled outputs can be terminated in 50 Ohms, typically like when connected to a clock input of an SDR.
  2. The 6th order 50MHz filter is constructed using 3 side-coupled (LC) resonating circuits that yield a good quality factor.
     More details on the construction of this filter will follow soon.
