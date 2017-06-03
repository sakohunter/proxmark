# Change Log
All notable changes to this project will be documented in this file.
This project uses the changelog in accordance with [keepchangelog](http://keepachangelog.com/). Please use this to write notable changes, which is not the same as git commit log...

## [unreleased][unreleased]

### Added
- Added experimental HitagS support (Oguzhan Cicek, Hendrik Schwartke, Ralf Spenneberg)
  see https://media.ccc.de/v/32c3-7166-sicherheit_von_125khz_transpondern_am_beispiel_hitag_s
  English video available
- Added a LF ASK Sequence Terminator detection option to the standard ask demod - and applied it to `lf search u`, `lf t55xx detect`, and `data rawdemod am s` (marshmellow)
- `lf t55xx bruteforce <start password> <end password> [i <*.dic>]` - Simple bruteforce attack to find password - (iceman and others)
- `lf viking clone`- clone viking tag to t55x7 or Q5 from 4byte hex ID input 
- `lf viking sim`  - sim full viking tag from 4byte hex ID input
- `lf viking read` - read viking tag and output ID
- `lf t55xx wipe`  - sets t55xx back to factory defaults
- Added viking demod to `lf search` (marshmellow)
- `data askvikingdemod` demod viking id tag from graphbuffer (marshmellow)
- `lf t55xx resetread` added reset then read command - should allow determining start
of stream transmissions (marshmellow)
- `lf t55xx wakeup` added wake with password (AOR) to allow lf search or standard lf read after (iceman, marshmellow)
- `hf iclass managekeys` to save, load and manage iclass keys.  (adjusted most commands to accept a loaded key in memory) (marshmellow)
- `hf iclass readblk` to select, authenticate, and read 1 block from an iclass card (marshmellow)
- `hf iclass writeblk` to select, authenticate, and write 1 block to an iclass card (or picopass) (marshmellow + others)
- `hf iclass clone` to take a saved dump file and clone selected blocks to a new tag (marshmellow + others)
- `hf iclass calcnewkey` - to calculate the div_key change to change a key - (experimental) (marshmellow + others)
- `hf iclass encryptblk` - to encrypt a data block hex to prep for writing that block (marshmellow)
- ISO14443a stand-alone operation with ARM CFLAG="WITH_ISO14443a_StandAlone". This code can read & emulate two banks of 14a tag UIDs and write to "magic" cards  (Craig Young) 
- AWID26 command context added as 'lf awid' containing realtime demodulation as well as cloning/simulation based on tag numbers (Craig Young)
- Added 'hw status'. This command makes the ARM print out some runtime information. (holiman) 
- Added 'hw ping'. This command just sends a usb packets and checks if the pm3 is responsive. Can be used to abort certain operations which supports abort over usb. (holiman)
- Added `data hex2bin` and `data bin2hex` for command line conversion between binary and hexadecimal (holiman)
- Added 'hf snoop'. This command take digitalized signal from FPGA and put in BigBuffer. (pwpiwi + enio)
- Added Topaz (NFC type 1) protocol support ('hf topaz reader', 'hf list topaz', 'hf 14a raw -T', 'hf topaz snoop'). (piwi)
- Added option c to 'hf list' (mark CRC bytes) (piwi)

### Changed
- Added `[l] <length>` option to data printdemodbuffer
- Adjusted lf awid clone to optionally clone to Q5 tags
- Adjusted lf t55xx detect to find Q5 tags (t5555) instead of just t55x7
- Adjusted all lf NRZ demods - works more accurately and consistently (as long as you have strong signal)
- Adjusted lf pskindalademod to reduce false positive reads.
- Small adjustments to psk, nrz, and ask clock detect routines - more reliable.
- Adjusted lf em410x em410xsim to accept a clock argument
- Adjusted lf t55xx dump to allow overriding the safety check and warning text (marshmellow)
- Adjusted lf t55xx write input variables (marshmellow)
- Adjusted lf t55xx read with password safety check and warning text and adjusted the input variables (marshmellow & iceman)
- Adjusted LF FSK demod to account for cross threshold fluctuations (898 count waves will adjust the 9 to 8 now...) more accurate.
- Adjusted timings for t55xx commands.  more reliable now. (marshmellow & iceman)
- `lf cmdread` adjusted input methods and added help text (marshmellow & iceman)
- changed `lf config t <threshold>` to be 0 - 128 and will trigger on + or - threshold value (marshmellow) 
- `hf iclass dump` cli options - can now dump AA1 and AA2 with different keys in one run (does not go to multiple pages for the larger tags yet)
- Revised workflow for StandAloneMode14a (Craig Young)
- EPA functions (`hf epa`) now support both ISO 14443-A and 14443-B cards (frederikmoellers)
- 'hw version' only talks to ARM at startup, after that the info is cached. (pwpiwi)
- Added `r` option to iclass functions - allows key to be provided in raw block 3/4 format 

## [2.2.0][2015-07-12]

### Changed
- Added `hf 14b raw -s` option to auto select a 14b std tag before raw command 
- Changed `hf 14b write` to `hf 14b sriwrite` as it only applied to sri tags (marshmellow)
- Added `hf 14b info` to `hf search` (marshmellow)
- Added compression of fpga config and data, *BOOTROM REFLASH REQUIRED* (piwi)
- Implemented better detection of mifare-tags that are not vulnerable to classic attacks (`hf mf mifare`, `hf mf nested`) (piwi)

### Added
- Add `hf 14b info` to find and print info about std 14b tags and sri tags (using 14b raw commands in the client)  (marshmellow)
- Add PACE replay functionality (frederikmoellers)

### Fixed 
- t55xx write timing (marshmellow)


## [2.1.0][2015-06-23]

### Changed
- Added ultralight/ntag tag type detection to `hf 14a read` (marshmellow)
- Improved ultralight dump command to auto detect tag type, take authentication, and dump full memory (or subset specified) of known tag types (iceman1001 / marshmellow)
- Combined ultralight read/write commands and added authentication (iceman1001)
- Improved LF manchester and biphase demodulation and ask clock detection especially for reads with heavy clipping. (marshmellow)
- Iclass read, `hf iclass read` now also reads tag config and prints configuration. (holiman)
- *bootrom* needs to be flashed, due to new address boundaries between os and fpga, after a size optimization (piwi)

### Fixed
- Fixed EM4x50 read/demod of the tags broadcasted memory blocks. 'lf em4x em4x50read' (not page read) (marshmellow)
- Fixed issue #19, problems with LF T55xx commands (iceman1001, marshmellow)
- Fixed various problems with iso14443b, issue #103 (piwi, marshmellow)

### Added
- Added `hf search` - currently tests for 14443a tags, iclass tags, and 15693 tags (marshmellow) 
- Added `hf mfu info` Ultralight/NTAG info command - reads tag configuration and info, allows authentication if needed (iceman1001, marshmellow)
- Added Mifare Ultralight C and Ultralight EV1/NTAG authentication. (iceman1001)
- Added changelog

## [2.0.0] - 2015-03-25
### Changed
- LF sim operations now abort when new commands arrive over the USB - not required to push the device button anymore.

### Fixed
- Mifare simulation, `hf mf sim` (was broken a long time) (pwpiwi)
- Major improvements in LF area and data operations. (marshmellow, iceman1001)
- Issues regarding LF simulation (pwpiwi)

### Added
- iClass functionality: full simulation of iclass tags, so tags can be simulated with data (not only CSN). Not yet support for write/update, but readers don't seem to enforce update. (holiman).
- iClass decryption. Proxmark can now decrypt data on an iclass tag, but requires you to have the HID decryption key locally on your computer, as this is not bundled with the sourcecode. 


