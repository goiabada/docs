## The Graphics System
- The GBA refresh rate equates do 280,896 clock cycles per frame (the time it takes to display the entire video buffer) which equals to **59.73 Hz**, our maximum frame rate.
- Any game that claims to achieve more than 60 FPS is **simply subframing the display**, which may have practical uses for special effects.
- There are three tile-based modes that resemble the previous Game Boy graphics system, plus new three bitmap-based modes that provide more *creative freedom* with games.

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

####