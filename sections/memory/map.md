## Overall Memory Map

### General Internal Memory

    - 00000000-00003FFF   BIOS - System ROM                                (16 KBytes)
    - 00004000-01FFFFFF   Not used
    - 02000000-0203FFFF   WRAM - On-board Work RAM (External Working RAM)  (256 KBytes) 2 Wait
    - 02040000-02FFFFFF   Not used
    - 03000000-03007FFF   WRAM - On-chip Work RAM (Internal Working RAM)   (32 KBytes)
    - 03008000-03FFFFFF   Not used
    - 04000000-040003FE   I/O Registers
    - 04000400-04FFFFFF   Not used

### Internal Display Memory

    - 05000000-050003FF BG/OBJ Palette RAM (1 Kbyte)
    - 05000400-05FFFFFF Not used
    - 06000000-06017FFF VRAM - Video RAM (96 KBytes)
    - 06018000-06FFFFFF Not used
    - 07000000-070003FF OAM - OBJ Attributes (1 Kbyte)
    - 07000400-07FFFFFF Not used

### External Memory (Game Pak)

    - 08000000-09FFFFFF Game Pak ROM/FlashROM (max 32MB) - Wait State 0
    - 0A000000-0BFFFFFF Game Pak ROM/FlashROM (max 32MB) - Wait State 1
    - 0C000000-0DFFFFFF Game Pak ROM/FlashROM (max 32MB) - Wait State 2
    - 0E000000-0E00FFFF Game Pak SRAM (max 64 KBytes) - 8bit Bus width
    - 0E010000-0FFFFFFF Not used

> Regarding the **GamePak ROM** memory: the access speed of each aforementioned sections can be set individually, thus they are named **Wait State 0**, **Wait State 1** and **Wait State 2**. This specifications enables the optional use of the ROM by varying the access speed.

### Unused Memory Area

    - 10000000-FFFFFFFF Not used (upper 4bits of address bus unused)

### Default WRAM Usage
- The **256 bytes** located at 03007F00h-03007FFFh **in the Internal Working RAM** are reserved for  Interrupt vector, Interrupt Stack, and BIOS Call Stack.
- The remaining memory is free for whatever use, including the User Stack, initially located at 03007F00h.

### CPU Read/Write Access Widths

| Region        | Bus | Read    | Write   | Cycles         |
| ------------- | --- | ------- | ------- | -------------- |
| BIOS ROM      | 32  | 8/16/32 | -       | 1/1/1          |
| Work RAM 32K  | 32  | 8/16/32 | 8/16/32 | 1/1/1          |
| I/O           | 32  | 8/16/32 | 8/16/32 | 1/1/1          |
| OAM           | 32  | 8/16/32 | 16/32   | 1/1/1 X        |
| Work RAM 256K | 16  | 8/16/32 | 8/16/32 | 3/3/6 XX       |
| Palette RAM   | 16  | 8/16/32 | 16/32   | 1/1/2 X        |
| VRAM          | 16  | 8/16/32 | 16/32   | 1/1/2 X        |
| GamePak ROM   | 16  | 8/16/32 | -       | 5/5/8 XX / XXX |
| GamePak Flash | 16  | 8/16/32 | 16/32   | 5/5/8 XX / XXX |
| GamePak SRAM  | 8   | 8       | 8       | 5     XX       |

> X - Plus 1 cycle if GBA accesses video memory at the same time.

> XX - Default waitstate settings, see System Control chapter.

> XXX - Separate timings for sequential, and non-sequential accesses.

> **Note on performance:** As the GamePak bus is limited to 16 bits, executing ARM instrucions (which has 32-bit opcodes) from inside of the ROM would eventually result in a not so good performance. It's reccomended to use THUMB instructions (16-bit each) so each opcode can be read at once.

[Go back](https://goiabada.github.io/docs/sections/memory/index)