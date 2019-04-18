## The Graphics System

- The GBA refresh rate equates to 280,896 clock cycles per frame (the time it takes to display the entire video buffer) which equals to **59.73 Hz**, our maximum frame rate.
- Any game that claims to achieve more than 60 FPS is **simply subframing the display**, which may have practical uses for special effects.
- There are three tile-based modes that resemble the previous Game Boy graphics system, plus new three bitmap-based modes that provide more _creative freedom_ with games.

### Tile-Based Modes (0-2)

> A "tile" is a small 8 x 8 section of the screen, and this is how the original Game Boy handled all backgrounds.

#### Mode 0

- In this mode four text background layers can be shown.
- Backgrounds 0-3 count as "text" backgrounds and cannot be scaled nor rotated.

#### Mode 1

- It's similar in most respects to mode 0, but the main difference here is that only three backgorunds are accessible: 0, 1 and 2.
- Backgrounds 0 and 1 are text, while 2 is a rotation/scaling background.

#### Mode 2

- Like Modes 0 and 1, Mode 2 uses tiled backgrounds.
- It uses backgrounds 2 and 3 as rotation/scaling backgrounds.

### Bitmap-Based Modes (3-5)

#### Mode 3

- Standard 16-bit bitmapped (nonpaletted) 240 x 160 mode
- The map starts at address 0x06000000 and it's 76,800 bytes long
- Allows the full color range to be displayed at once
- But as the frame buffer is too large, page flipping is not possible
  - A workaround would be to copy the frame buffer from de RAM to the VRAM during retrace
> Page flipping is a method of reducing flickering on the screen

#### Mode 4

- 8-bit bitmapped (paletted) 240 x 160 mode
- The map starts at either 0x06000000 or 0x0600A000 addresses, depending on bit 4 of the REG_DISPCNT register
- The pallete is located at 0x5000000 and contains 256 16-bit color entries
- Allows page-flipping techniques

#### Mode 5

- 16-bit bitmapped 160 x 128 mode
- The display starts at the upper-left corner but can be shifted using rotation and scaling registers for background 2
- It has two frame buffers available
- Bit 4 of the REG_DISPCNT register sets the start of the frame buffer to 0x06000000 when it's zero, or 0x0600A000 when it's one

[Go back](https://goiabada.github.io/docs/sections/overview/index)
