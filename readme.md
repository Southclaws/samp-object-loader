# Southclaw's Simple Map Parser

Loads .map files populated with CreateObject (or any variation) lines.
Existence of a 'maps.cfg' file enables Unix style option input.
Currently only supports '-d<0-4>' for various levels of debugging.

Default load directory: ```./scriptfiles/Maps/```


## Supported Syntax

### Objects

```CreateObject(1337, 5.0, -5.0, 3.0, 90.0, 90.0, 90.0);```
```CreateDynamicObject(1337, 5.0, -5.0, 3.0, 90.0, 90.0, 90.0);```

Any string is read as the function name, this is also valid:

```AnythingGoes(1337, 5.0, -5.0, 3.0, 90.0, 90.0, 90.0);```

### Object Removal

```RemoveBuildingForPlayer(playerid, 615, 0.0, 0.0, 0.0, 200.0);```

'playerid' is ignored, but still valid for flexibility.

### Options

Custom 'function' for altering world, interior and stream distance.
This updates the settings for the current file, any lines below this will use
these settings when creating objects. This function can be used multiple times.

Syntax: ```options(world, interior, stream distance)```

```options(0, 0, 300)```

Set the virtual world to 0, interior to 1 and stream distance to 300


### Comments

Single line ```//``` comments are supported at the end of lines or on their own.

    // comment
    options(0, 1, 200) // comment
    CreateObject(1337, 5.0, -5.0, 3.0, 90.0, 90.0, 90.0); // comment



## Debugging

Create a file inside the default directory called 'maps.cfg'
Use debug option followed by level parameter to make the script load with debug
mode enabled. Each 'level' of debugging offers different information:

* ```d0``` = Print information messages
* ```d1``` = Print each folder
* ```d2``` = Print each loaded file
* ```d3``` = Print each loaded data line in each file
* ```d4``` = Print each line in each file


## Todo

More cfg options:

* -r[path] = set the root directory to load maps from
* -s[value] = set default stream distance
* -S[value] = override all per-file stream distances
* -m[value] = set object limit
* -I[path] = include another directory for loading maps

Support for optional Create(Dynamic)Object parameters.
Test more cases of coding styles, line styles, support flexibility.
