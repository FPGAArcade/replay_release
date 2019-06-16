# Electron Core ROMS

In order to use the Electron core you will need the OS and Basic ROMs
or a combined os_basic ROM.

Rom sha1sum

  os.rom       a48b8fa0cfb09140e808ac8a187316c605a0b32e
  basic.rom    4a7393f3a45ea309f744441c16723e2ef447a281
  os_basic.rom bad51a4666ff9e9eed19811a1eb9d4cda10e69a3

Replay firmware newer than 25th May 2019 is recommended for full feature support.

# Core Status

The core is feature complete as far as the base Electron hardware goes.

Games and programs may be loaded from tape (uef/raw) and saved back out
to tape (raw). Refer to the Virtual Cassette section for file format/usage.

The notable missing features are:

  - Fast Forward / Rewind
  - Tape position counter
  - Various hardware add-ons


# Key Binds

Most non-shifted keys on the Electron have been mapped to the same non-shifted
key on a regular keyboard, however, the shifted and ctrl states will be the
Electron symbol not the symbol shown on a regular keyboard.

Exceptions to this are:

  - : and the shifted * are moved to the key for "'" and "@" key
  - COPY key is bound to "]"
  - BREAK key bound to SCROLL LOCK. Use SCROLL LOCK for soft reset or
    CTRL+SCROLL LOCK for hard reset.

For example, the "shift+8" on a normal keyboard outputs "*" whilst on the
Electron you get a "(". The "*" symbol on the Electron keyboard is shown
instead on the "shift+:" key. However, as noted above, the core uses the
"shift+'" key for a "*" as the ":" key was mapped to "'" due to conflicting with
the ";" key and its shifted key "+" (clear as mud?)

As with the original electron, caps-lock is toggled via shift+capslock, whilst
holding capslock will result in the function key, i.e capslock+e will output
"ELSE"


# Video Output

Two video modes are available. "Authentic" and "Compatible". By default the
core operates in "compatible" mode. Monitors should be set to a 4:3 aspect
ratio if available.

To change the default mode, edit the replay.ini file and move the ",default"
from the compatible option to authentic (or vice-versa). E.G to default to
"Authentic" mode

  item = "Accuracy", 0x00000021,dynamic
  option = "Authentic",  0x00000000,default
  option = "Compatible", 0x00000021

## Authentic Mode

Authentic mode is a more faithful recreation of the Electron's PAL signal
running at 15.625kHz line frequency and 50Hz vertical refresh using
CSync. The timing derived from the RTC and Display interrupts is also
more accurate.

TVs will accept this signal via scart sockets. (see below for cabling
information).

Note: Due to the use of CSync, even if your monitor supports a
15.625kHz line frequency over VGA, it is still unlikely to work as many
expect separate H & V Sync signals rather than CSync.

Also be aware that some monitors when connected via HDMI will mis-identify
authentic mode as a 720x576 @25Hz signal. This can cause excess flickering.

## Compatible Mode

Compatible mode uses a tweaked PAL signal (two fields of 312 lines rather than
312.5 lines) and scan line doubler to increase the chance of the Electron's
non-standard signal working with VGA/DVI/HDMI connected monitors.

Whilst supporting a wider range of displays, the dropping of one line per
frame means the core will run slightly faster than normal. Roughly 1 second
faster per 5 minutes of runtime or 99.9844Hz vs 100.128Hz


## Cables

For Scart connections a DVI/VGA adapter plus VGA to Scart cable will be needed.
Be aware that most VGA/Scart cables will not have a compatible pin-out but most
scart cables can easily have the pins switched around.

See http://www.fpgaarcade.com/punbb/viewtopic.php?id=1211 for instructions
on how to modify a regular VGA/Scart cable to work with the replay.

Alternatively, compatible cables can be bought, they'll be sold as suitable for
the "minimig" such as:

http://amigakit.leamancomputing.com/catalog/product_info.php?products_id=919


# Virtual Cassette Interface

## UEF Format

The UEF file format is the most common means of archiving Electron (and BBC)
tapes and is directly supported by the Replay in uncompressed form.

Whilst a program may have the .uef extension, it may be gzip compressed
and should be renamed to .uef.gz and decompressed by gunzip (Linux) or
7-zip on Windows before the resulting .uef file is transfered to your SD card.

## RAW Format

In addition to UEF, the core continues to support the older raw format with the
file extension ".raw". Such a file can be created by extracting the tape data
from a UEF file including start/stop bits. A python uef2raw.py script will
do this for you and can be found in the tools/ folder.

Usage:

  python uef2raw.py <input_file.uef> <output_file.raw>

