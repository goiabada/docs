## GBA hardware overview

### System Overview

- **CPU:** 32-bit RISC CPU (ARM7TDMI)/16.78 MHz
- **Second CPU:** 8-bit CISC CPU for GBC compatibility
- **Memory**
  - **System ROM:** 16Kbytes + 2Kbytes for GBC
  - **Working RAM:** 32 Kbytes + CPU External 256 Kbytes
  - **VRAM:** 96 Kbytes
  - **OAM:** 64 bits x 128
  - **Pallete RAM**: 16 bits x 512 (256 colors for OBJ, 256 colors for BG)
  - **Game Pak:** Up to 512 Kbits: SRAM or flash memory
- **Display:** 240 x 160, with 32,768 colors simultaneously displayable
- **Sound:** 4 sounds (corresponding to GBC sounds) + 2 CPU direct sounds (PCM format)

### Retrocompatibility

- The Game Boy Advance incorporated the original Z80 CPU from the old Game Boy Color, providing complete backward compatibility with all previous gameboy games.
- The GBA auto-detects the type of cartridge that has been inserted and either boots up the ARM7 or the Z80 CPU

### Hardware Access

- The GBA architecture is similar to a PC in many ways. Both have one or more processors, RAM, a digital signal processor (DSP), a motherboar and a BIOS (Basic Input/Output System) that causes the hardware to boot up.
- The GBA has no operating system, thus it controls the hardware at the lowest level.
- Making necessary for the running programs (games) to incorporate all the code necessary to display on the screen, play music and detect user input.
- Since we can't use interrupts since it does not have an OS, all operations must write a specific value to specific memory address to make things happen.

### Memory Architecture
| Memory Type | Access Widths | Description                                                                                      |
| ----------- | ------------- | ------------------------------------------------------------------------------------------------ |
| IWRAM       | 8, 16, 32     | 32 KB "internal" working RAM. Typically used for fast scratchpad RAM and for time-critical code. |
| EWRAM       | 8, 16         | 256 KB "external" working RAM. Typically used for        main data storage and multiboot code.   |
| VRAM        | 8, 16         | 96 KB video RAM. Stores all graphics data. Can only write 16 bits at a time.                     |
| ROM         | 8, 16         | ROMs can be read in either slow (4/2) or fast (3/1) mode                                         |
| Save RAM    | 8, 16         | The game save RAM, part of the cartridge                                                         |

> As far as the ARM processor is concerned, a word is 32 bits, halfword is 16 bits and a byte is 8 bits.

#### Internal Working RAM (IWRAM)
- The **IWRAM** is the only memory directly accessible on the 32-bit internal data bus, since it is **built into the CPU itself** (that's the reason why it's called *internal*).
- It's the fastest memory the GBA has access to, plus the only one that can be accessed 32 bits at a time.
- Only 256Kbits available, tho.

#### External Working RAM (EWRAM)
- Do not be misled by the name, the EWRAM is not built inside the cartrige, but **inside** the GBA as well.
- It's located outside the CPU's core, on a 16-bit data bus.
- **2048 Kbits** of memory available, with **each access costing three cycles**.
- This is where large data items are stored, such as graphics before they are transferred into de VRAM for display.

#### ROM
- Contains the game's data. Located inside the cartridge.
- Can operate at two different speeds, in two different modes:
  - Speeds are given as apair of wait-state values, such as 3/1.
  - Can be accessed sequentially or nonsequentially:
    - A nonsequential access occurs whenever a new area of the ROM is accessed. Sending the memory address to the ROM takes time, and these accesses take the number of wait states indicated by the first number (3, in this example). One full nonsequential access would take four cycles (three wait + one normal cycle) in this scenario.
    - A sequential access occurs when the very first memory acess to the ROM **is the following one**, taking one wait state less to run.
- Like EWRAM, it's accessible via the 16-bit data bus.

#### Game Save
- Some cartridges have nonvolatile memory for storing saved games inside the cartridge.
- Three different kinds of memory are used for this:
  - Battery-backed static RAM (SRAM)
  - Flash ROM
  - Serial EEPROM

#### Graphics Memory
- We have three kinds of memory that deal exclusively with the video memory and the display screen: video memory, palette memory and object attribute memory (OAM, for handling sprites)

##### 