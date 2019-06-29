# Entex Adventure Vision

## BIOS and cartridge ROMs

Due to copyright reasons, ROMs are not included and must be placed separately on the Replay SDCARD.

* `advision.rom` - Main CPU ROM

    sha1sum bf7b0663e9125c9bfb950232eab627d9dbda8460

* `avSoundRom.bin` - Sound CPU ROM

    sha1sum 6355909dc04c53c22427eaca5f7706f1c037211f

Place the cartridge ROM files next to the CPU ROMs. You can optionally organize them in a subfolder.

## Core startup

The Adventure Vision core is started by default with an empty cartridge slot and it's required to load a cartridge ROM file from the Replay OSD menu. The selected file is uploaded to the FPGA, the core is reset and the CPU executes the game.

## Controls

### Joystick

A joystick attached to first port is mapped to Adventure Vision's built-in controls:

* joystick up, down, left, right
* joytsick button 1 -> button 3 (bottom)
* joystick button 2 -> button 1 (top)

### Virtual keyboard

* Cursor up, down, left, right
* W -> button 1 (top)
* A -> button 2 (left)
* S -> button 3 (bottom)
* D -> button 4 (right)

## Video output

The core outputs standard 640x480 progressive with 60 Hz.
