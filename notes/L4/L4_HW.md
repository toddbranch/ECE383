# L4 Homework

- [4.1] Add an enable signal, en, to a 2-to-4 decoder. When `en` is '1', the decoder functions as usual. When `en` is '0', the decoder is disabled and output becomes "0000". Use the conditional signal assignment statement to derive this circuit. Draw the conceptual diagram.
- [4.2] Repeat Problem 4.1, but use the selected signal assignment statement instead.
- [4.3] Consider a 2-by-2 switch. It has two input data ports, x(0) and x(1), and a 2-bit control signal, ctrl. The input data are routed to output ports y(0) and y(1) according to the ctrl signal. The function table is specified below.
  1. Use concurrent signal assignment statements to derive the circuit.

| ctrl | y1 | y0 | Function |
| :-: | :-: | :-: | :-: |
| 00 | x1 | x0 | Pass |
| 01 | x0 | x1 | Cross |
| 10 | x0 | x0 | Broadcast x0 |
| 11 | x1 | x1 | Broadcast x1 |

- [4.4] Consider a comparator with two 8-bit inputs, `a` and `b`. The `a` and `b` are with the `std_logic_vector` data type and are interpreted as unsigned integers. The comparator has an output, `agtb`, which is asserted when `a` is greater than `b`. Assume that only a single-bit comparator is supported by synthesis software. Derive the circuit with concurrent signal assignment statement(s).
- [4.5] Repeat Problem 4.4, but assume that `a` and `b` are interpreted as signed integers.

## Turn-In Requirements

1. Answers to the above questions.
2. Simulation screenshots and source code where appropriate.
