## GBA hardware overview

#### System Overview

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

#### Retrocompatibility
- The Game Boy Advance incorporated the original Z80 CPU from the old Game Boy Color, providing complete backward compatibility with all previous gameboy games.
- The GBA auto-detects the type of cartridge that has been inserted and either boots up the ARM7 or the Z80 CPU