# L6 Homework

1. Write an entity and architecture for a decade counter (i.e., it counts from 0 to 9 before rolling over to 0 again).  Be sure to include the following signals `clk`, `reset` (back to 0), `en` (enable signal), and `q` (output).
  1. `q` should be of type `std_logic`, asserted when the counter rolls over
  2. The count should only increment on the rising edge of `clk` 2. Write a testbench for the decade counter.  Be sure to use the methods discussed in lecture.
  3. `reset` should be asynchronous
3. Once you have taken screenshots and documented your above design works, change your test vectors for the testbenches so that there are at least two failures.  Take a screenshot of the console output that shows the descriptive errors your testbench generates.

## Turn-In Requirements

1. Answers to the above questions
2. Simulation screenshots and source code where appropriate.
