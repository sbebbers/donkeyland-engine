# Donkeyland Engine Notes #

## Pre-amble: ##

The Donkeyland Engine is a text adventure engine written in Commodore BASIC 2 and is intended for the Commodore 64, preferably using an accelerator such as the CMD SuperCPU, although once the game is written, compilation should be considered.

This project has been developed with the excellent CBM prg Studio by Arthur Jordison et al. This easily allows for lines to exceed the default length of 80 character, and provides a very comfy development environment for those used to IDEs for programming and developing for more modern platforms. For information about CBM prg Studio, see http://www.ajordison.co.uk/

By default, no changes are made to the memory map of BASIC, and there is no protection added to the program; this is easily achieved though with the correct POKEs, ie:

POKE 808,234 

will protect the program listing from being human readable with the LIST command, as well as stopping the RUN/STOP and RESTORE combination to break into it when it's running.

To undo this POKE, simply:

POKE 808,237

which will allow you to break into the program and list it again.

## Sub-routines: ##

I have tried to separate out each component of the game into its own sub-routine; this makes it easier to make and track changes to the listing as required. These are listed below:

* 1000 - 1999: Initialisation of the game variables, populating locations and related items and game objects.
* 2000 - 2999: Custom 'INPUT' routine for keyboard handling

## Preset stuff: ##

When I was writing the engine, I decided that each location should have a description of no more than 500 characters, which is half of the C64's 40 columns screen. Therefore, the location string array (LO$) is set to 4, 1 - arrays count from zero, that means in my test engine, there are five locations, each location having enough string space for up to 510 characters. This allows for colour high-lighting as appropriate to emphasise key words and other clues.

My example only handles four directional commands, NORTH, SOUTH, EAST and WEST. Extra boolean logic in the command parsing sub-routine will need to be added for other locations, such as UP, DOWN etc...

## Default variables and uses: ##

```
#!
NAME  TYPE            USAGE

I$    String array    Used to store current inventory items of player.

IT$   String array    Items (first element) and related rooms (second element).

LO$   String array    Location number (first element) and location description (second element).

LR$   String array    Look-up table, linking each room/location (first element) with all available exits (second location).

LN$   String array    Location names.

SM$   String array    Special moves per room.

A$    String          Reusable variable.

B$    String          Buffer.

I     Integer         Reusable index/counter.

R     Integer         Current room/location.

S     Integer         Number of turns taken.

```
## Constants: ##
```
#!
NAME	TYPE        VALUE

N$    String        NORTH

S$    String        SOUTH

E$    String        EAST

W$    String        WEST

D$    String        {space}AND{space}

T$    String        THE{space}

Y$    String        YOU{space}

R$    String        {return}

Q$    String        "

P$    String        {space*3}

Z    Integer        0
```
