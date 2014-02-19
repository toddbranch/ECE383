title = 'Pong Review, Font Controller Introduction'

# Lesson 16 Notes

## Reading

## Assignments

- Lab 3 Prelab

## Lesson Outline

- Review Pong Lab
- Introduce Font Controller Lab
- Work Time

## Admin

- Today will be an easy day - a breather before the start of the next lab
  - We'll review the Pong lab
  - I'll intro the next lab (font controller)
  - I'll give you the rest of the time to work!

## Review Pong Lab

Things I noticed:

- Gigantic state machines
  - Break it into smaller machines and chain them together!
- Getting attached to early code
  - Your first crack at a problem is always going to suck - expect to rewrite it!
  - Rewriting bad code is much faster than hunting for that one bug that might fix everything
  - Arriving at a solution with well-written code makes it easier to add features
- Going for the "Home Run"
  - Trying to add in too many features before verifying that basic features work
  - When behavior issues might be due to multiple code issues, this becomes tough to debug!
- Trying to everything in `process` statements
  - Use combinational logic where it makes sense!
- Inferred memory
  - If you intend a `process` statement to be combinational, every input better be in your sensitivity list!
  - Set default values for everything being set within your `process`!

So, in capstone, if you're designing an embedded application that needs to implement a pong game on a large display, should you use an MCU or an FPGA?

YOU SHOULD USE AN MCU!

## Introduce Font Controller Lab

[Font Controller Lab](/labs/lab3)

**Discuss methods to infer block RAM.  `input_to_pulse`**

## Work Time

- Work on Pong writeup
- Clean up Pong code
- Work on Font Controller prelab
- Create Font Controller project, move applicable files over
