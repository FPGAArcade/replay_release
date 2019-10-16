Prerequisites:

- a Xilinx (web) ISE installation (preferrable any 14.x version)
- Tortoise SVN or any other SVN client
- a Replay 1.0B2 board
- any standard SD card, formatted with FAT / FAT32
- a replay loader setup (can be done the same way as any core set up described here)
- ROM files for the core , get the ROM content from a Phoenix board and name them like this:
    VIDEO EEPROMs (2k x 8bit):
      ic23
      ic24
      ic39
      ic40
    CPU EEPROMs (2k x 8bit):
      ic45
      ic46
      ic47
      ic48
      ic49
      ic50
      ic51
      ic52


Awareness first:

- you got files from a live project repository, so the state of the project may be instable or some work in progress

- do some testing, don't use the builds you generate from this code "as is" - you may also rename some files (see below)

- if you can't live with this, wait for regular releases on the forum (http://www.fpgaarcade.com/punbb/index.php)

- feedback is welcome if you notice something is broken, but you won't get any support for this intermediate versions


Build:

- check out the repository "http://svn.fpgaarcade.com/svn/ReplayPub/"
  (you find the access details here: http://svn.fpgaarcade.com/)

- run up a xilinx ISE command prompt
  (via start menu : "xilinx design tools/ise design suite.../accessories/ise design suite 32/64 command prompt"
   or normal command prompt if your environment is set up correctly via start menu and enter cmd)

- enter the repository directory and build the core (there must not be any errors during the run)
  # cd hw\replay\cores\<core-directory>
  # build


Setup the files on a sdcard:

- enter the sdcard directory or open it in the browser, here you find the result of your build
  * the binary has a default name "loader.bin", you may rename it as you like
  * if you rename it, you also need to modify the line
          bin = loader.bin
    in every ini file to the new file name you chose.
  * you may also adopt the ROM file names in the INI file to load if you use different versions.
- copy the result in a fresh directory of your sdcard
- due to copyright reasons, ROMs are not included in the repository and must be placed separately on the sdcard as well
- unmount the sdcard properly (to ensure a consistent file system) and put it into your Replay board

- just to mention: don't forget to set up the loader files in the root of the sdcard if you want to load multiple cores
  (you may also use only this core, in this case put the files in the root directory rename one of the desired ini files
   to "replay.ini" so it will be found on a Replay boot)

Again:

- USE ALL THIS AT YOUR OWN RISK
- PLEASE DO NOT DISTRIBUTE ROM FILES
