# L21 Homework

- Suppose that you profile a system and find that a certain function takes up 24% of the execution time.  What is the theoretical maximum speedup you can achieve with a hardware accelerator?
- List two advantages of using hardware and two advantages of using software to implement any given function.
- Write, simulate, and implement a PicoBlaze-based system that does the following:
  1. Reads in the value of the Atlys switches from Port 0xAF and stores the value in an internal register
  2. Reads in the value of the Atlys push buttons from Port 0xBC and stores the value in an internal register
  3. Writes the XOR of the push buttons and switches to Port 0x07, which in turn displays the value on the Atlys LEDs.
  4. Keeps repeating the previous three steps
  5. Note: You must use registers to handle the input/output ports (see slides).
- Imagine you had to develop an advanced version of Pong that met the below requirements.  Draw a decomposition diagram and recommend which portions should be implemented in hardware and which should be implemented in software.  Explain why.
  1. Rasterized graphics
  2. Add a picture to the background
  3. Add the ability to display text scores on the screen
  4. Have an overall game menu to start a new game, display high scores, or exit
  5. Randomly scroll barriers across the screen as obstacles the ball has to dodge.
- Draft your final project proposal
  - What's the general idea of your project?
    - Required Functionality
    - B Functionality
    - A Functionality
  - What hardware will you need?
    - Specify whether it's available in the department
      or not
    - How much will it cost?
  - Draft a rough timeline
    - You have seven lessons to complete the project
    - Detail how long you think you'll need for each
      project element

## Turn-In Requirements

1. Answers to the above questions
2. Simulation screenshots and source code where appropriate.
