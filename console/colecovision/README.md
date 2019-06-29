# Colecovision

## BIOS and cartridge ROMs

Due to copyright reasons, ROMs are not included and must be placed separately on the Replay SDCARD.

* `coleco_bios.bin` - BIOS ROM

    sha1sum 5d564490df4a80f0bab2b534a8102173619359f1

Place the cartridge ROM files next to the CPU ROMs. You can optionally organize them in a subfolder.

## Core startup

The Colecovision core is started by default with an empty cartridge slot and it's required to load a cartridge ROM file from the Replay OSD menu. The selected file is uploaded to the FPGA, the core is reset and the CPU executes the game.

## Controls

### Joystick

Joysticks attached to port 1 and 2 are mapped to the Colecovision controllers:

* joystick up, down, left, right
* joytsick button 1 -> left controller button
* joystick button 2 -> right controller button

### Virtual keyboard

The first controller is emulated in parallel using the virtual keyboard:

* Cursor up, down, left, right
* lctrl, space  -> left controller button
* lshift, enter -> right controller button
* keys 0-9      -> respective key on numberpad
* key ,         -> asterisk
* key .         -> hash

## Video output

* R1: 720x460 progressive with 60 Hz
* V4: 640x480 progressive with 60 Hz
