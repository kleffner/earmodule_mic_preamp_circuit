# Ear Module Mic Pre-Amp Circuit
* Author: Matt Kleffner
* License: CC BY-SA 4.0 or Later

# Requirements:
* Interface hearing-aid mems microphones to sound card
* Low power
* Low noise, less than or equal to EIN of mic
* High-impedance interface
  * Mic output impedance on the order of 5 kOhm
* 100 Ohm output to drive high-impendance sound cards
* Single-ended input
* Differential output
* 1V Mic-bias supply needed
* Bi-polar AA power supply, +/- 3.2V, operate down to +/- 2V
* Op-amps provide clean 3.5V swing at +/- 2V supply

# Filter Gain Requirements
* Typical mic sensitivity is -38 dB re 1V/Pa or approx. 0.0125 V/Pa
* 120 dB is 20 Pa (10^(120/20)*20e-6)
* Mic output voltage at 120 dB is 20 Pa * 0.0125 V/Pa = 250 mV
* Gain for 120 V -> 3.5 V is 3.5/.250 = 14
* Allow for overshoot and set gain to 7
* Set input impedance to 20K, which is feedback impedance of 140K
  * Higher input impedances could increase circuit noise
* Mic output voltage will be scaled to approx 20/(20+5) or 20% reduction
* Match resistance seen on both + and - terminals
* 20K//140K = 17.5K - not available, but lots of 17.4K and 100 are

# Filter Cutoff Requirements
* Cost-effective, tight tolerances are 0.1% resistors, 5% capacitors
* Low cutoff < 20Hz, including tolerances
  * R = 20K, C=0.47e-6 gives (min,nom,max) cutoff of (16.1, 16.9, 17.8) Hz
* High cutoff > 20kHz, including tolerances
  * R = 140K, C=51pF gives (min,nom,max) cutoff of (21.2, 22.3, 2.35) kHz

# Op-amp selection
* Input stage
  * Implements filter
  * Low-noise
  * Low output impedance
  * Candidates
    * ADA4807
    * ADA4177
    * ADA4661 seems to be the best selection for the constraints

* Differential output stage
  * Requirements:
  * Unity-gain
  * Single-to-differential operation
  * Built-in over-voltage protection
  * Low-noise
  * Accurate differential-input impedance
  * Use ADA8476
    * Matched to <0.05% error
    * Protection to over 18V 

# Voltage regulator
* Low-noise
* Low component count
* TPS7A2010 Looks good but doesn't seem available in desired package
* TLV71210 is close, use it
