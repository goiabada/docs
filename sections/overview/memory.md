## Memory Architecture

| Memory Type | Access Widths | Description                                                                                      |
| ----------- | ------------- | ------------------------------------------------------------------------------------------------ |
| IWRAM       | 8, 16, 32     | 32 KB "internal" working RAM. Typically used for fast scratchpad RAM and for time-critical code. |
| EWRAM       | 8, 16         | 256 KB "external" working RAM. Typically used for        main data storage and multiboot code.   |
| VRAM        | 8, 16         | 96 KB video RAM. Stores all graphics data. Can only write 16 bits at a time.                     |
| ROM         | 8, 16         | ROMs can be read in either slow (4/2) or fast (3/1) mode                                         |
| Save RAM    | 8, 16         | The game save RAM, part of the cartridge                                                         |

> As far as the ARM processor is concerned, a word is 32 bits, halfword is 16 bits and a byte is 8 bits.

### Internal Working RAM (IWRAM)
- The **IWRAM** is the only memory directly accessible on the 32-bit internal data bus, since it is **built into the CPU itself** (that's the reason why it's called *internal*).
- It's the fastest memory the GBA has access to, plus the only one that can be accessed 32 bits at a time.
- Only 256Kbits available, tho.

### External Working RAM (EWRAM)
- Do not be misled by the name, the EWRAM is not built inside the cartrige, but **inside** the GBA as well.
- It's located outside the CPU's core, on a 16-bit data bus.
- **2048 Kbits** of memory available, with **each access costing three cycles**.
- This is where large data items are stored, such as graphics before they are transferred into de VRAM for display.

### ROM
- Contains the game's data. Located inside the cartridge.
- Can operate at two different speeds, in two different modes:
  - Speeds are given as apair of wait-state values, such as 3/1.
  - Can be accessed sequentially or nonsequentially:
    - A nonsequential access occurs whenever a new area of the ROM is accessed. Sending the memory address to the ROM takes time, and these accesses take the number of wait states indicated by the first number (3, in this example). One full nonsequential access would take four cycles (three wait + one normal cycle) in this scenario.
    - A sequential access occurs when the very first memory acess to the ROM **is the following one**, taking one wait state less to run.
- Like EWRAM, it's accessible via the 16-bit data bus.

### Game Save
- Some cartridges have nonvolatile memory for storing saved games inside the cartridge.
- Three different kinds of memory are used for this:
  - Battery-backed static RAM (SRAM)
  - Flash ROM
  - Serial EEPROM

### Graphics Memory
- We have three kinds of memory that deal exclusively with the video memory and the display screen: video memory, palette memory and object attribute memory (OAM, for handling sprites)

#### Video Memory
- Video Memory is where all graphics data musta be stored to be displayed on the screen.
- **VRAM** is a zero wait-state memory, like **IWRAM**, but sits on the 16-bit data bus, thus making possible to move data half as fast comparing to the latter.
- Writing a byte actually writes 2 bytes of the same value, this seeming flaw can actually be useful to quickly redraw the screen, for example.
- Attempting to write memory when it's being used to draw the screen can result in graphical glitches and image tearing.
> Image tearing is the event when the image is being draw while the screen is refreshing, resulting in an uneven image

#### Palette Memory
- The GBA video modes use palettes to specify the colors being used.
- We have two separate 256-color palletes here: one for the background images and another one for the sprites.
- Furthermore, each palette can be divided into 16 palettes of 16 colors each.
- Color 0 of any palette is always transparent no matter the value we write into de palette memory.
- The **mode 4** video mode does not use a palette, but directly addresses color in each pixel.

#### Object Atribute Memory
- This is where we store the attributes of what sprite should be displayed, how and where.
- The actual data comes from the **VRAM**, but the rest comes form the **OAM**.


[Go back](https://goiabada.github.io/docs/sections/overview/index)