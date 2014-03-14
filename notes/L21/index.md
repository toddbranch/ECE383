title = 'PicoBlaze and HW/SW Partitioning'

# Lesson 21 Notes

## Readings

- Review the KCPSM6 User Guide - inside the [PicoBlaze files zip](/datasheets/)
  - Reading manuals like this is great practice for the Final Project!

## Instructor Reference

- Saas, Chapter 4
- Chu (examples), Chapters 14 - 17

## Assignments

## Lesson Outline

- Admin
- Main Lesson
- Intro Final Project
- Walk Through HW

## Admin

### Lab Notes

**git Notes**

- You don't have to push often.  It's perfectly
  acceptable to commit many times locally between
pushes.
- `git diff <filename>`
  - Shows changes in file since last commit
  - Useful in determining what you should put in commit
    messages

### Go Over GR

- Average = 77%
- Main Issues
  - Problem 2 - translating VHDL to hardware
- Testing
  - Lots of small point losses added up
- FSM
  - This was the most important question to me
  - Most people did great!
  - If you struggled, we need to fix that!

## Main Lesson

PicoBlaze is an 8-bit CPU - how big was the MSP430?

PicoBlaze has no special purpose registers - was that true of the MSP430?

Implementation has two main components - the PicoBlaze core and a custom ROM containing your assembled code.  Generics allow for configuration.

Why 4k instructions?  Based on address size!  2^12 = 4096

In the files zip, the User Guide and `kcpsm6_design_template` both contain a ton of useful code to help you.

Our standard 100MHz `clk` will work fine with the PicoBlaze.

You're creating a ROM hardware component with your code.

Recommended to use 1K block size due to hardware on Spartan 6 FPGA.

Setting JTGA Loader to 1 helps you load modifications to your ROM much faster - only one chip can have this set at a time.

## Introduce Final Project

- Rough proposal by next lesson
  - **Add this to the HW**
- Final approved project lesson prior to Spring Break
  - L25?
  - So Mr. Evans can order parts
- Example projects / ideas
  - 
- Tour of the parts room

## Walk Through Homework

- Give students a break - has been a busy week
