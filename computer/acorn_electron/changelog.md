# Acorn Electron Core - Change Log

Uses semantic versions. Major version bumps signify a breaking change and
should not be upgraded to blindly. For example, you may require newer ARM
firmware.

## [2.1] - 2019-06-16
### Added
  - Support new FPGA Replay build system, requires python 3

### Changed
  - Support OSD based ROM switching feature added in newer Replay firmware.
    i_halt no longer prevents clocking of ULA, only CPU is halted.
  - Replay Firmware newer than 25th May 2019 required for OSD ROM support.

## [2.0.1] - 2018-07-13
### Fixed
  - Turbo mode will not DOS the ARM/OSD once end of tape reached.
    Truncated fileio response is now correctly handled.

## [2.0.0] - 2018-07-01
### Added
  - Initial Plus 1 expansion support for ROM carts and joysticks.
  - Experimental Turbo Mode for loading from cassette ~6x faster.

### Changed
  - Driver changed to type 2 to use firmware support for loading from UEF.
    Loading now requires ARM firmware version newer than 8th Jan 2018.
  - V/H/CSync polarity changed to negative
  - Remove a couple of unnecessary latches

### Fixed
  - PS2 over serial usage.
  - Support ] Key over serial.

## [1.2.0] - 2018-01-04
### Changed
  - More accurate video address logic

### Fixed
  - Fixes issue with occasional glitch in top quarter of Firetrack

## [1.1.1] - 2017-12-28
### Added
  - Add authentic/compatibility video mode OSD option

### Changed
  - Generate a more accurate Electron PAL signal
  - Improve timing of RTC/DispEnd interrupts based on new PAL signal

## [1.0.0] - 2017-11-28
### Added
  - Improve accuracy of audio waveform with low+high pass filter

### Changed
  - Active video region offset to match Electron.

## [0.2.0] - 2017-11-16
### Fixed
  - Adjust audio tone frequency with extra div2.

## [0.1.0] - 2017-11-04
  - Initial release, feature complete.