"raw" was used prior to the Firmware support for uef and should no longer
be needed.


## Loading

From the "Virtual Tape" OSD menu, select tape "1" and choose a
uef or raw file (prepared as above). Switch to the "Cassette Player" menu
and switch "Play" to ON. The core implements motor control so the
tape will not begin playing until the Electron enables the motor.

Load the program/app/game as normal by issuing

  CHAIN""

There is no need to toggle play to OFF, the Electron will pause playback
as and when needed.

Rewind/Fast forward is not currently supported. You can work around this by
ejecting and re-inserting the tape which will reset the position to
the beginning of the tape.

Setting "Speed" to "Turbo Load" via the Tape Player menu will greatly
reduce tape loading time. Elite will take 5m 6s to load in authentic
mode and 52s in turbo mode.

Turbo Load may be activated at any time, however once enabled requests
to return to authentic mode will be ignored until the cassette motor
stops. It is recommended you set "Speed" prior to starting a load
and leave it set for the duration.


## Saving

In order to save, you need to mount a raw file with plenty of space. You
can create blank 1 megabyte tape on Linux using:-

  dd if=/dev/zero of=tape_1.raw bs=1M count=1

Tapes up to around 400MB in size should be usable although ill advised until
there's a way to jump to specific counter locations.

Before mounting a tape, ensure PLAY and REC are OFF. Insert the tape then
switch REC to ON and then PLAY to ON. Save as normal e.g

  SAVE "TESTING"

and press return.

Support for saving to the UEF format and creating "blank" tapes is planned
for a future firmware version.


## Physical Cassette Interface

A physical cassette recorder cannot yet be attached to the Replay Board.
However the core should support loading once suitable pins are routed to it.

You will need to replicate the original Acorn cassette hardware interface
for CAS IN, CAS OUT and optionally CAS MO. CAS RC is not used currently.
In addition be careful to adjust voltage levels to be within spec for the FPGA.


# Plus1 Hardware Expansion

The Plus1 add-on brought 2 cart slots for ROMs and additional hardware as
well as an analogue port for joysticks/paddles/other hw and a printer port.

ROMs and joysticks are supported. Other Plus1 features are not.

The Plus1 requires the plus1.rom (sha1sum below)

  plus1.rom 04bec46e1bb2259e5444cc7b8017221414165ed7

## ROMs

To use the plus1 and ROMs ensure the plus1.rom line is uncommented in the ini
and the above plus1.rom (or compatible slogger ROM) is located in the same
directory as the basic/os roms.

Transfer to a roms/ folder any games, program or language roms you wish to use.

Via the OSD or editing the ini defaults, toggle the "Plus1 Attached" menu
item to yes. The Electron will need at least a hard reset at this time
CTRL+BREAK.

You can verify the Plus1 is working after loading the core by typing *HELP
and seeing the response:

```
>*HELP
Expansion 1.00
  ADC/Printer/RS423

OS 1.00
>
```

The Plus1 has two cartridge slots each of which supports two 16KB ROMs.
Socket 1 is for rom pages 0 and 1, Socket 2 for pages 2 and 3. ROMs
in socket 1 will take priority.

Some games/programs were a single 16KB ROM in which case you can place
it into any page. Others came as 2x16KB ROMs, for these you should place
the two files in either page 0 and 1, or in page 2 and 3.

Any ROM page you do not wish to use should have the "empty.rom" loaded
into it unless you disable the Plus1 entirely.

You can load ROMs in two ways. At run time via the OSD ROM menu or
if you wish to have your ROM selections persist, you can edit the
ini. These two options are covered in more detail below.

### Ini Configuration

Editing the ini file is recommended if you always want a set of ROMs
to be loaded each time you load the Electron core. For example, to
simulate a LISP ROM cartridge in socket 1 uncomment the page 0
and 1 lines in the ini and edit to match.

```
ROM = roms/lisp_1.rom, 0x4000, 0x40000     # page 0
ROM = roms/lisp_2.rom, 0x4000, 0x44000     # page 1
ROM = empty.rom, 0x4000, 0x48000           # page 2
ROM = empty.rom, 0x4000, 0x4C000           # page 3
```

Alternatively if you wanted two different game ROMs, such as
Starship Command in socket 1 and Countdown to Doom in socket 2

```
ROM = roms/starship_command_1.rom,  0x4000, 0x40000    # page 0
ROM = roms/starship_command_2.rom,  0x4000, 0x44000    # page 1
ROM = roms/countdown_to_doom_1.rom, 0x4000, 0x48000    # page 2
ROM = roms/countdown_to_doom_2.rom, 0x4000, 0x4C000    # page 3
```

