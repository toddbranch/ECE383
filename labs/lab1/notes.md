# Lab 1 Teaching Notes

- Demo Atlys setup and programming
  - Plug in power supply
  - Plug in USB (to program it)
  - Show class HDMI to DVI cables
  - Demo programming via Adept
  - Show finished result

**Talk about prelab:**

- What does a state machine circuit look like?
  - Contrast Moore and Mealy
  - Strongly encourage students to treat each circuit entity separately
  - Label internal signals
- Talk about `count_reg` and `count_next`
  - How do you know when to transition between states?
  - You need a count - treat that as another input to your state machine
    - Draw on board
  - How do you know when to reset count?
- Talk about `completed` signal
  - Single cycle pulse set in last cycle of `back_porch`

If you try to write all of the code, then synthesize and hope for the best - you're going to have a bad time.  Use testbenches!  Focus on the signal transitions!

I'm grading you on use of git!  Only check-in the key files that you're changing
