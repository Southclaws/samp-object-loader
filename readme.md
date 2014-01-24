# Southclaw's Simple Map Parser

Loads .map files populated with CreateObject (or any variation) lines.
Existence of a 'maps.cfg' file enables Unix style option input.
Currently only supports '-d<0-4>' for various levels of debugging.

Default load directory: ```./scriptfiles/Maps/```


## Supported Syntax

### Objects

```CreateObject(1337, 5.0, -5.0, 3.0, 90.0, 90.0, 90.0);```
```CreateDynamicObject(1337, 5.0, -5.0, 3.0, 90.0, 90.0, 90.0);```

Any string starting with 'Create' is parsed as a CreateObject line, this is also valid:

```CreateCake(1337, 5.0, -5.0, 3.0, 90.0, 90.0, 90.0);```


### Object Materials

```cpp
CreateObject(1337, 5.0, -5.0, 3.0, 90.0, 90.0, 90.0);
SetObjectMaterial(object, 0, 18837, "mickeytextures", "ws_gayflag1", 0);
```
Any ```SetObjectMaterial``` or ```SetObjectMaterialText``` line will affect the last created object.
The first parameter (```objectid```) is ignored and can be any string for flexibility.


### Object Removal

```RemoveBuildingForPlayer(playerid, 615, 0.0, 0.0, 0.0, 200.0);```

'playerid' is ignored, but still valid to allow flexibility when copying from .pwn source code.

When a player connects (or when the filterscript loads, whichever comes first) a list of removed buildings is built and saved for that player.

If the filterscript reloads (perhaps to load an update to object data) any RemoveBuilding instructions that have already been called for each player are ignored. When a player disconnects, their data is discarded.

This data is stored in binary format in ```./scriptfiles/Maps/session/```


### Options

Custom 'function' for altering world, interior and stream distance.
This updates the settings for the current file, any lines below this will use
these settings when creating objects. This function can be used multiple times.

Syntax: ```options(world, interior, stream distance)```

```options(0, 1, 300)```

Set the virtual world to 0, interior to 1 and stream distance to 300


### Comments

Single line ```//``` comments are supported at the end of lines or on their own.

    // comment
    options(0, 1, 200) // comment
    CreateObject(1337, 5.0, -5.0, 3.0, 90.0, 90.0, 90.0); // comment

I have plans for adding block comments in the future.


## Debugging

Create a file inside the default directory called 'maps.cfg'
Use debug option followed by level parameter to make the script load with debug
mode enabled. Each 'level' of debugging offers different information:

* ```-d0``` = Print information messages
* ```-d1``` = Print each folder
* ```-d2``` = Print each loaded file
* ```-d3``` = Print each loaded data line in each file
* ```-d4``` = Print each line in each file


## Todo

More cfg options:

* -r[path] = set the root directory to load maps from
* -s[value] = set default stream distance
* -S[value] = override all per-file stream distances
* -m[value] = set object limit
* -I[path] = include another directory for loading maps

Test more cases of coding styles, line styles, support flexibility.
Block comment support with traditional C syntax ```/* */```
