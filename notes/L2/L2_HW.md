# Lesson 2 Homework

1. [2.1] What are the syntax and semantics of a programming language?
2. [2.2] List three major differences between an HDL and a traditional programming language, such as C.
3. [2.3] In a traditional language, such as C, we can write the statement a = !a, and in VHDL, we can write a concurrent statement as a `<= not a after 10 ns;`.
  a. Draw the circuit diagram for the VHDL statement.
  b. Describe the operation of the circuit in part (a).
  c. Discuss the differences between the VHDL and C statements.
4. [2.5] For the VHDL code shown below, treat each concurrent statement as a circuit part and draw the conceptual block diagram accordingly.
```vhdl
  y <= e1 and e0;
  e0 <= (a0 and b0) or ((not a0) and (not b0));
  e1 <= (a1 and b1) or ((not a1) and (not b1));
```
5. [2.7] The VHDL structural description of a circuit is shown below [see textbook]. Derive the block diagram according to the code. 
6. [2.8] From the description of the VHDL process in Section 2.2.3, discuss the difference between the VHDL process and the traditional programming languages' procedure and function.
7. [2.11] Explain why VHDL treats the entity declaration and architecture body as two separate design units.
8. Send a pull request to add a link to your Github account to the ECE383-student-accounts repo: https://github.com/toddbranch/ECE383-student-accounts

## Turn-In Requirements

1. Answers to the above questions

2. Note: **All** hard-copy or electronic-copy assignment submissions in this class must have the following: Simulation screenshots and **syntax highlighted** source code where appropriate.
