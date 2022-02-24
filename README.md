# Arrowmania

A 4 key rhythm game made in PICO-8 inspired by games such as Stepmania and DDR.

# Creating a Custom Song

First, create a copy of `amania-factory.p8`, which is the recommended cart to fork as it only contains the essentials. Then replace the sfx and music patterns with your own (make sure pattern #00 is an empty bar and make sure sfx #01 remains untouched as it is the note miss sound effect).

Once your song has been properly added to the cart, you'll have to make a few changes in the `_init()` functions.

`SYNCTIME` should equal `(The SPD of your music patterns) * 31.8`
`CARTNAME` should be the name of the cart you're editing
`SELECTCART` should be the name of your main menu cart (or should equal CARTNAME if you don't have one)

*If you're posting your mod to the BBS, use the format `#CART_NAME` instead of `CART_NAME.p8`*

# Creating a Custom Chart

If you go to tab 3 of the PICO-8 code editor, you'll find both `init_beatmap()` and `init_beatmap_hard()`. This is where you'll put both beatmaps, so start by erasing all the pre-existing calls to `map_add()`.

Once you've done that, open a second instance of PICO-8, and type `LOAD #AMANIA_CHARTER`. You can then use this cart to create your beatmap, where each step is equal to one step in the sfx editor (assuming that your `SYNCTIME` was set properly in the previous step)

Once you finish each part of your beatmap, press 🅾 to copy the string to your clipboard, and then add it to your beatmap using `map_add(offset, notes)`, where:

`offset` - The offset of all notes to be added. (If your charting pattern 1 of the song, the first notes offset would be 0 in the pattern, but 32 overall. So this should equal 32 in that instance.)

`notes` - The string generated by `#AMANIA_CHARTER`

# Creating Custom Background Art

If you go to tab 2 of the PICO-8 code editor, you'll find `background_draw()`. This function is called each frame and is where all the background art is drawn. Above this function exists variables that are unique to the pre-existing background art.

The top of `background_draw()` includes a for loop which checks the pitch, volume, and waveform of the notes being played on all 4 channels, so feel free to use this to make your visuals react to the music!

# Other Information

If you go to tab 4 of the PICO-8 code editor, you'll find `arrows_init()`. In here you can tweak a few variables:

`noteheight` - How many pixels between the bottom/top of the screen and the receptors

`notetime` - How long a note is on screen in frames (Essentially reverse note jump speed)

`hitrange` - The pixel radius of the arrows hitbox (Lower number means tighter inputs)

`receptorx` - The x position of the receptors (From the center)

PS: If you want to create modcharts (where the arrows start moving around and all that jazz) you can use `roffsets[i].x` and `roffsets[i].y`, where `i` is lanes 1 through 4.