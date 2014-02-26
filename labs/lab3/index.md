# Lab 3 - Font Controller

## Lab Overview

In the lab, you will develop a simple font controller for the VGA controller you previously created.  Your controller will allow a user to write a character to any location within a 30 character by 80 character grid on the screen.

## Font Controller Overview

In order to implement the font controller, you will need to create the below three modules.  Example VHDL entity declarations for these modules are provided in the Free Code section.

1. **Font ROM** - A "look-up table" that contains the 127 different characters that we are able to display on the screen.  An example 8x16 character is provided in Figure 1.  This module is provided for you on the course website.
2. **Screen Character Buffer** - 2400 (80 columns, 30 rows - based on a 640x480 screen resolution) character buffer that stores the character to display at each location on the screen.  The memory structure you will implement is shown in Figure 2.  To implement this module, you infer block RAM as shown in the XST User Guide (located on the [datasheets page](/datasheets).  The following definitions are helpful to interpret the terminology on Figure 3, i.e. how to structurally connect the screen buffer to the other signals in the character generator.
  1. `address_a`, `data_out_a`, `data_in` - used as a write port in the latter part of the lab when we will write new values to incrementing (internal_count) locations based on button presses
  2. `address_b`, `data_out_b` - used to read ASCII character in one of the 80 x 30 total memory locations in the RAM.  This is a continual process which is updated based on the current pixel's row and column
  3. f(row, column) - a combinational statement that calculates the ASCII character we are returning.  (e.g., row = 20, col = 5, retrieves the RAM location 80).  This is very similar to 2D array math, but you ignore the lowest 3/4 bits for column/row.
3. **Character Generation Controller** - This module takes in the current VGA row/column and outputs one RGB pixel based on whether or not that pixel is part of a font character.  To simplify the logic needed, the fonts are 8x16 pixels.  Most of the structure and logic is given to you in Figure 3.
4. **Top Level Design** - Connects `character_gen`, `input_to_pulse`, `vga_sync`, and the DCM together.  You will also need to add registers to delay the VGA signals to account for the pipeline delays within the character generation controller.

![Figure 1](figure1.jpg)

**Figure 1**: Example font 8x16 pixel character that is stored in the font ROM.  For clarity, only the "1" values are shown in this diagram.  In the actual hardware implementation, all the blank memory bits are "0"s.

![Figure 2](figure2.jpg)

**Figure 2**: Screen character buffer memory addresses for the characters that are displayed on the screen.  Each memory address contains the 7-bit pseudo-ASCII value that is used to look up the pixel data in the font ROM.  You will need to generate these addresses based on the current row and column from the VGA controller.

## Prelab Assignment

On the first day of the lab, turn in a typed hard copy the following items [Note: each number corresponds to a label in Figure 3]:

1. What is the purpose of the registers?
2. What is the purpose of the font ROM?
3. What does `data[7:0]` represent?
4. In what order should `row[3:0]` and `data_out_b[7:0]` be concatenated?  Why?
5. Which `data[7:0]` bit should be returned for each of the following column values:
  1. `column[2:0]` = "000"
  2. `column[2:0]` = "001"
  3. `column[2:0]` = "010"
  4. `column[2:0]` = "011"
  5. `column[2:0]` = "100"
  6. `column[2:0]` = "101"
  7. `column[2:0]` = "110"
  8. `column[2:0]` = "111"

Also, you must turn in the VHDL code and simulation results for your completed `input_to_pulse` module, as described in the next section.  Do not underestimate this task!  In the past, many students never were able to get a fully functional `input_to_pulse` module.

## Hardware Implementation

The core logic of your implementation will be contained within the `character_gen` module.  It takes in the current row/column and outputs the RGB value to the VGA screen.

For a given pixel row and column you can calculate the address needed to input to the character screen buffer.  The output of the screen buffer will be used to lookup that character in the font ROM.  The lower four bits of the row address determine which row of the font character to look up and display.  The lower three bits of the column data can be used to determine which column of the font character to display.  A graphical depiction of this process is available in Figure 3.

![Figure 3](figure3.jpg)

**Figure 3**: Example internal diagram for the `character_gen` module.

## B Functionality

To test your character generation control module in hardware, you should use switches as input and a push button to tell the controller to write the switch ASCII character into the screen character buffer.  In order to make this work, you should create an `input_to_pulse` module that takes a button press and generates a logic high signal for exactly one clock cycle.  This module must also debounce the input.  The debounce feature is usually implemented by using a shift register to store the last n input values.  When the shift register contains all logic high values, then the output will pulse high for one clock cycle.  Use an FSM to keep track of which state the `input_to_pulse` module is in.  Note that you will need to shift the shift register about once every 1 ms, not once every clock cycle.

## A Functionality

Interface with an NES controller to take input from the user!

![NES Controller](NES-controller.jpg)

**Figure 4**: The classic NES controller!

Users pressing the up / down arrows should scroll through available characters.  Users pressing left / right arrows should move cursor location.

I've given you code to drive the NES in Code Listing 3.  You'll need to interface this into your code to be successful!  You'll also have to connect the necessary driver signals to the NES through GPIO.  Here's the pinout for the custom connectors Mr. Evans built:

Controller pinout (**silver paint mark on one side is reference**):

1. Vcc (silver mark)
2. Data
3. Latch
4. Clk
5. Gnd

## Lab Hints

- In this lab you will be creating inferred block RAM.  Use the "Dual-Port RAM With Synchronous Read (Read Through) VHDL Coding Example" provided in the Xilinx XST User Guide to help you.
  - The XST user guide also explains how to initialize the memory.
  - Check your synthesis output log to check if the XST synthesizer correctly inferred the RAM.
- Since the `rgb_pixel` signal is delayed two clock cycles, you will need to pipeline (i.e., add registers) to your other VGA signals in your top-level design.
  - **WARNING:** If you delay in your top-level, you should delay off of
    `pixel_clk`, not `clk`!
  - This error usually manifests in a glitch on the left side of the screen -
    it looks like you're off by about two pixels
- Make sure you use the correct IO standard in your constraints file.  All GPIO pins should have the following constraint added: IOSTANDARD = LVCMOS33.
- For A Functionality, you'll have to find some GPIO to use for your Data,
  Latch, and Clk signals.  I found it easiest to use the JB connector on the
board.  Look through the master constraints file to see the location for each
pin.

## Free Code

```vhdl
entity input_to_pulse is
    port ( clk          : in std_logic;
           reset        : in std_logic;
           input        : in std_logic;
           pulse        : out std_logic
         );
end input_to_pulse;

entity font_rom is
    port(
           clk: in std_logic;
           addr: in std_logic_vector(10 downto 0);
           data: out std_logic_vector(7 downto 0)
         );
end font_rom;

entity char_screen_buffer is -- Dual-port RAM template from synthesis guide (minor mods)
    port ( clk        : in std_logic;
           we         : in std_logic;                     -- write enable
           address_a  : in std_logic_vector(11 downto 0); -- write address, primary port
           address_b  : in std_logic_vector(11 downto 0); -- dual read address
           data_in    : in std_logic_vector(7 downto 0);  -- data input
           data_out_a : out std_logic_vector(7 downto 0); -- primary data output
           data_out_b : out std_logic_vector(7 downto 0)  -- dual output port
         );
end char_screen_buffer;

entity character_gen is
    port ( clk            : in std_logic;
           blank          : in std_logic;
           row            : in std_logic_vector(10 downto 0);
           column         : in std_logic_vector(10 downto 0);
           ascii_to_write : in std_logic_vector(7 downto 0);
           write_en       : in std_logic;
           r,g,b          : out std_logic_vector(7 downto 0)
         );
end character_gen;

entity atlys_lab_font_controller is
    port ( 
             clk    : in  std_logic; -- 100 MHz
             reset  : in  std_logic;
             start  : in  std_logic;
             switch : in  std_logic_vector(7 downto 0);
             led    : out std_logic_vector(7 downto 0);
             tmds   : out std_logic_vector(3 downto 0);
             tmdsb  : out std_logic_vector(3 downto 0)
         );
end atlys_lab_font_controller;
```

**Code Listing 1** - Entity templates for the lab to ensure consistency between student designs.

```vhdl
library ieee;
use ieee.std_logic_1164.all;
use ieee.numeric_std.all;

library unisim;
use unisim.vcomponents.all;

entity char_screen_buffer is
    port ( clk        : in std_logic;
           we         : in std_logic;                     -- write enable
           address_a  : in std_logic_vector(11 downto 0); -- write address, primary read address
           address_b  : in std_logic_vector(11 downto 0); -- dual read address
           data_in    : in std_logic_vector(7 downto 0);  -- data input
           data_out_a : out std_logic_vector(7 downto 0); -- primary data output
           data_out_b : out std_logic_vector(7 downto 0)  -- dual output port
         );
end char_screen_buffer;

architecture behavioral of char_screen_buffer is
    signal address_a_reg : std_logic_vector(11 downto 0);
    signal address_b_reg : std_logic_vector(11 downto 0);

    type ram_type is array (4096-1 downto 0) of std_logic_vector(7 downto 0);
    signal RAM : ram_type :=
    (
        (others => x"41")
    );
    -- x"00", x"01", x"02", x"03", x"04", x"05", x"06", x"07", x"08", x"09", x"0A", x"0B", x"0C", x"0D", x"0E", x"0F"
begin

    process (clk) is
    begin
        if rising_edge(clk) then
            if (we = '1') then
                RAM(to_integer(unsigned(address_a))) <= data_in;
            end if;

            address_a_reg <= address_a;
            address_b_reg <= address_b;
        end if;
    end process;

    data_out_a <= RAM(to_integer(unsigned(address_a_reg)));
    data_out_b <= RAM(to_integer(unsigned(address_b_reg)));

end behavioral;
```

**Code Listing 2** - `char_screen_buffer` Code

```vhdl
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;
use IEEE.NUMERIC_STD.ALL;

library UNISIM;
use UNISIM.VComponents.all;

entity nes_controller is
    port (
        reset : in std_logic;
        clk : in std_logic;
        data : in std_logic;
        nes_clk : out std_logic;
        latch : out std_logic;
        a, b, sel, start, up, down, left, right : out std_logic
    );
end nes_controller;

architecture Behavioral of nes_controller is

    type nes_state_type is
        (idle, a_state, b_state, sel_state, start_state, up_state, down_state, left_state, right_state);

    signal state_reg, state_next : nes_state_type;

    signal counter_reg, counter_next : unsigned(9 downto 0);
    signal scalar_reg, scalar_next : unsigned(9 downto 0);

    signal  a_reg, a_next, 
                b_reg, b_next, 
                sel_reg, sel_next, 
                start_next, start_reg,
                up_reg, up_next, 
                down_reg, down_next, 
                left_reg, left_next, 
                right_reg, right_next : std_logic;
begin
    -- counter
    counter_next <=     (others => '0') when counter_reg = 20 else
                            counter_reg + 1 when scalar_reg = 599 else
                            counter_reg;

    scalar_next <= (others => '0') when scalar_reg = 599 else
                        scalar_reg + 1;

    process(clk, reset)
    begin
        if reset = '1' then
            counter_reg <= (others => '0');
            scalar_reg <= (others => '0');
        elsif rising_edge(clk) then
            counter_reg <= counter_next;
            scalar_reg <= scalar_next;
        end if;
    end process;

    -- state reg
    process(clk, reset)
    begin
        if reset = '1' then
            state_reg <= idle;
        elsif rising_edge(clk) then
            state_reg <= state_next;
        end if;
    end process;

    -- next state
    process(state_reg, counter_reg)
    begin
        state_next <= state_reg;

        case state_reg is
            when idle =>
                if counter_reg = 0 then
                    state_next <= a_state;
                end if;
            when a_state =>
                if counter_reg = 2 then
                    state_next <= b_state;
                end if;
            when b_state =>
                if counter_reg = 4 then
                    state_next <= sel_state;
                end if;
            when sel_state =>
                if counter_reg = 6 then
                    state_next <= start_state;
                end if;
            when start_state =>
                if counter_reg = 8 then
                    state_next <= up_state;
                end if;
            when up_state =>
                if counter_reg = 10 then
                    state_next <= down_state;
                end if;
            when down_state =>
                if counter_reg = 12 then
                    state_next <= left_state;
                end if;
            when left_state =>
                if counter_reg = 14 then
                    state_next <= right_state;
                end if;
            when right_state =>
                if counter_reg = 16 then
                    state_next <= idle;
                end if;
        end case;
    end process;

    latch <= '1' when counter_reg = 0 else
                '0';

    nes_clk <=  not counter_reg(0) when counter_reg < 16 and counter_reg > 1 else
                    '0';

    a_next <=   not data when counter_reg = 1
                    else a_reg;
    b_next <=   not data when counter_reg = 3
                    else b_reg; 
    sel_next <=     not data when counter_reg = 5
                        else sel_reg; 
    start_next <=   not data when counter_reg = 7
                        else start_reg; 
    up_next <=  not data when counter_reg = 9
                    else up_reg; 
    down_next <=    not data when counter_reg = 11
                        else down_reg; 
    left_next <=    not data when counter_reg = 13
                        else left_reg; 
    right_next <=   not data when counter_reg = 15
                        else right_reg; 

    -- outputs
    process(clk) 
    begin
        if rising_edge(clk) then
            a_reg <= a_next;
            b_reg <= b_next;
            sel_reg <= sel_next;
            start_reg <= start_next;
            up_reg <= up_next;
            down_reg <= down_next;
            left_reg <= left_next;
            right_reg <= right_next;
        end if;
    end process;

    a <= a_reg;
    b <= b_reg;
    sel <= sel_reg;
    start <= start_reg;
    up <= up_reg;
    down <= down_reg;
    left <= left_reg;
    right <= right_reg;

end Behavioral;
```

**Code Listing 3** - NES Driver

### Third-Party code you'll need

- [Font ROM](font_rom.vhd)

## Grading

| Item | Grade | Points | Out of | Date | Due |
|:-: | :-: | :-: | :-: | :-: |
| Prelab | **On-Time:** 0 ---- Check Minus ---- Check ---- Check Plus | | 10 | | BOC L17 |
| Required Functionality | **On-Time** ------------------------------------------------------------------ **Late:** 1Day ---- 2Days ---- 3Days ---- 4+Days| | 40 | | COB L19 |
| B Functionality | **On-Time** ------------------------------------------------------------------ **Late:** 1Day ---- 2Days ---- 3Days ---- 4+Days| | 10 | | COB L19 |
| A Functionality | **On-Time** ------------------------------------------------------------------ **Late:** 1Day ---- 2Days ---- 3Days ---- 4+Days| | 10 | | COB L19 |
| Use of Git / Github | **On-Time:** 0 ---- Check Minus ---- Check ---- Check Plus ---- **Late:** 1Day ---- 2Days ---- 3Days ---- 4+Days| | 5 | | COB L20 |
| Code Style | **On-Time:** 0 ---- Check Minus ---- Check ---- Check Plus ---- **Late:** 1Day ---- 2Days ---- 3Days ---- 4+Days| | 5 | | COB L20 |
| README | **On-Time:** 0 ---- Check Minus ---- Check ---- Check Plus ---- **Late:** 1Day ---- 2Days ---- 3Days ---- 4+Days| | 20 | | COB L20 |
| **Total** | | | **100** | | |
