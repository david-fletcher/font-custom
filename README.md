# Font Custom
![hero image](./assets/hero.png)

Create new fonts with Aseprite and load them in to be used in your projects!

All you'll need is a `font atlas` (i.e. a grid-based arrangement of the characters you'd like to use) and a simple `.json` file that describe the properties of the font.

![a demonstration](./assets/demo.png)

## FAQ

* Does this extension create fonts from my pixel art? (i.e., export to .ttf, .otf, etc)
    * No, unfortunately it does not create font files. It does, however, give you the option to use your custom font within Aseprite as if you were using the `Edit > Insert Text` menu option. If you'd like to create font files based on a pixel map, check out [this itch.io project](https://yellowafterlife.itch.io/pixelfont)!
* Why aren't special characters like `Ð`, `Þ`, `Æ`, or others working?
    * Unfortunately, for now, this extension can only handle the ASCII characters at the moment. I am investigating how we can modify the extension in the future to allow for (full) UTF-8, UTF-16 and UTF-32 compliant characters!
* Are there other Aseprite extensions / scripts related to this?
    * Of course! Here's a list of projects I know about thus far:
        * [PixelFont](https://yellowafterlife.itch.io/pixelfont)!
        * [Write Tool For Aseprite](https://bowgrape.itch.io/write-tool)

## How to Use Font Custom

1. Download this extension by visiting the releases page!
2. Create a pixel art font based on a grid with standard height and width. Don't worry about kerning, character widths, and etc; the next step will handle that. **Save this file as `.png`, `.ase`, or `.aseprite`!**

![gif for font creation](https://media.giphy.com/media/rPHEAnZYVDzcJ5ibR1/giphy-downsized.gif?cid=790b76117b2dc73e0ecf46e24ddc77c3a619f338dc40a823&rid=giphy-downsized.gif&ct=g)

3. Create a properties file with the extension `.json`. The data has to be formatted in a special way, so I recommend using the [example.json](./examples/example.json) file you can find here as a stepping stool.

![gif for property creation](https://media.giphy.com/media/YZRIUu7uKkSc0U7uyo/giphy-downsized.gif?cid=790b76113bc80f8bd1362c832c3086f14db0b405536b2262&rid=giphy-downsized.gif&ct=g)

4. In Aseprite, simply install this extension (only have to do this once) and navigate to `Edit > FX > Use Custom Font` and follow the dialog prompts to include text with your custom font in your Aseprite project!

![gif for using extension](https://media.giphy.com/media/BKyfLNEwpxNiiGD5O9/giphy-downsized.gif?cid=790b76118fd0d366939eb128c3f721f794a3b8445b297d8f&rid=giphy-downsized.gif&ct=g)

## Things to Know
1. In your properties file, not every "object" is mandatory. All possible objects are listed below; mandatory objects have a `*` next to them. DO NOT include the asterix in the key-names in your properties file (use [example.json](./examples/example.json) as a template).
    * `*alphabet` - a list of all of the characters found in the font file. Due to technical reasons, the list of characters must _match exactly_ the ordering found in the font file (left to right, top to bottom).
    * `*sprite_path` - a pointer to the sprite file that contains the font. Valid file extensions are `.png`, `.ase`, or `.aseprite`. If a _relative_ file name is given, the extension will look for a font file in the same directory as the property file (recommended). However, you can also give it an _absolute_ file name anywhere on your computer to locate the font file, if desired.
    * `*atlas` - an object containing information relevant to the construction of each character in the alphabet
        * `*rows` - how many rows of letters exist in the font file
        * `*cols` - how many columns of letters exist in the font file
        * `*grid_width` - in pixels, how wide is _exactly one letter_
        * `*grid_height` - in pixels, how tall is _exactly one letter_
        * `common_width` - in pixels, how wide should most characters _be rendered_ (will default to `grid_width` if not specified)
        * `character_widths` - an object containing width information for particular letters (will default to `grid_width` if not specified)
            * every `key` in this object will be _a single letter_ from the `alphabet`; every `value` in this object will be the number of pixels wide that this `key` should be rendered with
    * `default_spacing` - in pixels, the default amount of space to be left in between each letter when rendering (will default to `1` if not specified)
    * `kerning` - an object that specifies spacing between relationships of characters (will default to not use any kerning if not specified)
        * every `key` in this object will be _a single letter_ from the `alphabet`; every `value` will be another object with the form:
            * `*paired_with` - a list of all of the characters, that when appearing _after_ `key`, will have their spacing adjusted by the amount `spacing`
            * `*spacing` - in pixels, how much should the spacing be changed to accomodate the `key` : `paired_with` relationship (can be a negative value) when rendering

2. If you encounter a bug, please report it as an Issue here on this repository! If you are code-saavy, you can also fork this repository and then submit a pull-request.

## Credits

This extension was commissioned by `dani boye` on the [Aseprite Discord server](https://discord.gg/Rt5S6NZFkK). He also provided the [6_by_9.png](./examples/6_by_9.png) to use as an example font!

The json-parsing library, `json.lua`, was provided by `rxi` under the MIT License: https://github.com/rxi/json.lua

As an advocate of open-source software, feel free to suggest edits, or just fork this repository and make your own! The license on this software is open for commercial and private use. This extension will remain free forever; however, if you'd like to buy me a coffee, you can do so here: 

[![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/L3L766S5F)