### OSD Configuration

You can change which ROMs are loaded at runtime without having to edit
the ini file. This is done via the OSD ROM menu. However, unlike ini file
editing, changes via the OSD will not persist if you reboot the board.

Currently the OSD lists the address each ROM is loaded into including
the OS, Basic and Plus1 ROMs.

For the Plus1 expansion slots, the ROM address/page mapping is:-
  0x40000    page 0
  0x44000    page 1
  0x48000    page 2
  0x4C000    page 3
  0x50000    page 13

Page 13 should not be used unless you know a cartridge included
a page 13 based ROM.

As with the ini file, you can place a 16K ROM into any page, but a 32K
ROM (comprised of 2x16K ROMs) should be loaded into either page 0 & 1 for
cart socket 1 or into page 2 & 3 for cart socket 2.

As with the ini example, if you wish to load the starship command
ROM which is a 32K ROM (2x16K), you load starship_command_1.rom into 0x40000 (page 0)
and starship_command_2.rom into 0x44000 (page1).

After replacing any ROM via the OSD, the core will halt allowing you to load
additional ROMs as required. Whilst the core is halted, you will see a number of
white horizontal bars in the video output. Once your ROM changes are complete, select
"Reboot Target" from the OSD to reset the core to resume normal operation.

NOTE: At this time _ALL_ ROMs are available for switching via the OSD
including the "soldered" 16K OS (0xC000) and Basic (0x8000) ROMs. As well
as the Plus1's expansion ROM (8K mirrored at 0x70000 and 0x72000).

### Usage

Some ROMs (such as games) will auto load when the machine
is switched on preventing you from making use of BASIC (or another
language ROM) and loading the game in the other ROM socket. ROMs
in the page 0/1 socket will take priority.

To prevent this from occurring, press CTRL+BREAK, wait about one second
and then press ESCAPE. This should drop you to the prompt for the active
language.

From here you can select the ROM filing system and list/load a ROM, for
example to load countdown to doom which is in the second socket and not
auto loaded on machine reset:

```
*ROM
*CAT
CHAIN "DOOM"
```

or switch back to the TAPE filing system and load a tape.

```
*TAPE
CHAIN""
```

For more information on ROM usage, please refer to the Acorn Plus1 user manual.

Editing the ini to select ROMs is a temporary requirement. Switching via
the OSD as you can with tapes, will likely be supported by a future firmware
update.

Note: Page 13 is also available as a ROM slot but should not be used
unless you know a ROM cartridge requires it, leave the empty.rom in this slot.

NOTE2: Be aware the Electron will run slower when the Plus1 is active, for example
the following program (idea stolen from the stardot forums :) in MODE 0 takes about
1426ms to run without the Plus1, just over 1600ms with the Plus1 enabled and around
1726ms with ROMs in both cart sockets.

```
10 TIME=0
20 FOR I=0 to 10000:NEXT
30 PRINT TIME
```

You can disable the Plus1 on the fly using:

```
*FX163,128,1
```

and re-enable with

```
*FX163,128,0
```

Alternatively you can physical detached the Plus1 via the OSD "Plus1 Attached"
menu item (followed by CTRL+BREAK).

## Joystick

The Plus1 provides support for two single button joysticks.

Game support for Joysticks is patchy at best. Games have to explicitly support
the Plus1, for example Starship Command.

You can verify your joysticks are working using

```
10 CLS
20 PRINT TAB(0,0);ADVAL(1),ADVAL(2)
30 PRINT TAB(0,0);ADVAL(1),ADVAL(2)
40 PRINT TAB(0,0);ADVAL(0) AND 3
50 GOTO 20
```

Which will output the X and Y axis values for each joystick port as well
as the state of the firebuttons for both ports. For the fire buttons,
0 = neither pressed, 1 = button0 pressed, 2 = button1 pressed, 3 = both pressed.


# Resources

The "Acorn Electron User Guide" is a good starting point. An on-line version
can be found at:

http://www.acornelectron.co.uk/ugs/acorn/ug-english/contents_eng.html

Following on from that is the "Acorn Electron - Advanced User Guide"

It's worth downloading the "Introductory Cassette" to really follow along
with the User Guide and when you're bored of that, hop over to
http://www.elitehomepage.org/c64/index.htm and download the Electron
version of Elite. Perhaps the only game you'll ever need ;)

Numerous games have been tested with this core including, Elite, Hopper,
Sphinx Adventures, Jet Set Willy, Monsters, Repton, Exile and the Introductory
Cassette.

Please report any issues with the core and any games on the fpgaarcade
forum http://www.fpgaarcade.com/punbb/viewforum.php?id=20

