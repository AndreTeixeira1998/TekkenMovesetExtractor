# Pre-requisites

- Python 3.6.5 specifically
- Pywin32: `python -m pip install pywin32 --user`

# Exporting movesets

This tool exports movesets from memory, you therefore need the game running with the target moveset loaded up already.
The extractor works with both Tekken 7 and Tag 2, as there is little differences between their moveset formats.

## Exporting from Tekken 7
In order to work with Tekken 7, the extractor only needs the player's base address, to be indicated at the entry `p1_ptr` of the file `game_addresses.txt`.
You have to then start a game with the targeted moveset loaded up, and simply running the tool `Ton-Chan's_Motbin_export.py` without any arguments will do the job.

Every moveset extracted from Tekken7 will be prefixed with `7_`

## Exporting from Tag2 (CEMU, Wii U emulator)
In order to work with Tag2, you need to first get the base address of the game in Cemu, and feed it to the variable `cemu_base` in `game_addresses.txt`
This address changes everytime CEMU is started. You can find it by finding any game-related value (an easy one is 32770 for crouching and 32769 for standing, in big endian), then looking at what accesses the value and dumping the r13 register from there. The r13 register will contain the `cemu_base` address.
Then, you need to run the extractor with the argument `tag2`. Example:

`python Ton-Chan's_Motbin_export.py tag2`

Every moveset extracted from Tag2 will be prefixed with `2_`

# Importing moveset into Tekken 7

Movesets are imported directly in memory, requiring the game to be loaded up and being only temporary.
After having extracted a moveset, you can import it like such:

`Ton-Chan's_Motbin_import.py CHARACTER` 

**CHARACTER** is to be replaced with the folder name of the target character, containing the .json and animation data.
Administrator rights may be required to import the moveset into memory.

# TODO:

- Fix Tag2 projectiles (doesn't seem possible at all)
- Fix missing TAG2 commands that use command buffer. Placeholder?
- Alias throw camera values for tag2 (kunimitsu f4 f 4 4 4 4, angel 2+4)
- Make bound use screw ressource?
- Fix parries
- Fix King Tag2 shining wizard that always thinks he's at the wall
- Fix Kunimitsu backturned 4 that doesn't turn around
- Fix bound floorbreak that doesn't bound