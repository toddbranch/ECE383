title = 'VGA Lab Review, Pong Lab Introduction'

# Lesson 8 Notes

## Reading

- [Why are inferred latches bad?](http://electronics.stackexchange.com/questions/38645/why-are-inferred-latches-bad)

## Assignments

- Lab 2 Prelab

## Lesson Outline

- Review VGA Lab
- Introduce Pong Lab
- Work Time

## Review VGA Lab

### Lessons Learned

- Be disciplined in how you write code
  - Just because it simulates doesn't mean it will synthesize (Kevin)
    - Work-around may be to change synthesis to target area over speed, but this should be a red flag your code is difficult for the synthesizer to interpret
  - Draw picture, show my code, trace each block to picture
- Timing is critical!
  - Even being off by one is too much
- The simulator isn't always right
  - But it's way faster than synthesizing!
  - Understand the limitations and requirements of the simulator
- Mind your code style
  - `rising_edge(clk)` is better than `clk'event and clk=1`
  - Setting defaults is better than specifying values every time
    - `if` statements
    - `case` statements
  - Mind your spacing and indentation!
  - Well-written code over comments!
    - But use comments to describe the purpose of blocks of code
  - Use constants!
  - Use naturals / integers over binary!
  - Use `(others => '0')` or `(others => '1')` syntax
- Don't get attached to bad code!
  - If your understanding of the problem changes, rewrite it!
  - Too much time gets wasted in thinking "I can fix this if I just add one here or subtract one there"
- Don't just copy the book!
  - Know why you're doing what you're doing (FFs, lookahead buffers, etc)
- Don't be creative with code!
  - The synthesizer isn't that smart
  - Writing clear, simple code helps it help you

So, in capstone, if you're designing an embedded application that needs to drive a large display, should you use an MCU or FPGA?

YOU SHOULD USE AN MCU!!! A more powerful one than the MSP430, but an MCU nonetheless. FPGAs are good for applications that absolutely must be high-speed, low-power. Or you need flexibility in peripherals or need custom peripherals.  Putting embedded linux on an MCU and using their device driver libraries would be a much better choice both cost and ease-of-development-wise if you wanted to do something like this in CAPSTONE.

### Ways to Clean Up Lab 1
 
- Use generics
  - You may want to change display resolution in future labs
- Add constants
- Improve your testbenches
  - So you know if anything goes wrong in the future
- Implement look-ahead buffers (moore)
  - To prevent glitches!
- Improve code style
- Finish up your readme

## Introduce Pong Lab

[Pong Lab](/labs/lab2)

## Work Time

- Work on VGA writeup
- Clean up VGA code
- Work on pong prelab
- Create pong project, move applicable files over
