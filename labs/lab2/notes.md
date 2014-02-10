# Lab 2 Teaching Notes

This is a fun lab!  Unlike last lab where it either works or it doesn't, this lab allows you to make a lot of visible, incremental progress.  Here's the approach I took:

1. Copy your necessary Lab 1 files over to your Lab 2 project.  Ensure it generates the correct bit file.
2. Alter your `pixel_gen` module to draw the static AF on the screen.
  - Bear in mind that the ball must path underneath the AF logo.
3. Draw the paddle and ball.
  - Modify your `pixel_gen` to the entity declaration given in the lab writeup - have it paint the paddle and ball based on the passed in `paddle_y`, `ball_x`, and `ball_y`.
  - Create your `pong_control` module - have it pass out a static `paddle_y`, `ball_x`, and `ball_y`.
  - Ensure your code draws these elements to the screen properly.
  - It's a great idea to create a `constants` package - there are values you'll need to share between these modules!
4. Move your paddle in response to button pushes.
  - Modify your `atlys_lab_video` top-level and constraints file to take in button pushes from the board.
  - Modify `pong_control` to move the paddle on button push
    - Depending on your desired button functionality, you may have to debounce and prevent a held button from moving the paddle continuously.
    - Don't let players move the paddle off of the screen!
  - Ensure your code moves the paddle properly.
5. Write code to make your ball move.
  - My initial test let the ball bounce off of all screen edges, just to test that it worked properly.
  - It might be useful to separate the code that determines ball velocity from the code that updates ball position.
  - The screen updates quickly!  You shouldn't update ball position on every screen refresh.
  - `ball_x` and `ball_y` are unsigned - if you make velocity signed, this math might be tricky!
  - Make sure you handle edge conditions cleanly - you don't want your ball getting stuck on the edge of the screen!
6. Make the ball bounce off your paddle.
7. Make the ball freeze when it hits the left edge of the screen.
8. Implement bonus functionality, if you have time.  B can be implemented within a few minutes if your code is structured like mine.

A good schedule:

- Day 1 - task 1-3
- Day 2 - task 4-5
- Day 3 - task 6-7, bonus functionality
