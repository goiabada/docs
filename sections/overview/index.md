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

- The GBA architecture is similar to a PC in many ways. Both have one or more processors, RAM, a digital signal processor (DSP), a motherboard and a BIOS (Basic Input/Output System) that causes the hardware to boot up.
- The GBA has no operating system, thus it controls the hardware at the lowest level.
- Making necessary for the running programs (games) to incorporate all the code necessary to display on the screen, play music and detect user input.
- Since we can't use interrupts since it does not have an OS, all operations must write a specific value to specific memory address to make things happen.

You can dedicated sections below:
1. [Memory Architecture](https://goiabada.github.io/docs/sections/overview/memory)
2. [Processor](https://goiabada.github.io/docs/sections/overview/processor)
3. [Graphics System](https://goiabada.github.io/docs/sections/overview/graphics)
4. [Sound System](https://goiabada.github.io/docs/sections/overview/sound)

[Go back](https://goiabada.github.io/docs/)