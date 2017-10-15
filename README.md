# Self-Protected-Output-Driver-with-Feedback

Note: Circuit simulation was done using LT Spice and source file is included.

To use this circuit, uC GPIO pin has to be configured as ouput and driven Lo in order to turn output On. Once output is turned on, uC GPIO pin is re-configured to "input" and used as feedback.
In case of output fault, circuit will shut off imidiately.

![Alt Text](/img/circuit.jpg)

### Operation:
So, when driven "Lo" by uC, Q1 will turn ON and Q2 will latch ON. 
Next, uC will re-configure pin to "input" (HiZ). At this point, uC can use this pin as a diagnostics feedback for the driver circuit. If voltage on the pin is approximately Vcc-Vce, circuit is working fine.
In case output is short to GND, base of Q2 is going to get current starved and Q2 will un-latch (turn off). THis will turn Q1 off. Now uC will read Vcc on the feedback line.
This way, single uC pin is used to drive the circuit as well as for diagnostics. Also, circuit is self protected.

![Alt Text](/img/simulation.jpg)

### Simulation:
Plot above shows at tize 0ms-100ms uC pin is pulled to Vcc, 5V in this case. Q1 is off and Vout is at 0V.
At time 100ms uC ouput is switched Lo (0V).In simulation, this is done turning ON Vsw_Lo. Q1 turns ON and Vout goes high (Vcc-Vce). 
At time 200ms, uC ouput pin is re-configured to input. In simulation this is done turning Off Vsw_Lo. At this point Q2 is latched ON and it keeps Q1 in ON state. uC input is at ~Vcc-0.7V and can be used as a feedback.
At time 350ms, short circuit is applied to output. This is done by switching Vsw_short ON.  Vout instantly goes to 0V. Q2 turns Off and so does Q1. uC input is now at Vcc and if used as feedback signals that circuit switched itself Off.

### Design:

