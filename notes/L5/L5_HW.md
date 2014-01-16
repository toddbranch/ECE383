# L5 Homework
- [5.1] Consider a circuit described by the following code segment:
  1. Describe the operation of this circuit.
  2. Does this circuit resemble any real physical component?

```vhdl
process (a)
begin
	q <= d;
end process;
```

- [5.2] Consider a circuit described by the following code segment:
  1. Describe the operation of this circuit.
  2. Draw the conceptual diagram of this circuit.

```vhdl
process (a, b)
begin
	if a = '1' then
		q <= b;
	end if;
end process;
```

- [5.3] Add an enable signal, en, to the 2-to-4 decoder discussed in Section 5.4.1.  When en is '1', the decoder functions as usual.  When en is '0', the decoder is disabled and the output becomes "0000".  Use an **if** statement to derive this circuit.
- [5.4] Add an enable signal, en, to the 2-to-4 decoder discussed in Section 5.4.1.  When en is '1', the decoder functions as usual.  When en is '0', the decoder is disabled and the output becomes "0000".  Use a **case** statement to derive the circuit.
- [5.10] Assume that `op` is a 2-bit signal with `std_logic_vector` data type.  Consider the following code segment:
  1. Draw the conceptual diagram.
  2. Rewrite the code using only concurrent conditional and selected signal assignment statements.

```vhdl
case op is
	when "00" =>
		y <= (others => '0');
	when "01" =>
		if (a > 0) then
			y <= a - 1;
		else
			y <= a + 1;
		end if;
	when others =>
		y <= a + b;
end case;
```

- [5.11] Consider the shift-left circuit discussed in Problem 4.6.  The inputs include `a`, which is an 8-bit signal to be shifted, and `ctrl`, which is a 3-bit signal specifying the amount to be shifted.  Both are with the `std_logic_vector` data type.  The output `y` is an 8-bit signal with the `std_logic_vector` data type.  Use any VHDL construct to implement this functionality.

## Turn-In Requirements

1. Answers to the above questions
2. Simulation screenshots and source code where appropriate.
