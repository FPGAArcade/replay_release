# Odyssey2

## BIOS and cartridge ROMs

Due to copyright reasons, ROMs are not included and must be placed separately on the Replay SDCARD.

* `o2rom.bin` - BIOS ROM

    sha1sum b2e1955d957a475de2411770452eff4ea19f4cee

Place the cartridge ROM files next to the CPU ROMs. You can optionally organize them in a subfolder.

## Core startup

The Odyssey2 core is started by default with an empty cartridge slot and it's required to load a cartridge ROM file from the Replay OSD menu. The selected file is uploaded to the FPGA, the core is reset and the CPU executes the game.

## Controls

### Joystick

Joysticks attached to port 1 and 2 are mapped to the console controllers:

* joystick up, down, left, right
* joytsick button 1 -> action button

### Virtual keyboard

The first joystick is emulated in parallel using the virtual keyboard:

* Cursor up, down, left, right
* enter -> action button

Virtual keys are also mapped to the console keyboard:

* alphanumeric keys 0-9, a-z
* keys `.`, `,`, `+`, `-`, `/`, `=`
* space, enter, backspace

## Video output

* NTSC 720x480 progressive with 60 Hz
