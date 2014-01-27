# L8 Homework

- [10.7] Can we apply the look-ahead output buffer for Mealy output?  Explain.
- [10.12] Non-return to-zero inverted (NRZI) code is a code used in some serial transmissions.  In the USB interpretation of this protocol, the output of an NRZI is flipped to transmit a '0' while the output does not change to transmit a '1'.  Assume the first input and output value is always zero.  For example, the NRZI encoded value of "00000001" is "01010011".
  1. Draw the Moore FSM state-transition diagram.
  2. Write the complete VHDL code to implement this NRZI as an FSM.  Use a look-ahead buffer for the output.

[**Side Note**: In the actual USB implementation, if there are six ones transmitted (i.e., the output value does not change for six cycles), an extra '0' is transmitted to ensure there are enough signal transitions for the receiver clock to remain synchronized.  Also, USB uses differential signaling, a concept we will discuss later in this course.]

## Turn-In Requirements

1. Answers to the above questions.
2. Simulation screenshots and source code where appropriate.
