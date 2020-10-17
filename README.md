# Link to the Past Palette Randomizer

JavaScript app to randomize palettes in The Legend of Zelda: A Link to the Past.

## Table of Contents

- [Link to the Past Palette Randomizer](#link-to-the-past-palette-randomizer)
  - [Table of Contents](#table-of-contents)
  - [Installation](#installation)
  - [Usage](#usage)
    - [randomize](#randomize)
    - [randomize_copy](#randomize_copy)
  - [What is a palette randomizer?](#what-is-a-palette-randomizer)
  - [Advantages over other palette randomizers](#advantages-over-other-palette-randomizers)
  - [Contributions](#contributions)
  - [Credits](#credits)
  - [License](#license)

## Installation

Using npm to install as an ES6 module:

```
$ npm i @maseya/z3pr
```

Alternatively, an UMD build (minified, with source map) is available through npm:

```
$ npm i @maseya/z3pr-umd
```

Or from the [release page](https://github.com/maseya/z3pr-js/releases).

## Usage

Import the ES6 module:

```
import { randomize } from 'z3pr';
```

In browser with the UMD build:

```
<script src="z3pr-umd.js"></script>
<script>
const z3pr = window.z3pr;
const randomize = z3pr.randomize;
</script>
```
Example of use:

```
const rom = data; // Uint8Array instance
randomize(rom, { mode: 'maseya', seed: 0x01234567 });
```

### randomize

**Arguments**

1. `rom` (Uint8Array): The ROM data to modify.
2. `[options={}]` (object): The options object
3. `[options.mode]` (string): Specifies the randomization mode to use. A missing
  or invalid mode will throw an exception.
    - `none`: No modifications to the ROM data.
    - `maseya`: Modify according to the rules described in later sections.
    - `grayscale`: Modify all colors to be grayscale.
    - `blackout`: Set all colors to black.
    - `classic`: Modify according to the "legacy" randomization rules.
    - `dizzy`: Modify all colors by hue shift only.
    - `sick`: Modify all colors by luma shift only.
    - `puke`: Change all colors to completely random color values.
    - `randomize_overworld`: Modify all overworld palettes.
    - `randomize_dungeon`: Modify all dungeon and underworld palettes.
    - `randomize_link_sprite`: Modify the palette of the Link sprite.
    - `randomize_sword`: Modify the palette of Link's sword.
    - `randomize_shield`: Modify the palette of Link's shield.
    - `randomize_hud`: Modify the palette of the HUD.
4. `[options.seed]` (number|number[..3]): The optional seed number(s). Up to
  three 32 bit integer numbers can be specified. If no numbers are present
  the standard `random` function will be used for seeding internally.
3. `[next_blend]` (function*): The optional generator function that returns a
  sequence of color blend values. (seed)
    - `[seed]` (number|number[..3]): The seed that was passed through *4.*, or
    undefined if missing.
    - *yield* (color_f): An object compatible with values returned by the
    `color_f` function.
        - `color_f` (function): A function that creates RGB color component values.

**Returns**

(Uint8Array): Returns the ROM data.

### randomize_copy

Same interface and behavior as `randomize`, except that it makes modifications
to a copy of the ROM data argument.

## What is a palette randomizer?

A palette randomizer is, as the name suggests, something that randomizes a
game's _palettes_ (its color collections). This randomizer is designed to
randomize colors according to their groupings. For example, all colors that
represent grass will be randomized with the same logic, whereas water's colors
will be randomized with different logic. This creates a consistent color scheme
without any disconnects in colors (e.g. grass having two different colors).

A set of colors is randomized according to the following rules:

- Shift a color's hue by at least 2.5%. This ensures a color is actually changed.
- If increasing saturation, do so very gently and proportional to current value.
- Saturation is allowed to decrease all the way to zero.
- Increasing brightness is similar to increasing saturation.
- If a lot of saturation was removed, allow increasing the brightness slightly more.
- If reducing brightness, do so by no more than half (this may be restricted
  further in the future).

![example1](https://cdn.discordapp.com/attachments/329059206030295051/641420281608405022/unknown.png)
![example2](https://cdn.discordapp.com/attachments/329059206030295051/641445510074466304/unknown.png)

## Advantages over other palette randomizers

While [Link to the Past Randomizer](https://alttpr.com) already has a built-in
palette randomizer, it does not take the necessary care to ensure every palette
can be randomized. Certain items like houses and rocks are never randomized.
Further, the overworld palette randomizer does not have as much control as this
app does, which allows for much richer variety of colors.

TODO: Add pictures

- The overworld map palette is updated to reflect the new overworld palette.
- Sprite palettes of rocks and bushes match their object palettes.
- Ice golem palettes match Ice Palace palettes.

![example3](https://media.discordapp.net/attachments/329059206030295051/712227454248550450/unknown.png?width=783&height=684)
![example4](https://media.discordapp.net/attachments/329059206030295051/712228332552323112/unknown.png?width=783&height=684)
![example5](https://media.discordapp.net/attachments/329059206030295051/712383831268786216/unknown.png?width=782&height=684)

## Contributions

Do you want to add a feature, report a bug, or propose a change to the project?
That's awesome! First, please refer to our [Contributing](CONTRIBUTING.md) file.
We use it in hopes having the best working environment we can.

## Credits

- [Nelson Garcia](https://github.com/bonimy): Project leader and original C# programmer.
- [HalfARebel](https://github.com/rebelusquo): Java Script port implementer.

## License

Java Script App for randomizing Link to the Past palettes
Copyright (C) 2018-2020 Nelson Garcia

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU Lesser General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU Lesser General Public License for more details.

You should have received a copy of the GNU Lesser General Public License
along with this program.  If not, see <https://www.gnu.org/licenses/>.
