# Self-Protected-Output-Driver-with-Feedback

Note: Circuit simulation was done using LT Spice and source file is included.

To use this circuit, uC GPIO pin has to be configured as ouput and driven Lo in order to turn output On. Once output is turned on, uC GPIO pin is re-configured to "input" and used as feedback.
In case of output fault, circuit will shut off imidiately.

![Alt Text](/img/circuit.jpg)

### Operation:
So, when driven "Lo" by uC, Q1 will turn ON and Q2 will latch ON. 
Next, uC will re-configure pin to "input" (HiZ). At this point, uC can use this pin as a diagnostics feedback for the driver circuit. If voltage on the pin is approximately Vcc-Vce, circuit is working fine.
In case output is short to GND, base of Q2 is going to get current starved and Q2 will un-latch (turn off). THis will turn Q1 off. Now uC will read Vcc on the feedback line.
This way, single uC pin is used to drive the circuit as we as for diagnostics. Also, circuit is self protected.

![Alt Text](/img/simulation.jpg)

### Simulation:

### Design:

